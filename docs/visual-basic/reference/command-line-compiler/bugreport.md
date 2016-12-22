---
title: "/bugreport | Microsoft Docs"
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
  - "/bugreport 编译器选项 [Visual Basic]"
  - "bugreport 编译器选项 [Visual Basic]"
  - "-bugreport 编译器选项 [Visual Basic]"
ms.assetid: e4325406-8dbd-4b48-b311-9ee0799e48bb
caps.latest.revision: 22
caps.handback.revision: 22
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /bugreport
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

创建一个可以在归档 bug 报告时使用的文件。  
  
## 语法  
  
```  
/bugreport:file  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`file`|必选。  将包含 bug 报告的文件的名称。  如果文件名包含空格，则将该文件名置于引号 \(" "\) 中。|  
  
## 备注  
 下列信息将添加到 `file` 中：  
  
-   编译中所有源代码文件的副本。  
  
-   编译中使用的编译器选项的列表。  
  
-   编译器、公共语言运行时和操作系统的版本信息。  
  
-   编译器输出（如果有）。  
  
-   对问题（将就此向您发出提示）的说明。  
  
-   对您认为问题应当如何解决（将就此向您发出提示）的说明。  
  
 由于所有源代码文件的副本都包含在 `file` 中，因此可能需要在尽可能短的程序内重现（可疑的）代码缺陷。  
  
> [!IMPORTANT]
>  `/bugreport` 选项会生成一个包含可能是敏感信息的文件。  这些信息包括：当前时间、编译器版本、[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 版本、操作系统版本、用户名、运行编译器所使用的命令行参数、所有源代码以及任何二进制形式的引用程序集。  此选项可以通过在 Web.config 文件中指定用于在服务器端编译 [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] 应用程序的命令行选项来进行访问。  若要防止执行此操作，可修改 Machine.config 文件以禁止用户在服务器上编译。  
  
 如果此选项与 `/errorreport:prompt`、`/errorreport:queue` 或 `/errorreport:send` 一起使用，而应用程序遇到内部编译器错误，则 `file` 中的信息将会被发送给 Microsoft Corporation。  这些信息有助于 Microsoft 工程师识别错误的原因，从而改善下一个版本的 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。  默认情况下，不会向 Microsoft 发送任何信息。  不过，当使用 `/errorreport:queue`（默认情况下已启用）编译应用程序时，此应用程序会收集其错误报告。  然后，在计算机的管理员登录时，错误报告系统会显示一个弹出窗口，使管理员能够将自登录之后发生的任何错误报告转发给 Microsoft。  
  
> [!NOTE]
>  `/bugreport` 选项不能在 Visual Studio 开发环境中使用；它仅在从命令行进行编译时可用。  
  
## 示例  
 下面的示例将编译 `T2.vb`，并将所有 bug 报告信息放入文件 `Problem.txt` 中。  
  
```  
vbc /bugreport:problem.txt t2.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/debug](../../../visual-basic/reference/command-line-compiler/debug.md)   
 [\/errorreport](../../../visual-basic/reference/command-line-compiler/errorreport.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [securityPolicy 的 trustLevel 元素（ASP.NET 设置架构）](http://msdn.microsoft.com/zh-cn/729ab04c-03da-4ee5-86b1-be9d08a09369)