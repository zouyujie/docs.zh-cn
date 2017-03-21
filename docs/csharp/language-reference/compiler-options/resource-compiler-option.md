---
title: "/resource (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/resource"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-resource compiler option [C#]"
  - "/resource compiler option [C#]"
  - "-res compiler option [C#]"
  - "/res compiler option [C#]"
  - "res compiler option [C#]"
  - "resource compiler option [C#]"
ms.assetid: 5212666e-98ab-47e4-a497-b5545ab15c7f
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# /resource (C# Compiler Options)
将指定的资源嵌入到输出文件中。  
  
## 语法  
  
```  
/resource:filename[,identifier[,accessibility-modifier]]  
```  
  
## 参数  
 `filename`  
 要在输出文件中嵌入的 .NET Framework 资源文件。  
  
 `identifier`（可选）  
 资源的逻辑名称；用于加载资源的名称。  默认为文件的名称。  
  
 `accessibility-modifier`（可选）  
 资源的可访问性：公共或私有。  默认为公共。  
  
## 备注  
 使用 [\/linkresource](../../../csharp/language-reference/compiler-options/linkresource-compiler-option.md) 将资源链接到程序集，但不将资源文件添加到输出文件中。  
  
 默认情况下，如果资源是用 C\# 编译器创建的，则该资源在程序集中就是公共的。  若要使这些资源成为私有的，请将 `private` 指定为可访问性修饰符。  不允许使用 `public` 或 `private` 以外的可访问性。  
  
 如果 `filename` 是由例如 [Resgen.exe](../Topic/Resgen.exe%20\(Resource%20File%20Generator\).md) 创建或在开发环境中创建的 .NET Framework 资源文件，则可以通过 <xref:System.Resources> 命名空间中的成员访问该文件。  有关更多信息，请参见 <xref:System.Resources.ResourceManager?displayProperty=fullName>。  对于所有其他资源，请使用 <xref:System.Reflection.Assembly> 类中的 `GetManifestResource`\* 方法在运行时访问资源。  
  
 **\/res** 是 **\/resource** 的缩写形式。  
  
 资源在输出文件中的顺序是由命令行上指定的顺序决定的。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  将资源文件添加到项目中。  
  
2.  在**“解决方案资源管理器”**中，选择要嵌入的文件。  
  
3.  在**“属性”**窗口中，为该文件选择**“生成操作”**。  
  
4.  将**“生成操作”**设置为**“嵌入的资源”**。  
  
 有关如何以编程方式设置此编译器选项的信息，请参见 <xref:VSLangProj80.FileProperties2.BuildAction%2A>。  
  
## 示例  
 编译 `in.cs` 并附加资源文件 `rf.resource`：  
  
```  
csc /resource:rf.resource in.cs  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)