---
title: "/delaysign | Microsoft Docs"
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
  - "/delaysign 编译器选项 [Visual Basic]"
  - "delaysign 编译器选项 [Visual Basic]"
  - "-delaysign 编译器选项 [Visual Basic]"
ms.assetid: c76e61a4-1884-4252-9fb2-377f99caa690
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# /delaysign
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定程序集是完全签名的还是部分签名的。  
  
## 语法  
  
```  
/delaysign[+ | -]  
```  
  
## 参数  
 `+` &#124; `-`  
 可选。  如果需要完全签名的程序集，则使用 `/delaysign-`。  如果要将公钥放在程序集中，并为签名的散列保留空间，请使用 `/delaysign+`。  默认值为 `/delaysign-`。  
  
## 备注  
 如果不与 [\/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md) 或 [\/keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md) 一起使用，`/delaysign` 选项将无效。  
  
 如果要求完全签名的程序集，编译器将对包含清单（程序集元数据）的文件进行散列处理，并用私钥对该散列数据进行签名。  产生的数字签名存储在包含清单的文件中。  当某个程序集的签名延迟时，编译器将不会计算和存储签名，但会在文件中保留空间以便以后添加签名。  
  
 例如，通过使用 `/delaysign+`，组织中的开发人员可以分发未签名的程序集测试版本，测试人员将能够向全局程序集缓存注册这些版本，并使用它们。  当针对程序集的处理完成后，负责组织的私钥的人员可对程序集进行完全签名。  这种划分可防止组织的私钥泄露，同时允许所有开发人员对程序集进行处理。  
  
 有关对程序集进行签名的更多信息，请参见 [创建和使用具有强名称的程序集](../Topic/Creating%20and%20Using%20Strong-Named%20Assemblies.md)。  
  
### 在 Visual Studio 集成开发环境中设置 \/delaysign  
  
1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。  
  
2.  单击**“签名”**选项卡。  
  
3.  设置**“仅延迟签名”**框中的值。  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md)   
 [\/keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)