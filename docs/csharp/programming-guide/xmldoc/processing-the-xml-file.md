---
title: "处理 XML 文件（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "XML [C#], 处理"
  - "XML 处理 [C#]"
ms.assetid: 60c71193-9dac-4cd3-98c5-100bd0edcc42
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# 处理 XML 文件（C# 编程指南）
编译器为代码中被标记为生成文档的每一个构造生成一个 ID 字符串。  （有关如何标记代码的信息，请参见[建议的文档注释标记](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)。）ID 字符串唯一地标识构造。  处理 XML 文件的程序可以使用 ID 字符串标识文档应用于的相应 .NET Framework 元数据\/反射项。  
  
 XML 文件不是代码的分层表示形式，它是一个平面列表，其中的每一个元素都有一个生成的 ID。  
  
 编译器在生成 ID 字符串时遵循下列规则：  
  
-   字符串中没有空白。  
  
-   ID 字符串的第一部分通过单个字符后跟一个冒号来标识所标识成员的种类。  使用下列成员类型：  
  
    |字符|说明|  
    |--------|--------|  
    |N|命名空间<br /><br /> 不可将文档注释添加到命名空间中，但是可以对它们进行 cref 引用（在受支持的位置）。|  
    |T|类型：类、接口、结构、枚举、委托|  
    |F|字段|  
    |P|属性（包括索引程序或其他索引属性）|  
    |M|方法（包括一些特殊方法，例如构造函数、运算符等）|  
    |E|事件|  
    |\!|错误字符串<br /><br /> 字符串的其余部分会提供有关此错误的信息。  C\# 编译器为无法解析的链接生成错误信息。|  
  
-   字符串的第二部分是项的完全限定名，从命名空间的根开始。  项的名称、其封闭类型和命名空间以句号分隔。  如果项的名称本身包含句号，则用哈希符号 \('\#'\) 替换这些句号。  假定任何项的名称中都不直接存在哈希符号。  例如，String 构造函数的完全限定名是“System.String.\#ctor”。  
  
-   对于属性和方法，如果该方法带参数，则将其后的参数列表括在括号中。  如果没有参数，则没有括号。  多个参数以逗号分隔。  每个参数的编码都直接遵循它在 .NET Framework 签名中的编码方法：  
  
    -   基类型。  常规类型（ELEMENT\_TYPE\_CLASS 或 ELEMENT\_TYPE\_VALUETYPE）表示为类型的完全限定名。  
  
    -   内部类型（例如，ELEMENT\_TYPE\_I4、ELEMENT\_TYPE\_OBJECT、ELEMENT\_TYPE\_STRING、ELEMENT\_TYPE\_TYPEDBYREF。  和 ELEMENT\_TYPE\_VOID）表示为相应完全类型的完全限定名。  例如，System.Int32 或 System.TypedReference。  
  
    -   ELEMENT\_TYPE\_PTR 表示为“\*”，在修改的类型之后。  
  
    -   ELEMENT\_TYPE\_BYREF 表示为“@”，在修改的类型之后。  
  
    -   ELEMENT\_TYPE\_PINNED 表示为“^”，在修改的类型之后。  C\# 编译器永远不会生成此结果。  
  
    -   ELEMENT\_TYPE\_CMOD\_REQ 表示为“&#124;”和修饰符类的完全限定名，在修改的类型之后。  C\# 编译器永远不会生成此结果。  
  
    -   ELEMENT\_TYPE\_CMOD\_OPT 表示为“\!”和修饰符类的完全限定名，在修改的类型之后。  
  
    -   ELEMENT\_TYPE\_SZARRAY 表示为“\[\]”，在数组的元素类型之后。  
  
    -   ELEMENT\_TYPE\_GENERICARRAY 表示为“\[?\]”，在数组的元素类型之后。  C\# 编译器永远不会生成此结果。  
  
    -   ELEMENT\_TYPE\_ARRAY 表示为 \[*lowerbound*:`size`,*lowerbound*:`size`\]，其中逗号数为秩 \- 1，每一维的下限和大小（如果已知）用十进制表示。  如果未指定下限及大小，它将完全被省略。  如果省略了特定维的下限及大小，则“:”也将被省略。  例如，以 1 作为下限并且未指定大小的二维数组是 \[1:,1:\]。  
  
    -   ELEMENT\_TYPE\_FNPTR 表示为“\=FUNC:`type`\(*signature*\)”，其中 `type` 是返回类型，*signature* 是方法的参数。  如果没有参数，则将省略括号。  C\# 编译器永远不会生成此结果。  
  
     不表示下列签名组件，因为从不使用它们来区分重载方法：  
  
    -   调用约定  
  
    -   返回类型  
  
    -   ELEMENT\_TYPE\_SENTINEL  
  
-   仅对于转换运算符（op\_Implicit 和 op\_Explicit），方法的返回值才被编码为“~”，后跟返回类型，如上述编码所示。  
  
-   对于泛型类型，类型名称后跟反勾号，再跟一个数字，指示泛型类型参数的个数。  例如，  
  
     对于定义为 `public class SampleClass<T, U>` 的类型，`<member name="T:SampleClass`2">` 是其标记。  
  
     对于接受泛型类型作为参数的方法，泛型类型参数被指定为数字前面加上反勾号（如 \`0、\`1）。  表示类型泛型参数的数组表示法（从零开始）的每个数字。  
  
## 示例  
 下列示例显示了如何生成类及其成员的 ID 字符串：  
  
 [!code-cs[csProgGuidePointers#21](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/processing-the-xml-file_1.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [\/doc \(Process Documentation Comments\)](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)   
 [XML 文档注释](../../../csharp/programming-guide/xmldoc/xml-documentation-comments.md)