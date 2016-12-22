---
title: "/linkresource (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/linkresource"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/linkresource compiler option [C#]"
  - "linkres compiler option [C#]"
  - "/linkres compiler option [C#]"
  - "-linkres compiler option [C#]"
  - "-linkresource compiler option [C#]"
  - "linkresource compiler option [C#]"
ms.assetid: 440c26c2-77c1-4811-a0a3-57cce3f5fc96
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /linkresource (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

在输出文件中创建指向 .NET Framework 资源的链接。  该资源文件未添加到输出文件中。  这与 [\/resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md) 选项不同，后者会将资源文件嵌入到输出文件中。  
  
## 语法  
  
```  
/linkresource:filename[,identifier[,accessibility-modifier]]  
```  
  
## 参数  
 `filename`  
 要从程序集链接的 .NET Framework 资源文件。  
  
 `identifier`（可选）  
 资源的逻辑名称；用于加载资源的名称。  默认为文件的名称。  
  
 `accessibility-modifier`（可选）  
 资源的可访问性：公共或私有。  默认为公共。  
  
## 备注  
 默认情况下，如果链接的资源是用 C\# 编译器创建的，则链接资源在程序集中就是公共的。  若要使这些资源成为私有的，请将 `private` 指定为可访问性修饰符。  不允许使用 `public` 或 `private` 以外的其他修饰符。  
  
 **\/linkresource** 需要除 **\/target:module** 选项之外的 [\/target](../../../csharp/language-reference/compiler-options/target-compiler-option.md) 选项之一。  
  
 如果 `filename` 是由例如 [Resgen.exe](../Topic/Resgen.exe%20\(Resource%20File%20Generator\).md) 创建或在开发环境中创建的 .NET Framework 资源文件，则可以通过 <xref:System.Resources> 命名空间中的成员访问该文件。  有关更多信息，请参见 <xref:System.Resources.ResourceManager?displayProperty=fullName>。  对于所有其他资源，请使用 <xref:System.Reflection.Assembly> 类中的 `GetManifestResource`\* 方法在运行时访问资源。  
  
 在 `filename` 中指定的文件可以为任何格式。  例如，您可能想将本机 DLL 设置为程序集的一部分，以便可将其安装到全局程序集缓存中，并且可从程序集中的托管代码访问它。  下面的第二个示例演示如何执行此操作。  您可以在程序集链接器中执行相同的操作。  下面的第三个示例演示如何执行此操作。  有关更多信息，请参见[Al.exe（程序集链接器）](../Topic/Al.exe%20\(Assembly%20Linker\).md)和 [使用程序集和全局程序集缓存](../Topic/Working%20with%20Assemblies%20and%20the%20Global%20Assembly%20Cache.md)。  
  
 **\/linkres** 是 **\/linkresource** 的缩写形式。  
  
 此编译器选项在 Visual Studio 中不可用，且不能通过编程方式进行更改。  
  
## 示例  
 编译 `in.cs` 并链接到资源文件 `rf.resource`：  
  
```  
csc /linkresource:rf.resource in.cs  
```  
  
## 示例  
 将 `A.cs` 编译为 DLL，链接到本机 DLL N.dll，并将输出放置在全局程序集缓存 \(GAC\) 中。  在此示例中，A.dll 和 N.dll 都驻留在 GAC 中。  
  
```  
csc /linkresource:N.dll /t:library A.cs  
gacutil -i A.dll  
```  
  
## 示例  
 此示例和前一个示例执行的是同样的操作，但使用的是程序集链接器选项。  
  
```  
csc /t:module A.cs  
al /out:A.dll A.netmodule /link:N.dll   
gacutil -i A.dll  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Al.exe（程序集链接器）](../Topic/Al.exe%20\(Assembly%20Linker\).md)   
 [使用程序集和全局程序集缓存](../Topic/Working%20with%20Assemblies%20and%20the%20Global%20Assembly%20Cache.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)