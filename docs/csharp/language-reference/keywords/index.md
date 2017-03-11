---
title: "C# 关键字 | Microsoft Docs"
ms.date: "2017-03-07"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "cs.keywords"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "@ 关键字"
  - "C# 语言, 关键字"
  - "关键字 [C#]"
  - "Visual C#, 关键字"
ms.assetid: e929b0f2-4b92-4d37-8060-23d323b098ad
caps.latest.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 22
---
# C# 关键字
关键字是对编译器具有特殊意义的预定义保留标识符。  它们不能在程序中用作标识符，除非它们有一个 `@` 前缀。  例如，`@if` 是有效的标识符，但 `if` 不是，因为 `if` 是关键字。  
  
 本主题中的第一个表列出的关键字在 C\# 程序的任何部分都是保留标识符。  本主题中的第二个表列出了 C\# 中的上下文关键字。  上下文关键字仅在受限制的程序上下文中具有特殊含义，并且可在该上下文外部用作标识符。  通常，在将新关键字添加到 C\# 语言的同时，也会将它们添加为上下文关键字，以便避免破坏用该语言的早期版本编写的程序。  
  
|||||  
|-|-|-|-|  
|[abstract](../../../csharp/language-reference/keywords/abstract.md)|[as](../../../csharp/language-reference/keywords/as.md)|[base](../../../csharp/language-reference/keywords/base.md)|[bool](../../../csharp/language-reference/keywords/bool.md)|  
|[break](../../../csharp/language-reference/keywords/break.md)|[byte](../../../csharp/language-reference/keywords/byte.md)|[case](../../../csharp/language-reference/keywords/switch.md)|[catch](../../../csharp/language-reference/keywords/try-catch.md)|  
|[char](../../../csharp/language-reference/keywords/char.md)|[checked](../../../csharp/language-reference/keywords/checked.md)|[class](../../../csharp/language-reference/keywords/class.md)|[const](../../../csharp/language-reference/keywords/const.md)|  
|[continue](../../../csharp/language-reference/keywords/continue.md)|[decimal](../../../csharp/language-reference/keywords/decimal.md)|[default](../../../csharp/language-reference/keywords/default.md)|[Delegate — 委托](../../../csharp/language-reference/keywords/delegate.md)|  
|[do](../../../csharp/language-reference/keywords/do.md)|[double](../../../csharp/language-reference/keywords/double.md)|[else](../../../csharp/language-reference/keywords/if-else.md)|[enum](../../../csharp/language-reference/keywords/enum.md)|  
|[事件](../../../csharp/language-reference/keywords/event.md)|[explicit](../../../csharp/language-reference/keywords/explicit.md)|[extern](../../../csharp/language-reference/keywords/extern.md)|[false](../../../csharp/language-reference/keywords/false.md)|  
|[finally](../../../csharp/language-reference/keywords/try-finally.md)|[fixed](../../../csharp/language-reference/keywords/fixed-statement.md)|[float](../../../csharp/language-reference/keywords/float.md)|[for](../../../csharp/language-reference/keywords/for.md)|  
|[foreach](../../../csharp/language-reference/keywords/foreach-in.md)|[goto](../../../csharp/language-reference/keywords/goto.md)|[if](../../../csharp/language-reference/keywords/if-else.md)|[implicit](../../../csharp/language-reference/keywords/implicit.md)|  
|[in](../../../csharp/language-reference/keywords/foreach-in.md)|[in（泛型修饰符）](../../../csharp/language-reference/keywords/in-generic-modifier.md)|[int](../../../csharp/language-reference/keywords/int.md)|[interface](../../../csharp/language-reference/keywords/interface.md)|  
|[internal](../../../csharp/language-reference/keywords/internal.md)|[为](../../../csharp/language-reference/keywords/is.md)|[lock](../../../csharp/language-reference/keywords/lock-statement.md)|[long](../../../csharp/language-reference/keywords/long.md)|  
|[命名空间](../../../csharp/language-reference/keywords/namespace.md)|[new](../../../csharp/language-reference/keywords/new.md)|[null](../../../csharp/language-reference/keywords/null.md)|[对象](../../../csharp/language-reference/keywords/object.md)|  
|[operator](../../../csharp/language-reference/keywords/operator.md)|[out](../../../csharp/language-reference/keywords/out.md)|[out（泛型修饰符）](../../../csharp/language-reference/keywords/out-generic-modifier.md)|[override](../../../csharp/language-reference/keywords/override.md)|  
|[params](../../../csharp/language-reference/keywords/params.md)|[private](../../../csharp/language-reference/keywords/private.md)|[protected](../../../csharp/language-reference/keywords/protected.md)|[public](../../../csharp/language-reference/keywords/public.md)|  
|[readonly](../../../csharp/language-reference/keywords/readonly.md)|[ref](../../../csharp/language-reference/keywords/ref.md)|[return](../../../csharp/language-reference/keywords/return.md)|[sbyte](../../../csharp/language-reference/keywords/sbyte.md)|  
|[sealed](../../../csharp/language-reference/keywords/sealed.md)|[short](../../../csharp/language-reference/keywords/short.md)|[sizeof](../../../csharp/language-reference/keywords/sizeof.md)|[stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)|  
|[static](../../../csharp/language-reference/keywords/static.md)|[string](../../../csharp/language-reference/keywords/string.md)|[struct](../../../csharp/language-reference/keywords/struct.md)|[switch](../../../csharp/language-reference/keywords/switch.md)|  
|[this](../../../csharp/language-reference/keywords/this.md)|[throw](../../../csharp/language-reference/keywords/throw.md)|[true](../../../csharp/language-reference/keywords/true.md)|[try](../../../csharp/language-reference/keywords/try-catch.md)|  
|[typeof](../../../csharp/language-reference/keywords/typeof.md)|[uint](../../../csharp/language-reference/keywords/uint.md)|[ulong](../../../csharp/language-reference/keywords/ulong.md)|[unchecked](../../../csharp/language-reference/keywords/unchecked.md)|  
|[unsafe](../../../csharp/language-reference/keywords/unsafe.md)|[ushort](../../../csharp/language-reference/keywords/ushort.md)|[using](../../../csharp/language-reference/keywords/using.md)|[virtual](../../../csharp/language-reference/keywords/virtual.md)|  
|[void](../../../csharp/language-reference/keywords/void.md)|[volatile](../../../csharp/language-reference/keywords/volatile.md)|[while](../../../csharp/language-reference/keywords/while.md)||  
  
