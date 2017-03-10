---
title: "/linkresource (Visual Basic) | Microsoft Docs"
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
  - "/linkres 编译器选项 [Visual Basic]"
  - "/linkresource 编译器选项 [Visual Basic]"
  - "linkres 编译器选项 [Visual Basic]"
  - "-linkres 编译器选项 [Visual Basic]"
  - "linkresource 编译器选项 [Visual Basic]"
  - "-linkresource 编译器选项 [Visual Basic]"
ms.assetid: cf4dcad8-17b7-404c-9184-29358aa05b15
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# /linkresource (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

创建到托管资源的链接。  
  
## 语法  
  
```  
/linkresource:filename[,identifier[,public|private]]  
' -or-  
/linkres:filename[,identifier[,public|private]]  
```  
  
## 参数  
 `filename`  
 必选。  要链接到程序集的资源文件。  如果文件名包含空格，则将该文件名置于引号 \(" "\) 中。  
  
 `identifier`  
 可选。  资源的逻辑名称。  用于加载资源的名称。  默认为文件的名称。  或者，可以指定文件在程序集清单中是公共的还是私有的，如 `/linkres:filename.res,myname.res,public`。  默认情况下，`filename` 在程序集中是公共的。  
  
## 备注  
 `/linkresource` 选项不会将资源文件嵌入到输出文件中，若要这样做，请使用 `/resource` 选项。  
  
 `/linkresource` 选项需要除 `/target:module` 选项之外的 `/target` 选项之一。  
  
 如果 `filename` 是由 [Resgen.exe（资源文件生成器）](../Topic/Resgen.exe%20\(Resource%20File%20Generator\).md)（举例）或在开发环境中创建的 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 资源文件，则可以通过 <xref:System.Resources> 命名空间中的成员访问它。  （有关更多信息，请参见<xref:System.Resources.ResourceManager>。）若要在运行时访问其他所有资源，请使用 <xref:System.Reflection.Assembly> 类中以 `GetManifestResource` 开头的方法。  
  
 文件名可以是任何文件格式。  例如，您可能想将本机 DLL 设置为程序集的一部分，以便可将其安装到全局程序集缓存中，并且可从程序集中的托管代码访问它。  
  
 `/linkresource` 的缩写形式是 `/linkres`。  
  
> [!NOTE]
>  `/linkresource` 选项不能在 Visual Studio 开发环境中使用；它仅在从命令行进行编译时可用。  
  
## 示例  
 下面的代码编译 `In.vb` 并链接到资源文件 `Rf.resource`。  
  
```  
vbc /linkresource:rf.resource in.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [\/resource](../../../visual-basic/reference/command-line-compiler/resource.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)