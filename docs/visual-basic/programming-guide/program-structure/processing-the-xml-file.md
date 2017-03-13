---
title: "处理 XML 文件 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "XML 注释, 分析 [Visual Basic]"
ms.assetid: 78a15cd0-7708-4e79-85d1-c154b7a14a8c
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# 处理 XML 文件 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

编译器为代码中被标记为生成文档的每一个构造生成一个 ID 字符串。  （有关如何标记代码的信息，请参见 [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)。）ID 字符串唯一地标识构造。  处理 XML 文件的程序可以使用 ID 字符串标识相应的 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 元数据\/反射项。  
  
 XML 文件不是代码的分层表示形式，它是一个平面列表，每一个元素有一个生成的 ID。  
  
 编译器在生成 ID 字符串时遵循下列规则：  
  
-   不在字符串中放置空白。  
  
-   ID 字符串的第一部分通过单个字符后跟一个冒号来标识被标识成员的种类。  使用下列成员类型。  
  
|||  
|-|-|  
|字符|说明|  
|N|命名空间<br /><br /> 不可将文档注释添加到命名空间中，但是可以对它们进行 CREF 引用（在受支持的位置）。|  
|T|类型：`Class`、`Module`、`Interface`、`Structure`、`Enum`、`Delegate`|  
|F|字段：`Dim`|  
|P|属性：`Property`（包括默认属性）|  
|M|方法：`Sub`、`Function`、`Declare`、`Operator`|  
|E|事件：`Event`|  
|\!|错误字符串<br /><br /> 字符串的其余部分会提供有关此错误的信息。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器为无法解析的链接生成错误信息。|  
  
-   `String` 的第二部分是项的完全限定名，从命名空间的根开始。  项的名称、其封闭类型和命名空间以句点分隔。  如果项的名称本身包含句点，则用数字符号 \(\#\) 替换这些句点。  假设任何项的名称中都未直接包含数字符号。  例如，`String` 构造函数的完全限定名是 `System.String.#ctor`。  
  
-   对于属性和方法，如果该方法带参数，则将其后的参数列表括在括号中。  如果没有参数，则没有括号。  多个参数以逗号分隔。  每个参数的编码都直接遵循它在 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 签名中的编码方法。  
  
## 示例  
 下面的代码演示如何生成类及其成员的 ID 字符串。  
  
 [!code-vb[VbVbcnXmlDocComments#10](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/processing-the-xml-file_1.vb)]  
  
## 请参阅  
 [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md)   
 [如何：创建 XML 文档](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)