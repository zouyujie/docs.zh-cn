---
title: "/target (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/target 编译器选项 [Visual Basic]"
  - "target 编译器选项 [Visual Basic]"
  - "-target 编译器选项 [Visual Basic]"
ms.assetid: e0954147-548b-461f-9c4b-a8f88845616c
caps.latest.revision: 29
caps.handback.revision: 29
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /target (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

指定编译器输出的格式。  
  
## 语法  
  
```  
/target:{exe | library | module | winexe | appcontainerexe | winmdobj}  
```  
  
## 备注  
 下表总结了 `/target` 选项的影响。  
  
|**选项**|**行为**|  
|------------|------------|  
|`/target:exe`|使编译器创建可执行的控制台应用程序。<br /><br /> 如果不指定 `/target` 选项，则它为默认选项。  创建带有 .exe 扩展名的可执行文件。<br /><br /> 除非使用 `/out` 选项另行指定，否则，输出文件的名称将采用包含 `Sub Main` 过程的输入文件的名称。<br /><br /> 在要编译为 .exe 文件的源代码文件中只需要一个 `Sub Main` 过程。  使用 `/main` 编译器选项可指定哪个类包含 `Sub Main` 过程。|  
|`/target:library`|使编译器创建动态链接库 \(DLL\)。<br /><br /> 所创建的动态链接库文件具有 .dll 扩展名。<br /><br /> 除非用 `/out` 选项另外指定，否则输出文件的名称将采用第一个输入文件的名称。<br /><br /> 生成 DLL 时，不需要 `Sub Main` 过程。|  
|`/target:module`|使编译器生成一个可以添加到程序集中的模块。<br /><br /> 所创建的输出文件具有  扩展名。  netmodule。<br /><br /> .NET 公共语言运行时无法加载没有程序集的文件。  但是，可以通过使用 `/reference` 将这样的文件合并到程序集的程序集清单中。<br /><br /> 如果一个模块中的代码引用了另一个模块中的内部类型，则必须使用 `/reference` 将两个模块合并到一个程序集清单中。<br /><br /> [\/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md) 选项导入模块中的元数据。|  
|`/target:winexe`|使编译器创建一个基于 Windows 的可执行应用程序。<br /><br /> 创建带有 .exe 扩展名的可执行文件。  基于 Windows 的应用程序是一种通过 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 类库或使用 Win32 API 提供用户界面的程序。<br /><br /> 除非使用 `/out` 选项另行指定，否则，输出文件的名称将采用包含 `Sub Main` 过程的输入文件的名称。<br /><br /> 在要编译为 .exe 文件的源代码文件中只需要一个 `Sub Main` 过程。  如果代码中有多个包含 `Sub Main` 过程的类，则可以使用 `/main` 编译器选项指定包含 `Sub Main` 过程的类。|  
|`/target:appcontainerexe`|导致编译器创建在应用容器必须运行的可执行基于 windows 的应用程序。  此设置会用于 [!INCLUDE[win8_appname_long](../../../csharp/language-reference/compiler-options/includes/win8_appname_long_md.md)] 应用程序。<br /><br /> **appcontainerexe** 将的属性设置 [可移植可执行文件](http://go.microsoft.com/fwlink/p/?LinkId=236960) 为个文件字段。  此位指示在应用容器必须运行应用程序。  当该位为设置时，将会出错，如果 `CreateProcess` 方法尝试启动应用程序在应用容器外部。  除了设置此的位外，**\/target:appcontainerexe** 与 **\/target:winexe**等效。<br /><br /> 创建带有 .exe 扩展名的可执行文件。<br /><br /> 使用 `/out` 选项，除非另外指定，输出文件名采用包含 `Sub Main` 程序输入文件的名称。<br /><br /> 在要编译为 .exe 文件的源代码文件中只需要一个 `Sub Main` 过程。  如果代码包含多个具有一个 `Sub Main` 程序的一选件类，请使用 `/main` 编译器选项指定要选件类包含 `Sub Main` 程序|  
|`/target:winmdobj`|导致编译器创建可转换为 Windows 运行时二进制文件的一个中间文件\(.winmd\)文件。  除托管语言过程之外，.winmd 文件可以由 JavaScript 和 C\+\+程序使用。<br /><br /> 中间文件的.winmdobj 扩展创建。<br /><br /> 使用 `/out` 选项，除非另外指定，输出文件名采用第一个输入文件的名称。  不需要 `Sub Main` 程序。<br /><br /> .winmdobj 文件旨在用作输入以 <xref:Microsoft.Build.Tasks.WinMDExp> 导出工具会导致 Windows 元数据\(WinMD\)文件。  WinMD 文件的.winmd 扩展并包含从原始库的代码和 JavaScript、C\+\+和 Windows 运行时使用的 WinMD 定义。|  
  
 如果不指定 `/target:module`，`/target` 会将 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 程序集清单添加到输出文件中。  
  
 每个 Vbc.exe 实例最多产生一个输出文件。  如果多次指定编译器选项（如 `/out` 或 `/target`），则编译器处理的最后一个选项将生效。  编译过程中所有文件的相关信息都添加到清单中。  除了使用 `/target:module` 创建的输出文件以外，其他所有输出文件都会包含清单中的程序集元数据。  使用 [Ildasm.exe（IL 反汇编程序）](../Topic/Ildasm.exe%20\(IL%20Disassembler\).md) 可查看输出文件中的元数据。  
  
 `/target` 的缩写形式是 `/t`。  
  
### 在 Visual Studio IDE 中设置 \/target  
  
1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。  
  
2.  单击**“应用程序”**选项卡。  
  
3.  修改**“应用程序类型”**框中的值。  
  
## 示例  
 下面的代码编译 `in.vb`，从而创建 `in.dll`：  
  
```  
vbc /target:library in.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/main](../../../visual-basic/reference/command-line-compiler/main.md)   
 [\/out](../../../visual-basic/reference/command-line-compiler/out.md)   
 [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md)   
 [\/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)   
 [\/moduleassemblyname](../../../visual-basic/reference/command-line-compiler/moduleassemblyname.md)   
 [程序集和全局程序集缓存](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)