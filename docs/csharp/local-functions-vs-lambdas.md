---
title: "本地函数与 Lambda 表达式"
description: "为什么选择本地函数可能比选择 Lambda 表达式更好"
keywords: "C#, .NET, .NET Core, 最新功能, 新增功能, 本地函数, Lambda 表达式"
author: BillWagner
ms.author: wiwagn
ms.date: 10/27/2016
ms.topic: article
ms.prod: visual-studio-dev-15
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 368d1752-3659-489a-97b4-f15d87e49ae3
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: bba2a8d183f928e298c452f6ec132f3eb9dffbd3
ms.lasthandoff: 03/13/2017

---

### <a name="local-functions-compared-to-lambda-expressions"></a>本地函数与 Lambda 表达式比较

在某些用例中，可以创建并使用 lambda 表达式，而无需创建本地函数。 以下就是采用这种操作的异步方法示例：

[!code-csharp[TaskLambdaExample](../../samples/snippets/csharp/new-in-7/AsyncWork.cs#36_TaskLambdaExample "使用 lambda 表达式返回方法的任务")]

但是，建议使用本地函数，而不是定义和调用 lambda 表达式，原因如下。

首先，对于 lambda 表达式，编译器必须创建匿名类和该类的实例以存储任何由闭包捕获的变量。 该 lambda 表达式的闭包包含 `address`、`index` 和 `name` 变量。 

其次，lambda 表达式是通过实例化委托并调用该委托来实现的。 而本地函数是作为方法调用来实现的。
Lambda 表达式所需的实例化意味着额外的内存分配，后者可能是时间关键代码路径中的性能因素。
本地函数不会产生这种开销。

第三，本地函数可以在定义前进行调用。 必须先声明 Lambda 表达式，然后再进行定义。 这意味着本地函数在递归算法中更易于使用：

[!code-csharp[LocalFunctionFactorial](../../samples/snippets/csharp/new-in-7/MathUtilities.cs#37_LocalFunctionFactorial "使用本地函数实现阶乘递归")]

将该实现与使用 Lambda 表达式的版本对比：

[!code-csharp[26_LambdaFactorial](../../samples/snippets/csharp/new-in-7/MathUtilities.cs#38_LambdaFactorial "使用 lambda 表达式实现阶乘递归")]

请注意，使用 lambda 表达式的版本必须先定义 lambda 表达式 `nthFactorial`，然后再对其进行声明并实例化。 否则，会导致分配前引用 `nthFactorial` 时出现编译时错误。
使用本地函数创建递归算法更轻松。 

虽然本地函数对 lambda 表达式可能有点冗余，但实际上它们的目的和用法都不一样。
如果想要编写仅从上下文或其他方法中调用的函数，则使用本地函数更高效。


