---
title: "/link (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/l compiler option [C#]"
  - "/link compiler option [C#]"
  - "-l compiler option [C#]"
  - "EmbedInteropTypes"
  - "l compiler option [C#]"
  - "embed interop types [COM Interop]"
  - "-link compiler option [C#]"
  - "link compiler option [C#]"
ms.assetid: 00da70c6-9ea1-43c2-86f2-aa7f26c03475
caps.latest.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# /link (C# Compiler Options)
使编译器将指定程序集中的 COM 类型信息提供给当前正在编译的项目使用。  
  
## 语法  
  
```  
/link:fileList  
// -or-  
/l:fileList  
```  
  
## 参数  
 `fileList`  
 必选。  程序集文件名的逗号分隔列表。  如果文件名包含空格，则将该文件名置于引号中。  
  
## 备注  
 通过 `/link` 选项，可以部署包含嵌入类型信息的应用程序。  这样，该应用程序无需引用运行时程序集，就可以使用运行时程序集中实现嵌入类型信息的类型。  如果发布了各种版本的运行时程序集，则包含嵌入类型信息的应用程序可以使用各种版本，而不必重新编译。  有关示例，请参见[演练：嵌入托管程序集中的类型](../Topic/Walkthrough:%20Embedding%20Types%20from%20Managed%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 当使用 COM 互操作时，使用 `/link` 选项尤为有用。  通过嵌入 COM 类型，您的应用程序不再要求目标计算机上存在主互操作程序集 \(PIA\)。  `/link` 选项指示编译器将所引用的互操作程序集中的 COM 类型信息嵌入到所生成的编译代码中。  该 COM 类型由 CLSID \(GUID\) 值标识。  因此，您的应用程序可以在安装有 CLSID 值相同的相同 COM 类型的目标计算机上运行。  自动执行 Microsoft Office 的应用程序就是一个很好的示例。  由于诸如 Office 之类的应用程序通常在不同的版本中保留相同的 CLSID 值，因此只要目标计算机上安装有 .NET Framework 4 或更高版本，的应用程序就可以使用所引用的 COM 类型，并使用包含在所引用 COM 类型中的方法、属性或事件。  
  
 `/link` 选项仅嵌入接口、结构和委托。  不支持嵌入 COM 类。  
  
> [!NOTE]
>  当在代码中创建嵌入 COM 类型的实例时，必须使用适当的接口创建该实例。  如果尝试使用 CoClass 创建嵌入 COM 类型的实例，则会导致错误。  
  
 若要在 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 中设置 `/link` 选项，请添加程序集引用并将 `Embed Interop Types` 属性设置为 **true**。  `Embed Interop Types` 属性的默认值为 **false**。  
  
 如果链接至一个 COM 程序集（程序集 A），而其本身又引用另一个 COM 程序集（程序集 B），则在符合下列任一条件的情况下也必须链接至程序集 B：  
  
-   程序集 A 中的类型继承自程序集 B 中的类型或实现程序集 B 中的接口。  
  
-   调用具有程序集 B 中的返回类型或参数类型的字段、属性、事件或方法。  
  
 与 [\/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md) 编译器选项类似，`/link` 编译器选项使用 Csc.rsp 响应文件，该文件引用经常用到的 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 程序集。  如果希望编译器不要使用 Csc.rsp 文件，请使用 [\/noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md) 编译器选项。  
  
 `/link` 的缩写形式是 `/l`。  
  
## 泛型和嵌入类型  
 以下各节介绍在嵌入互操作类型的应用程序中使用泛型类型时所存在的限制。  
  
### 泛型接口  
 不能使用从互操作程序集中嵌入的泛型接口。  这将在下面的示例中显示。  
  
 [!code-cs[VbLinkCompilerCS#1](../../../csharp/language-reference/compiler-options/codesnippet/csharp/vblinkcompilercs/program.cs#1)]  
  
### 具有泛型参数的类型  
 对于具有泛型参数并且该参数类型是从互操作程序集嵌入的类型，如果该类型来自外部程序集，则不能使用该类型。  此限制不适用于接口。  例如，请考虑在 <xref:Microsoft.Office.Interop.Excel> 程序集中定义的 <xref:Microsoft.Office.Interop.Excel.Range> 接口。  如果库从 <xref:Microsoft.Office.Interop.Excel> 程序集嵌入互操作类型并公开一个返回泛型类型的方法，该泛型类型的参数类型为 <xref:Microsoft.Office.Interop.Excel.Range> 接口，则该方法必须返回一个泛型接口，如下面的代码示例中所示。  
  
 [!code-cs[VbLinkCompilerCS#2](../../../csharp/language-reference/compiler-options/codesnippet/csharp/vblinkcompilercs/utility.cs#2)]  
[!code-cs[VbLinkCompilerCS#3](../../../csharp/language-reference/compiler-options/codesnippet/csharp/vblinkcompilercs/utility.cs#3)]  
[!code-cs[VbLinkCompilerCS#4](../../../csharp/language-reference/compiler-options/codesnippet/csharp/vblinkcompilercs/utility.cs#4)]  
  
 在下面的示例中，客户端代码可调用在不出错的情况下返回 <xref:System.Collections.IList> 泛型接口的方法。  
  
 [!code-cs[VbLinkCompilerCS#5](../../../csharp/language-reference/compiler-options/codesnippet/csharp/vblinkcompilercs/program.cs#5)]  
  
## 示例  
 下面的代码编译源文件 `OfficeApp.cs` 并引用 `COMData1.dll` 和 `COMData2.dll` 中的程序集来生成 `OfficeApp.exe`。  
  
```c#  
csc /link:COMData1.dll,COMData2.dll /out:OfficeApp.exe OfficeApp.cs  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [演练：嵌入托管程序集中的类型](../Topic/Walkthrough:%20Embedding%20Types%20from%20Managed%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)   
 [\/reference \(Import Metadata\)](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)   
 [\/noconfig \(Ignore csc.rsp\)](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md)   
 [Command\-line Building With csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)   
 [互操作性概述](../../../csharp/programming-guide/interop/interoperability-overview.md)