## 上下文关键字  
 上下文关键字用于提供代码中的特定含义，但它不是 C\# 中的保留字。  某些上下文关键字（如 `partial` 和 `where`）在两个或更多个上下文中具有特殊含义。  
  
||||  
|-|-|-|  
|[添加](../../../csharp/language-reference/keywords/add.md)|[Alias — 别名](../../../csharp/language-reference/keywords/extern-alias.md)|[ascending](../../../csharp/language-reference/keywords/ascending.md)|  
|[async](../../../csharp/language-reference/keywords/async.md)|[等待](../../../csharp/language-reference/keywords/await.md)|[descending](../../../csharp/language-reference/keywords/descending.md)|  
|[dynamic](../../../csharp/language-reference/keywords/dynamic.md)|[from](../../../csharp/language-reference/keywords/from-clause.md)|[get](../../../csharp/language-reference/keywords/get.md)|  
|[global](../../../csharp/language-reference/keywords/global.md)|[group](../../../csharp/language-reference/keywords/group-clause.md)|[into](../../../csharp/language-reference/keywords/into.md)|  
|[join](../../../csharp/language-reference/keywords/join-clause.md)|[let](../../../csharp/language-reference/keywords/let-clause.md)|[orderby](../../../csharp/language-reference/keywords/orderby-clause.md)|  
|[partial（类型）](../../../csharp/language-reference/keywords/partial-type.md)|[partial（方法）](../../../csharp/language-reference/keywords/partial-method.md)|[remove](../../../csharp/language-reference/keywords/remove.md)|  
|[select](../../../csharp/language-reference/keywords/select-clause.md)|[set](../../../csharp/language-reference/keywords/set.md)|[value](../../../csharp/language-reference/keywords/value.md)|  
|[var](../../../csharp/language-reference/keywords/var.md)|[where（泛型类型约束）](../../../csharp/language-reference/keywords/where-generic-type-constraint.md)|[where（查询子句）](../../../csharp/language-reference/keywords/where-clause.md)|  
|[yield](../../../csharp/language-reference/keywords/yield.md)||  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)