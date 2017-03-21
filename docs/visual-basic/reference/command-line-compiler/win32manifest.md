---
title: "/win32manifest (Visual Basic) | Microsoft Docs"
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
  - "/win32manifest 编译器选项 [Visual Basic]"
  - "win32manifest 编译器选项 [Visual Basic]"
  - "-win32manifest 编译器选项 [Visual Basic]"
ms.assetid: 9e3191b4-90db-41c8-966a-28036fd20005
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# /win32manifest (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

标识要嵌入到项目的可移植可执行 \(PE\) 文件中的用户定义的 Win32 应用程序清单文件。  
  
## 语法  
  
```  
/win32manifest: fileName  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`fileName`|自定义清单文件的路径。|  
  
## 备注  
 默认情况下，Visual Basic 编译器嵌入指定“asInvoker”的请求执行级别的应用程序清单。  它在生成该可执行文件的文件夹中创建清单，如果使用 Visual Studio，该文件夹通常为 bin\\Debug 或 bin\\Release。  如果要提供自定义清单（例如，指定“highestAvailable”或“requireAdministrator”的请求执行级别的清单），请使用此选项指定文件名。  
  
> [!NOTE]
>  此选项和 [\/win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md) 选项是互斥的。  如果尝试在同一命令行中同时使用这两个选项，则会产生一个生成错误。  
  
 如果应用程序没有用于指定请求执行级别的应用程序清单，则会受到 Windows Vista 的用户帐户控制功能下的文件\/注册表虚拟化的影响。  有关虚拟化的更多信息，请参见[Windows Vista 上的 ClickOnce 部署](/visual-studio/deployment/clickonce-deployment-on-windows-vista)。  
  
 如果满足以下任一条件，则应用程序受到虚拟化的影响：  
  
1.  使用 `/nowin32manifest` 选项，并且在随后的生成步骤中未提供清单，或者没有通过使用 `/win32resource` 选项将其包含在 Windows 资源 \(.res\) 文件中。  
  
2.  提供的自定义清单未指定请求执行级别。  
  
 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 创建默认的 .manifest 文件，并将该文件与可执行文件一起存储在 debug 和 release 目录中。  在项目设计器的**“应用程序”**选项卡上单击**“查看 UAC 设置”**，可以查看或编辑默认的 app.manifest 文件。有关更多信息，请参见[“项目设计器”, “应用程序”页 \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic)。  
  
 提供应用程序清单的操作，可以作为自定义后期生成步骤，也可以通过使用 `/nowin32manifest` 选项作为 Win32 资源文件的组成部分。  如果希望应用程序受到 Windows Vista 的文件\/注册表虚拟化的影响，请使用该选项。  这样可防止编译器在 PE 文件中创建和嵌入默认清单。  
  
## 示例  
 下面的示例演示 Visual Basic 编译器插入到 PE 中的默认清单。  
  
> [!NOTE]
>  编译器将一个标准应用程序名称 MyApplication.app 插入到清单 XML 中。  这是一种使应用程序可以在 Windows Server 2003 Service Pack 3 上运行的解决方法。  
  
```  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
  <assemblyIdentity version="1.0.0.0" name="MyApplication.app"/>  
  <trustInfo xmlns="urn:schemas-microsoft-com:asm.v2">  
    <security>  
      <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">  
        <requestedExecutionLevel level="asInvoker"/>  
      </requestedPrivileges>  
    </security>  
  </trustInfo>  
</assembly>  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/nowin32manifest](../../../visual-basic/reference/command-line-compiler/nowin32manifest.md)