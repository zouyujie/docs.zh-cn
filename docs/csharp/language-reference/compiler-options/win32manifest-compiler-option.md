---
title: "/win32manifest (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/win32manifest"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/win32manifest compiler option [C#]"
  - "win32manifest compiler option [C#]"
  - "-win32manifest compiler option [C#]"
ms.assetid: 9460ea1b-6c9f-44b8-8f73-301b30a01de1
caps.latest.revision: 13
caps.handback.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /win32manifest (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

使用 **\/win32manifest** 选项可以指定要嵌入到项目的可迁移可执行 \(PE\) 文件中的用户定义的 Win32 应用程序清单文件。  
  
## 语法  
  
```  
/win32manifest: filename  
```  
  
## 参数  
 `filename`  
 自定义清单文件的名称和位置。  
  
## 备注  
 默认情况下，[!INCLUDE[csharp_current_short](../../../csharp/language-reference/compiler-options/includes/csharp_current_short_md.md)] 编译器嵌入指定“asInvoker”的请求执行级别的应用程序清单。它在生成该可执行文件的文件夹中创建清单，如果使用 Visual Studio，该文件夹通常为 bin\\Debug 或 bin\\Release。  如果要提供自定义清单（例如，指定“highestAvailable”或“requireAdministrator”的请求执行级别的清单），请使用此选项指定文件名。  
  
> [!NOTE]
>  此选项和 [\/win32res \(Import a Win32 Resource File\)](../../../csharp/language-reference/compiler-options/win32res-compiler-option.md) 选项是互斥的。  如果尝试在同一命令行中同时使用这两个选项，则会收到一个生成错误。  
  
 如果应用程序没有用于指定请求执行级别的应用程序清单，则会受到 Windows Vista 的用户帐户控制功能下的文件\/注册表虚拟化的影响。  有关虚拟化的更多信息，请参见 [The Windows Vista Developer Story: Windows Vista Application Development Requirements for User Account Control \(UAC\)](http://go.microsoft.com/fwlink/?LinkId=95452)。  
  
 如果满足下列任一条件，则应用程序会受到虚拟化的影响：  
  
-   使用 **\/nowin32manifest** 选项，并且在随后的生成步骤中未提供清单，或者没有通过使用 **\/win32res** 选项将其包含在 Windows 资源 \(.res\) 文件中。  
  
-   提供的自定义清单未指定请求执行级别。  
  
 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 创建默认的 .manifest 文件，并将该文件与可执行文件一起存储在 debug 和 release 目录中。  可以用任意文本编辑器创建一个清单，然后将该文件添加到项目中，以此添加自定义清单。  或者，也可以右击**“解决方案资源管理器”**中的**“项目”**图标，单击**“添加新项”**，然后单击**“应用程序清单文件”**。  添加完新的或现有清单文件后，该文件将显示在**“清单”**下拉列表中。  有关详细信息，请参阅[“项目设计器”\-\>“应用程序”页 \(C\#\)](/visual-studio/ide/reference/application-page-project-designer-csharp)。  
  
 提供应用程序清单的操作，可以作为自定义后期生成步骤，也可以通过使用 [\/nowin32manifest \(No Win32 Manifest\)](../../../csharp/language-reference/compiler-options/nowin32manifest-compiler-option.md) 选项作为 Win32 资源文件的组成部分。  如果希望应用程序受到 Windows Vista 的文件\/注册表虚拟化的影响，请使用该选项。  这会阻止编译器在可迁移可执行 \(PE\) 文件中创建和嵌入默认清单。  
  
## 示例  
 下面的示例演示 Visual C\# 编译器插入到 PE 中的默认清单。  
  
> [!NOTE]
>  编译器将一个标准应用程序名称“MyApplication.app”插入到 xml 中。  这是一种使应用程序可以在 Windows Server 2003 Service Pack 3 上运行的解决方法。  
  
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
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [\/nowin32manifest \(No Win32 Manifest\)](../../../csharp/language-reference/compiler-options/nowin32manifest-compiler-option.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)