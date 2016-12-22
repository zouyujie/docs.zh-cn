---
title: "按字母顺序列出的 Visual Basic 编译器选项 | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "Visual Basic 编译器, 选项"
ms.assetid: e67febba-bacf-4e1f-a143-c141e063f90e
caps.latest.revision: 27
caps.handback.revision: 27
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 按字母顺序列出的 Visual Basic 编译器选项
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 命令行编译器用作一种编译来自 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 集成开发环境 \(IDE\) 的程序的替代方法。  以下是按字母顺序排序的 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 命令行编译器选项的列表。  
  
|选项|目标|  
|--------|--------|  
|[@（指定响应文件）](../../../visual-basic/reference/command-line-compiler/specify-response-file.md)|指定响应文件。|  
|[\/?](../../../visual-basic/reference/command-line-compiler/help.md)|显示编译器选项。  此命令等同于指定 `/help` 选项。  不进行编译。|  
|`/additionalfile`|命名其他文件，这些文件不会直接影响代码生成，但可能被分析器用于生成错误或警告。|  
|[\/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)|使编译器让指定文件中的所有类型信息可供当前正在编译的项目使用。|  
|`/analyzer`|从此程序集（缩写形式：\/a）运行分析器|  
|[\/baseaddress](../../../visual-basic/reference/command-line-compiler/baseaddress.md)|指定 DLL 的基址。|  
|[\/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)|创建一个文件，其中包含可以轻松报告 bug 的信息。|  
|`/checksumalgorithm:<alg>`|指定用于计算 PDB 中存储的源文件校验和的算法。  支持的值为：SHA1（默认值）或 SHA256。|  
|[\/codepage](../../../visual-basic/reference/command-line-compiler/codepage.md)|指定要用于编译中所有源代码文件的代码页。|  
|[\/debug](../../../visual-basic/reference/command-line-compiler/debug.md)|生成调试信息。|  
|[\/define](../../../visual-basic/reference/command-line-compiler/define.md)|定义条件编译的符号。|  
|[\/delaysign](../../../visual-basic/reference/command-line-compiler/delaysign.md)|指定程序集是完全签名的还是部分签名的。|  
|[\/doc](../../../visual-basic/reference/command-line-compiler/doc.md)|将文档注释处理到一个 XML 文件中。|  
|[\/errorreport](../../../visual-basic/reference/command-line-compiler/errorreport.md)|指定 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器报告内部编译器错误的方式。|  
|[\/filealign](../../../visual-basic/reference/command-line-compiler/filealign.md)|指定输出文件各节的对齐位置。|  
|[\/help](../../../visual-basic/reference/command-line-compiler/help.md)|显示编译器选项。  此命令等同于指定 `/?` 选项。  不进行编译。|  
|[\/highentropyva](../../../visual-basic/reference/command-line-compiler/highentropyva.md)|指示特定的可执行文件是否支持高熵地址空间布局随机化 \(ASLR\)。|  
|[\/imports](../../../visual-basic/reference/command-line-compiler/imports.md)|从指定的程序集导入命名空间。|  
|[\/keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md)|指定密钥对的密钥容器名称从而为程序集赋予强名称。|  
|[\/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md)|指定包含密钥或密钥对的文件从而为程序集赋予强名称。|  
|[\/langversion](../../../visual-basic/reference/command-line-compiler/langversion.md)|指定语言版本：9&#124;9.0&#124;10&#124;10.0&#124;11&#124;11.0。|  
|[\/libpath](../../../visual-basic/reference/command-line-compiler/libpath.md)|指定通过 [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md) 选项引用的程序集的位置。|  
|[\/linkresource](../../../visual-basic/reference/command-line-compiler/linkresource.md)|创建指向托管资源的链接。|  
|[\/main](../../../visual-basic/reference/command-line-compiler/main.md)|指定包含启动时要使用的 `Sub``Main` 过程的类。|  
|[\/moduleassemblyname](../../../visual-basic/reference/command-line-compiler/moduleassemblyname.md)|指定模块所属程序集的名称。|  
|`/modulename:<string>`|指定源模块的名称|  
|[\/netcf](../../../visual-basic/reference/command-line-compiler/netcf.md)|设置面向 [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)] 的编译器。|  
|[\/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)|禁止使用 Vbc.rsp 进行编译。|  
|[\/nologo](../../../visual-basic/reference/command-line-compiler/nologo.md)|禁止显示编译器横幅信息。|  
|[\/nostdlib](../../../visual-basic/reference/command-line-compiler/nostdlib.md)|禁止编译器引用标准库。|  
|[\/nowarn](../../../visual-basic/reference/command-line-compiler/nowarn.md)|禁止编译器生成警告。|  
|[\/nowin32manifest](../../../visual-basic/reference/command-line-compiler/nowin32manifest.md)|指示编译器不在可执行文件中嵌入任何应用程序清单。|  
|[\/optimize](../../../visual-basic/reference/command-line-compiler/optimize.md)|启用\/禁用代码优化。|  
|[\/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)|指定字符串比较是否应为二进制，或是否应使用特定于区域设置的文本语义。|  
|[\/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)|强制执行变量显式声明。|  
|[\/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)|允许在变量声明中使用局部类型推理。|  
|[\/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)|强制执行严格的语言语义。|  
|[\/out](../../../visual-basic/reference/command-line-compiler/out.md)|指定输出目录。|  
|`/parallel[+&#124;-]`|指定是否使用并发生成 \(\+\)。|  
|[\/platform](../../../visual-basic/reference/command-line-compiler/platform.md)|为输出文件指定编译器面向的处理器平台。|  
|`/preferreduilang`|指定首选输出语言名称。|  
|[\/quiet](../../../visual-basic/reference/command-line-compiler/quiet.md)|阻止编译器显示与语法相关的错误和警告代码。|  
|[\/recurse](../../../visual-basic/reference/command-line-compiler/recurse.md)|搜索要编译的源文件的子目录。|  
|[\/reference](../../../visual-basic/reference/command-line-compiler/reference.md)|从程序集导入元数据。|  
|[\/removeintchecks](../../../visual-basic/reference/command-line-compiler/removeintchecks.md)|禁用整数溢出检查。|  
|[\/resource](../../../visual-basic/reference/command-line-compiler/resource.md)|将托管资源嵌入程序集。|  
|[\/rootnamespace](../../../visual-basic/reference/command-line-compiler/rootnamespace.md)|指定所有类型声明的命名空间。|  
|`/ruleset:<file>`|指定可禁用特定诊断的规则集文件。|  
|[\/sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)|指定 Mscorlib.dll 和 Microsoft.VisualBasic.dll 的位置。|  
|[\/subsystemversion](../../../visual-basic/reference/command-line-compiler/subsystemversion.md)|指定生成的可执行文件可以使用的子系统的最低版本。|  
|[\/target](../../../visual-basic/reference/command-line-compiler/target.md)|指定输出文件的格式。|  
|[\/utf8output](../../../visual-basic/reference/command-line-compiler/utf8output.md)|显示使用 UTF\-8 编码的编译器输出。|  
|[\/vbruntime](../../../visual-basic/reference/command-line-compiler/vbruntime.md)|指定编译器应在不引用 Visual Basic 运行库的情况下进行编译，或在引用特定运行库的情况下进行编译。|  
|[\/verbose](../../../visual-basic/reference/command-line-compiler/verbose.md)|在编译期间输出其他信息。|  
|[\/warnaserror](../../../visual-basic/reference/command-line-compiler/warnaserror.md)|将警告提升为错误。|  
|[\/win32icon](../../../visual-basic/reference/command-line-compiler/win32icon.md)|将 .ico 文件插入到输出文件。|  
|[\/win32manifest](../../../visual-basic/reference/command-line-compiler/win32manifest.md)|标识要嵌入到项目可移植可执行 \(PE\) 文件的用户定义的 Win32 应用程序清单文件。|  
|[\/win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md)|将 Win32 资源插入到输出文件。|  
  
## 请参阅  
 [按类别列出的 Visual Basic 编译器选项](../../../visual-basic/reference/command-line-compiler/compiler-options-listed-by-category.md)   
 [Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)   
 [C\# Compiler Options Listed Alphabetically](../../../csharp/language-reference/compiler-options/listed-alphabetically.md)   
 [C\# Compiler Options Listed by Category](../../../csharp/language-reference/compiler-options/listed-by-category.md)