---
title: "/baseaddress | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "/baseaddress"
  - "baseaddress"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/baseaddress 编译器选项 [Visual Basic]"
  - "baseaddress 编译器选项 [Visual Basic]"
  - "-baseaddress 编译器选项 [Visual Basic]"
ms.assetid: c982bcf2-46e5-47a2-bc8f-a5cc32b7dc47
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# /baseaddress
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定创建 DLL 时的默认基址。  
  
## 语法  
  
```  
/baseaddress:address  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`address`|必选。  DLL 的基址。  该地址必须指定为十六进制数。|  
  
## 备注  
 DLL 的默认基址由 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 设置。  
  
 请注意，该地址中的低位字将被舍入。  例如，如果指定 0x11110001，将舍入为 0x11110000。  
  
 若要完成 DLL 的签名进程，请使用强命名工具 \(Sn.exe\) 的 `–R` 选项。  
  
 如果目标不是 DLL，则会忽略此选项。  
  
||  
|-|  
|在 Visual Studio IDE 中设置 \/baseaddress|  
|1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.  单击**“编译”**选项卡。<br />3.  单击**“高级”**。<br />4.  修改**“DLL 基址：”**框中的值。 **Note:**      如果目标不是 DLL，则**“DLL 基址：”**框为只读。|  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Sn.exe（强名称工具）](../Topic/Sn.exe%20\(Strong%20Name%20Tool\).md)