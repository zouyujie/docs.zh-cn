---
title: "/keyfile | Microsoft Docs"
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
  - "/keyfile 编译器选项 [Visual Basic]"
  - "keyfile 编译器选项 [Visual Basic]"
  - "-keyfile 编译器选项 [Visual Basic]"
ms.assetid: ffa82a4b-517a-4c6c-9889-5bae7b534bb8
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# /keyfile
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定包含密钥或密钥对的文件以给予程序集强名称。  
  
## 语法  
  
```  
/keyfile:file  
```  
  
## 参数  
 `file`  
 必选。  包含密钥的文件。  如果文件名包含空格，则将该文件名置于引号 \(" "\) 中。  
  
## 备注  
 编译器将公钥插到程序集清单中，然后用私钥对最终的程序集进行签名。  若要生成密钥文件，请在命令行上键入 `sn -k file`。  有关更多信息，请参见 [Sn.exe（强名称工具）](../Topic/Sn.exe%20\(Strong%20Name%20Tool\).md)。  
  
 如果使用 `/target:module` 进行编译，则将密钥文件的名称保存在模块中，并将其合并到使用 [\/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md) 编译程序集时创建的程序集中。  
  
 也可以通过 [\/keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md) 将加密信息传递给编译器。  如果需要部分签名的程序集，则使用 [\/delaysign](../../../visual-basic/reference/command-line-compiler/delaysign.md)。  
  
 还可以将此选项指定为任何 Microsoft 中间语言模块的源代码中的自定义特性 \(<xref:System.Reflection.AssemblyKeyFileAttribute>\)。  
  
 如果在同一编译中指定了 `/keyfile` 和 [\/keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md) 两者（通过命令行选项或通过自定义特性），则编译器首先尝试密钥容器。  如果成功，则使用密钥容器中的信息对程序集进行签名。  如果编译器没有找到密钥容器，则将尝试用 `/keyfile` 指定的文件。  如果成功，则使用密钥文件中的信息对程序集进行签名，并且将把密钥信息安装到密钥容器中（类似 `sn -i`），这样，下次编译时密钥容器将会有效。  
  
 请注意，密钥文件可能只包含公钥。  
  
 有关对程序集进行签名的更多信息，请参见 [创建和使用具有强名称的程序集](../Topic/Creating%20and%20Using%20Strong-Named%20Assemblies.md)。  
  
> [!NOTE]
>  `/keyfile` 选项不能在 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 开发环境中使用；它仅在从命令行进行编译时可用。  
  
## 示例  
 下面的代码编译源文件 `Input.vb` 并指定密钥文件。  
  
```  
vbc /keyfile:myfile.sn input.vb  
```  
  
## 请参阅  
 [程序集和全局程序集缓存](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)   
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)