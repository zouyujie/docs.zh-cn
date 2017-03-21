---
title: "Imports 语句（XML 命名空间） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.ImportsXmlns"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "导入 [Visual Basic]"
  - "Imports 语句 [Visual Basic]"
  - "命名空间 [Visual Basic], 导入"
  - "XML 命名空间 [Visual Basic], 导入"
ms.assetid: 1f4d50a6-08c7-4c2e-8206-ccae35fcd1b4
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Imports 语句（XML 命名空间）
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

导入 XML 命名空间前缀以便在 XML 文本和 XML 轴属性中使用。  
  
## 语法  
  
```  
Imports <xmlns:xmlNamespacePrefix = "xmlNamespaceName">  
```  
  
## 部件  
 `xmlNamespacePrefix`  
 可选。  XML 元素和特性用来引用 `xmlNamespaceName` 的字符串。  如果未提供 `xmlNamespacePrefix`，则导入的 XML 命名空间为默认 XML 命名空间  必须是有效的 XML 标识符。  有关更多信息，请参见 [已声明的 XML 元素和特性的名称](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)。  
  
 `xmlNamespaceName`  
 必选。  标识要导入的 XML 命名空间的字符串。  
  
## 备注  
 使用 `Imports` 语句可以定义可用于 XML 文本和 XML 轴属性或用作传递给 `GetXmlNamespace` 运算符的参数的全局 XML 命名空间。  （有关使用 `Imports` 语句导入可在代码中使用类型名称的位置使用的别名的信息，请参见 [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)。）使用 `Imports` 语句声明 XML 命名空间的语法与 XML 中使用的语法相同。  因此，可以从 XML 文件复制命名空间声明并在 `Imports` 语句中使用该声明。  
  
 如果需要重复创建同一命名空间的 XML 元素，XML 命名空间前缀会很有用。  文件中的所有代码都可以使用通过 `Imports` 语句声明的 XML 命名空间前缀，从这一意义上说，它是全局性的。  您可以在创建 XML 元素文本和访问 XML 轴属性时使用它。  有关更多信息，请参见[XML 元素文本](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)和 [XML 轴属性](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)。  
  
 如果定义一个不带命名空间前缀的全局 XML 命名空间（例如 `Imports <xmlns="http://SomeNameSpace>"`），则该命名空间将被视为默认 XML 命名空间。  默认 XML 命名空间被用于任何不显式指定命名空间的 XML 元素文本或 XML 特性轴属性。  如果指定的命名空间为空命名空间（即 `xmlns=""`），则也会使用默认命名空间。  默认 XML 命名空间不适用于 XML 文本中的 XML 特性以及没有命名空间的 XML 特性轴属性。  
  
 XML 文本中定义的 XML 命名空间（称为“本地 XML 命名空间”）优先于被 `Imports` 语句定义为全局命名空间的 XML 命名空间。  `Imports` 语句定义的 XML 命名空间优先于为 Visual Basic 项目导入的 XML 命名空间。  如果 XML 文本定义了 XML 命名空间，则本地命名空间不适用于嵌入式表达式。  
  
 全局 XML 命名空间遵循和 .NET Framework 命名空间相同的范围和定义规则。  因此，可以包含 `Imports` 语句以便在可以导入 .NET Framework 命名空间的任何位置定义全局 XML 命名空间。  这包括代码文件级和项目级导入命名空间。  有关项目级导入命名空间的信息，请参见[项目设计器 \-\>“引用”页 \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic)。  
  
 每个源文件可以包含任意数量的 `Imports` 语句。  这些语句必须位于选项声明（如 `Option Strict` 语句）之后、编程元素声明（如 `Module` 或 `Class` 语句）之前。  
  
## 示例  
 下面的示例导入一个默认 XML 命名空间和一个用前缀 `ns` 标识的 XML 命名空间。  然后，创建使用这两个命名空间的 XML 文本。  
  
 [!code-vb[VbXMLSamples#45](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/imports-statement-xml-namespace_1.vb)]  
  
 这段代码将显示以下文本：  
  
```  
<ns:outer xmlns="http://DefaultNamespace"   
          xmlns:ns="http://NewNamespace">  
  <ns:innerElement></ns:innerElement>  
  <siblingElement></siblingElement>  
  <innerElement />  
</ns:outer>  
```  
  
## 示例  
 下面的示例导入 XML 命名空间前缀 `ns`。  然后，该示例创建一个使用该命名空间前缀的 XML 文本，并显示该元素的最终形式。  
  
 [!code-vb[VbXMLSamples#22](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/imports-statement-xml-namespace_2.vb)]  
  
 这段代码将显示以下文本：  
  
```  
<ns:outer xmlns:ns="http://SomeNamespace">  
  <ns:middle xmlns:ns="http://NewNamespace">  
    <ns:inner1 />  
    <inner2 xmlns="http://SomeNamespace" />  
  </ns:middle>  
</ns:outer>  
```  
  
 请注意，编译器将 XML 命名空间前缀从全局前缀转换为本地前缀定义。  
  
## 示例  
 下面的示例导入 XML 命名空间前缀 `ns`。  然后，该示例使用该命名空间前缀创建 XML 文本并访问第一个具有限定名 `ns:name` 的子节点。  
  
 [!code-vb[VbXMLSamples#19](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/imports-statement-xml-namespace_3.vb)]  
  
 这段代码将显示以下文本：  
  
 `Patrick Hines`  
  
## 请参阅  
 [XML 元素文本](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML 轴属性](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [已声明的 XML 元素和特性的名称](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)   
 [GetXmlNamespace 运算符](../../../visual-basic/language-reference/operators/getxmlnamespace-operator.md)