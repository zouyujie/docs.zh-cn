---
title: "框架和目标"
description: "解释编写 .NET 代码时的框架目标概念。"
keywords: .NET, .NET Core
author: richlander
manager: wpickett
ms.date: 09/19/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 6ef56a2e-593d-497b-925a-1e25bb6df2e6
translationtype: Human Translation
ms.sourcegitcommit: 38561c2d25c6950d166bf706f4306c867e683b04
ms.openlocfilehash: 82ba6f4abe200dc48158eac1ad3e3609feeda2c9

---

# <a name="frameworks-and-targets"></a>框架和目标

.NET 生态系统使用框架的概念。 框架定义了可用于指定特定平台的目标的 API。 .NET Framework 4.6 就是这样一种平台。 在 Visual Studio、其他 IDE 和编辑器中使用框架可以提供正确的 API 集。 NuGet 也可以通过框架来生成和使用 NuGet 包，确保针对目标框架生成并使用适当的包（和基础资产）。 可将框架看作 .NET 生态系统中的关键货币之一。 推出这一概念是为了确保准确性，帮助你以及你的客户避免遇到 @System.MissingMethodException 和类似异常。

## <a name="framework-versions"></a>框架版本

下表定义了可以使用的框架集、如何引用这些框架，以及它们实现哪个 [.NET 标准库](library.md)版本。

| 框架 | 最新版本 | 目标框架名字对象 (TFM) | 精简目标框架名字对象 (TFM) | .NET Standard 版本 | 元包 |
|:--------: | :--: | :--: | :--: | :--: | :--: | :--: |
| .NET Standard | 1.6 | .NETStandard,Version=1.6 | netstandard1.6 | 不可用 | [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library)|
| .NET Core 应用程序 | 1.0.1 | .NETCoreApp,Version=1.0 | netcoreapp1.0 | 1.6 | [Microsoft.NETCore.App](https://www.nuget.org/packages/Microsoft.NETCore.App)|
| .NET Framework | 4.6.2 | .NETFramework,Version=4.6.2 | net462 | 1.5 | 不可用 |

> [!NOTE]
> 这些框架版本是最新的稳定版本。 可能还有此表格并未提到的一些预发行版。

## <a name="writing-about-frameworks"></a>有关框架的书面内容

可通过多种方式以书面形式提到框架，本文档使用了其中的大多数形式。 下面介绍了这些形式，目的是举例解释如何阅读本文档，同时帮助读者在其他文档中理解这些形式。

以 .NET Framework 4.6.1 为例，可以使用以下形式：

**提到产品**

可以提到 .NET 平台或运行时。

- ".NET Framework 4.6.1"

**提到框架**

可以使用 TFM 的完整形式或缩写形式提到框架或框架的目标。 一般情况下，这两种形式都是有效的。

- `.NETFramework,Version=4.6.1`
- `net461`

**提到框架系列**

可以使用框架 ID 的完整形式或缩写形式提到框架系列。 一般情况下，这两种形式都是有效的。

- `.NETFramework`
- `net`



<!--HONumber=Nov16_HO3-->


