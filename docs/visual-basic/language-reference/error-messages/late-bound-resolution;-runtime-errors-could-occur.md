---
title: "后期绑定解决方案；可能会发生运行时错误 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc42017"
  - "BC42017"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42017"
ms.assetid: 45f552c8-57c6-44c0-97d3-e510119b257a
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 后期绑定解决方案；可能会发生运行时错误
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

为声明为 [Object 数据类型](../../../visual-basic/language-reference/data-types/object-data-type.md) 的变量指派了对象。  
  
 当您将变量声明为 `Object` 时，编译器必须执行“后期绑定”，这将会导致在运行时出现额外的操作。  它还使应用程序易于发生潜在的运行时错误。  例如，如果将 <xref:System.Windows.Forms.Form> 指派给 `Object` 变量，然后尝试访问 <xref:System.Xml.XmlDocument.NameTable%2A?displayProperty=fullName> 属性，则运行时会引发 <xref:System.MemberAccessException>，因为 <xref:System.Windows.Forms.Form> 类不会公开 `NameTable` 属性。  
  
 如果将变量声明为某个具体类型，编译器将能在编译时执行“早期绑定”。  这样，性能将会提高，对特定类型成员的访问可得到控制，并且您的代码的可读性将更好。  
  
 默认情况下，此消息是一个警告。  有关隐藏警告或将警告视为错误的信息，请参见 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC42017  
  
### 更正此错误  
  
-   如有可能，请将变量声明为具体类型。  
  
## 请参阅  
 [早期绑定和后期绑定](../../../visual-basic/programming-guide/language-features/early-late-binding/early-and-late-binding.md)   
 [对象变量声明](../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)