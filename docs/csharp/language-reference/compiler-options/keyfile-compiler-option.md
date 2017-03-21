---
title: "/keyfile (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/keyfile"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/keyfile compiler option [C#]"
  - "-keyfile compiler option [C#]"
  - "keyfile compiler option [C#]"
ms.assetid: 0815f9de-ace4-4e98-b4c6-13c55dea40c2
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# /keyfile (C# Compiler Options)
指定包含加密密钥的文件名。  
  
## 语法  
  
```  
/keyfile:file  
```  
  
## 参数  
  
|术语|定义|  
|--------|--------|  
|`file`|包含强名称密钥的文件的名称。|  
  
## 备注  
 使用此选项时，编译器将从指定的文件将公钥插入程序集清单中，然后使用私钥对最终程序集进行签名。  若要生成密钥文件，请在命令行上键入 sn \-k `file`。  
  
 如果使用 **\/target:module** 进行编译，则将密钥文件的名称保存在模块中，并在使用 [\/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md) 编译程序集时将其包含到创建的程序集中。  
  
 也可以使用 [\/keycontainer](../../../csharp/language-reference/compiler-options/keycontainer-compiler-option.md) 将加密信息传递给编译器。  如果需要部分签名的程序集，则使用 [\/delaysign](../../../csharp/language-reference/compiler-options/delaysign-compiler-option.md)。  
  
 如果在相同的编译中指定了 \/keyfile 和 \/keycontainer（通过命令行选项或自定义特性），编译器将首先尝试密钥容器。  如果成功，则使用密钥容器中的信息对程序集进行签名。  如果编译器没有找到密钥容器，则将尝试用 \/keyfile 指定的文件。  如果成功，则使用密钥文件中的信息对程序集进行签名，并且将把密钥信息安装到密钥容器中（类似 sn \-i），这样，下次编译时密钥容器将是有效的。  
  
 请注意，密钥文件可能只包含公钥。  
  
 有关更多信息，请参见[创建和使用具有强名称的程序集](../Topic/Creating%20and%20Using%20Strong-Named%20Assemblies.md)和[延迟为程序集签名](../Topic/Delay%20Signing%20an%20Assembly.md)。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“签名”**属性页。  
  
3.  修改**“选择强名称密钥文件”**属性。  
  
 可以使用 <xref:VSLangProj.ProjectProperties.AssemblyOriginatorKeyFile%2A> 以编程方式访问此编译器选项。  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)