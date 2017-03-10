---
title: "/keycontainer (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/keycontainer"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/keycontainer compiler option [C#]"
  - "keycontainer compiler option [C#]"
  - "-keycontainer compiler option [C#]"
ms.assetid: b3982b6d-2382-4f7e-bebd-ce98eaa30763
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# /keycontainer (C# Compiler Options)
指定加密密钥容器的名称。  
  
## 语法  
  
```  
/keycontainer:string  
```  
  
## 参数  
 `string`  
 强名称密钥容器的名称。  
  
## 备注  
 使用 **\/keycontainer** 选项时，通过将来自所指定容器的公钥插入到程序集清单中并且用私钥签名最终程序集，编译器可创建可共享的组件。  生成密钥文件，请在命令行上键入sn \-k `file`。sn \-i 安装密钥对为容器。  
  
 如果使用 [\/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md) 进行编译，则将密钥文件的名称保存在模块中，并在使用 [\/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md) 编译程序集时将其包含到该程序集中。  
  
 还可以将此选项指定为任何 Microsoft 中间语言 \(MSIL\) 模块的源代码中的自定义特性 \(<xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName>\)。  
  
 也可以通过 [\/keyfile](../../../csharp/language-reference/compiler-options/keyfile-compiler-option.md) 将加密信息传递给编译器。  如果希望将公钥添加到程序集清单中，但将程序集的签名延迟到该程序集通过测试，则请使用 [\/delaysign](../../../csharp/language-reference/compiler-options/delaysign-compiler-option.md)。  
  
 有关更多信息，请参见[创建和使用具有强名称的程序集](../Topic/Creating%20and%20Using%20Strong-Named%20Assemblies.md)和[延迟为程序集签名](../Topic/Delay%20Signing%20an%20Assembly.md)。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  此编译器选项在 Visual Studio 开发环境中不可用。  
  
 可以使用 <xref:VSLangProj.ProjectProperties.AssemblyKeyContainerName%2A> 以编程方式访问此编译器选项。  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)