---
title: "如何：使用 XML 文档功能（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "XML 文档 [C#]"
  - "C# 语言中，XML 文档功能"
ms.assetid: 8f33917b-9577-4c9a-818a-640dbbb0b399
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# 如何：使用 XML 文档功能（C# 编程指南）
下面的示例为提供已存档的类型的基本的概述。  
  
## <a name="example"></a>示例  
 [!code-cs[csProgGuideDocComments#15](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/how-to-use-the-xml-documentation-features_1.cs)]  
  
 **使用上面的代码示例生成该.xml 文件。**  
**\<？ xml 版本 ="1.0"？>**  
**\< 文档>**  
 **\< 程序集>**  
 **\< 名称>xmlsample \< / 名称>**  
 **\< / 程序集>**  
 **\< 成员>**  
 **\< 成员名称 ="T:SomeClass">**  
 **\< 摘要>**  
 **类级别摘要文档进入这里。 \< / 摘要>**  
 **\< 备注>**  
 **较长的注释可与一个类型或成员相关联**   
 **通过备注标记 \< / 备注>**  
 **\< / 成员>**  
 **\< 成员 name="F:SomeClass.m_Name">**  
 **\< 摘要>**  
 **名称属性的应用商店 \< / 摘要>**  
 **\< / 成员>**  
 **\< 成员名称 ="M:SomeClass.#ctor">**  
 **\< 摘要>类构造函数。 \< / 摘要>**   
 **\< / 成员>**  
 **\< 成员 name="M:SomeClass.SomeMethod(System.String)">**  
 **\< 摘要>**  
 **描述 SomeMethod。 \< / 摘要>**  
 **\< 参数名称 ="s"> s 的参数说明此处 \< / 参数>**  
 **\< seealso cref="T:System.String">**  
 **可以使用任何标记上 cref 特性来引用类型或成员**   
 **编译器将检查存在该引用。\< / seealso>**  
 **\< / 成员>**  
 **\< 成员 name="M:SomeClass.SomeOtherMethod">**  
 **\< 摘要>**  
 **一些其他方法。\< / 摘要>**  
 **\< 返回>**  
 **返回结果通过返回标记。 描述 \< / 返回>**  
 **\< seealso cref="M:SomeClass.SomeMethod(System.String)">**  
 **请注意使用 cref 特性来引用特定的方法 \< / seealso>**  
 **\< / 成员>**  
 **\< 成员 name="M:SomeClass.Main(System.String[])">**  
 **\< 摘要>**  
 **应用程序入口点。**  
 **\< / 摘要>**  
 **\< 参数名称 ="args"> 命令行参数的列表 \< / 参数>**  
 **\< / 成员>**  
 **\< 成员 name="P:SomeClass.Name">**  
 **\< 摘要>**  
 **Name 属性 \< / 摘要>**  
 **\< 值>**  
 **值标记用来描述的属性值 \< / 值>**  
 **\< / 成员>**  
 **\< / 成员>**  
**\< / doc>**   
## <a name="compiling-the-code"></a>编译代码  
 若要编译该示例，请键入以下命令行︰  
  
 `csc XMLsample.cs /doc:XMLsample.xml`  
  
 这将创建 XML 文件 XMLsample.xml，您可以查看在您的浏览器或使用 TYPE 命令。  
  
## <a name="robust-programming"></a>可靠编程  
 XML 文档开头 / /。 创建新项目时，向导将为您放入一些起始 / / 行。 这些注释的处理有一些限制︰  
  
-   文档必须是格式正确 XML。 如果 XML 格式不正确，将生成警告，并且文档文件将包含注释，指出遇到错误。  
  
-   开发人员可以随意创建其自己的标记集。 没有一组建议的标记 （请参阅更多参考资料部分）。 建议的标记的一些具有特殊含义︰  
  
    -   \< Param> 标记用来描述的参数。 如果使用，编译器将验证该参数存在并在文档中描述了所有参数。 如果验证失败，编译器会发出警告。  
  
    -    `cref` 属性可以附加到任何标记，以提供对代码元素的引用。 编译器将验证该代码元素存在。 如果验证失败，编译器会发出警告。 编译器考虑所有 `using` 语句时中描述的类型，它查找 `cref` 属性。  
  
    -   \< 摘要> 标记 IntelliSense 将使用 Visual Studio 内以显示有关类型或成员的其他信息。  
  
        > [!NOTE]
        >  XML 文件未提供有关类型和成员的完整信息 （例如，它不包含任何类型信息）。 若要获取有关类型或成员的完整信息，必须与对实际类型或成员的反射一起使用的文档文件。  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [/doc （C# 编译器选项）](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)   
 [XML 文档注释](../../../csharp/programming-guide/xmldoc/xml-documentation-comments.md)