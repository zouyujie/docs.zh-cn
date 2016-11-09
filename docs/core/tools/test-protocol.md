---
title: ".NET Core CLI 测试通信协议"
description: ".NET Core CLI 测试通信协议"
keywords: .NET, .NET Core
author: mairaw
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 88cba792-3640-41de-b55d-00f575e9d5e2
translationtype: Human Translation
ms.sourcegitcommit: 81e7604f0a646e5de9c2ed35ff3b6ef6d7fb2e71
ms.openlocfilehash: a35385cbb08614493fdcfc74504b00178dc532ea

---

#<a name="net-core-cli-test-communication-protocol"></a>.NET Core CLI 测试通信协议

## <a name="introduction"></a>介绍
每次将端口传递给 dotnet 测试时，命令将在设计时运行。 这意味着 dotnet 测试将使用 TCP 连接到该端口，然后与连接到此端口的其他任何内容交换一组已确定的消息。 发生这种情况时，运行程序还会收到 dotnet 测试将用于与其通信的新端口。 运行程序也使用 TCP 与 dotnet 测试通信的原因是因为，在设计模式中，仅将结果输出到控制台是不够的。 命令需要发送包含测试执行结果的适配器结构消息。

### <a name="communication-protocol-at-design-time"></a>设计时的通信协议。

1. 由于在设计时期间，dotnet 测试在启动时会连接到某个端口，因此适配器需要侦听此端口，否则 dotnet 测试将失败。 这样一来，适配器可通过在 dotnet 测试运行和尝试获取运行程序的端口前绑定和侦听这些端口，保留它所需的所有端口。
2. dotnet 测试启动后，将向适配器发送 TestSession.Connected 消息，指示它已准备好接收消息。
3. 可以在发送可选[版本检查](https://github.com/dotnet/cli/blob/rel/1.0.0/src/Microsoft.Extensions.Testing.Abstractions/Messages/ProtocolVersionMessage.cs)消息时，随附协议的适配器版本。 Dotnet 测试将发送回其支持的协议版本。

所有消息都采用此处所述的格式：[Message.cs](https://github.com/dotnet/cli/blob/rel/1.0.0/src/Microsoft.Extensions.Testing.Abstractions/Messages/Message.cs)。 每条消息的有效负载格式在指向用于序列化/反序列化协议描述中信息的类的链接中有所介绍。

#### <a name="test-execution"></a>测试执行
![测试执行](./media/test-protocol/dotnet-test-execute.png)

1. 可选版本检查后，适配器会发送 TestExecution.GetTestRunnerProcessStartInfo，内含适配器希望在其中执行的[测试](https://github.com/dotnet/cli/blob/rel/1.0.0/src/Microsoft.Extensions.Testing.Abstractions/Messages/RunTestsMessage.cs)。 Dotnet 测试会在适配器可用于启动运行程序的 [TestStartInfo](https://github.com/dotnet/cli/blob/rel/1.0.0/src/Microsoft.DotNet.Tools.Test/TestStartInfo.cs) 有效负载内发送回文件名和参数。 过去，我们会发送测试列表作为参数的一部分进行运行，但对某些测试项目来说，我们实际上要超过了命令行大小限制。
  1. 作为参数的一部分，我们会发送运行程序应连接的端口，而对于执行测试，会发送一个 --wait-command 标志，指示运行程序应连接到端口并等待命令，而不是继续执行测试。
2. 此时，适配器可以启动运行程序（并附加到运行程序进行调试，如果选择这样做的话）。
3. 运行程序启动后，会向 dotnet 测试发送 TestRunner.WaitCommand 消息，指示它已准备好接收命令，此时 dotnet 测试会发送 TestRunner.Execute，随附要运行的[测试](https://github.com/dotnet/cli/blob/rel/1.0.0/src/Microsoft.Extensions.Testing.Abstractions/Messages/RunTestsMessage.cs)列表。 这将绕过上述的命令行大小限制。
4. 启动时，运行程序会向 dotnet 测试发送用于每个测试的 TestExecution.TestStarted（dotnet 测试再传递到适配器），其中随附[测试](https://github.com/dotnet/cli/blob/rel/1.0.0/src/Microsoft.Extensions.Testing.Abstractions/Test.cs)信息。
5. 运行程序也会向 dotnet 测试发送用于每个测试的 TestExecution.TestResult（dotnet 测试再转发到适配器），随附测试的[各个结果](https://github.com/dotnet/cli/blob/rel/1.0.0/src/Microsoft.Extensions.Testing.Abstractions/TestResult.cs)。
6. 所有测试完成后，运行程序将向 dotnet 测试发送 TestRunner.Completed 消息，dotnet 测试再将该消息作为 TestExecution.Completed 发送到适配器。
7. 适配器完成操作后，会向 dotnet 测试发送 TestSession.Terminate，这将关闭 dotnet 测试。

#### <a name="test-discovery"></a>测试发现
![测试发现](./media/test-protocol/dotnet-test-discover.png)

1. 可选版本检查后，适配器发送 TestDiscovery.Start 消息。 因为在这种情况下，适配器并不需要附加到进程，dotnet 测试将自己启动运行程序。 此外，由于没有要传递到运行程序的参数长列表，因此无需将 --wait-command 标志传递到运行程序。 dotnet 测试仅将 --list 参数传递到运行程序，这意味着运行程序不应运行测试，而应仅列出测试。
2. 然后，运行程序向 dotnet 测试发送用于每个找到的[测试](https://github.com/dotnet/cli/blob/rel/1.0.0/src/Microsoft.Extensions.Testing.Abstractions/Test.cs)的 TestDiscovery.TestFound（dotnet 测试再传递到适配器）。
3. 发现所有测试后，运行程序将向 dotnet 测试发送 TestRunner.Completed 消息，dotnet 测试再将该消息作为 TestDiscovery.Completed 发送到适配器。
4. 适配器完成操作后，会向 dotnet 测试发送 TestSession.Terminate，这将关闭 dotnet 测试。


<!--HONumber=Nov16_HO1-->


