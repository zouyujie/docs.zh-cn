---
title: "/baseaddress (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/dllbase"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "baseaddress compiler option [C#]"
  - "/baseaddress compiler option [C#]"
  - "-baseaddress compiler option [C#]"
ms.assetid: ce13c965-dfe4-4433-94f5-63b476e3a608
caps.latest.revision: 18
caps.handback.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /baseaddress (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

**\/baseaddress** 选项使您可以指定加载 DLL 的首选基址。  有关为何和何时使用此选项的更多信息，请参见 [提高应用开始时间](http://go.microsoft.com/fwlink/?LinkId=107043) 和 [拉里 Osterman 的网络日志](http://go.microsoft.com/fwlink/?LinkId=107044)。  
  
## 语法  
  
```  
/baseaddress:address  
```  
  
## 参数  
 `address`  
 DLL 的基址。  可以将该地址指定为十进制、十六进制或八进制数。  
  
## 备注  
 DLL 的默认基址由 .NET Framework 公共语言运行时设置。  
  
 请注意：该地址中低位的数将会被舍入。  例如，如果指定 0x11110001，它将被舍入为 0x11110000。  
  
 若要完成 DLL 的签名过程，请结合使用 SN.EXE 和 \-R 选项。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“生成”**属性页。  
  
3.  单击“高级”按钮。  
  
4.  修改**“DLL 基址”**属性。  
  
     若要以编程方式设置此编译器选项，请参见 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.BaseAddress%2A>。  
  
## 请参阅  
 <xref:System.Diagnostics.ProcessModule.BaseAddress%2A?displayProperty=fullName>   
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)