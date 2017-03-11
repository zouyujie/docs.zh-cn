---
title: "/keycontainer | Microsoft Docs"
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
  - "/keycontainer 编译器选项 [Visual Basic]"
  - "keycontainer 编译器选项 [Visual Basic]"
  - "-keycontainer 编译器选项 [Visual Basic]"
ms.assetid: 6a9bc861-1752-4db1-9f64-b5252f0482cc
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# /keycontainer
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定密钥对的密钥容器名称以给予程序集强名称。  
  
## 语法  
  
```  
/keycontainer:container  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`container`|必选。  包含密钥的容器文件。  如果文件名包含空格，则将该文件名置于引号 \(" "\) 中。|  
  
## 备注  
 通过将一个公钥插入到程序集清单并用私钥对最终的程序集签名，编译器可以创建可共享的组件。  若要生成密钥文件，请在命令行上键入 `sn -k` `file`。  `-i`  选项将密钥对安装到容器中。  有关更多信息，请参见 [Sn.exe（强名称工具）](../Topic/Sn.exe%20\(Strong%20Name%20Tool\).md)。  
  
 如果使用 `/target:module` 进行编译，则将密钥文件的名称保存在模块中，并将其合并到使用 [\/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md) 编译程序集时创建的程序集中。  
  
 还可以将此选项指定为任何 Microsoft 中间语言 \(MSIL\) 模块的源代码中的自定义特性 \(<xref:System.Reflection.AssemblyKeyNameAttribute>\)。  
  
 也可以通过 [\/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md) 将加密信息传递给编译器。  如果需要部分签名的程序集，则使用 [\/delaysign](../../../visual-basic/reference/command-line-compiler/delaysign.md)。  
  
 有关对程序集进行签名的更多信息，请参见 [创建和使用具有强名称的程序集](../Topic/Creating%20and%20Using%20Strong-Named%20Assemblies.md)。  
  
> [!NOTE]
>  `/keycontainer` 选项不能在 Visual Studio 开发环境内部使用，它仅在从命令行进行编译时可用。  
  
## 示例  
 下面的代码编译源文件 `Input.vb` 并指定密钥容器。  
  
```  
vbc /keycontainer:key1 input.vb  
```  
  
## 请参阅  
 [程序集和全局程序集缓存](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)   
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)