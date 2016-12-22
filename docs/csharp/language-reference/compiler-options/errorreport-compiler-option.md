---
title: "/errorreport (C# Compiler Options) | Microsoft Docs"
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
  - "/errorreport"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-errorreport compiler option [C#]"
  - "errorreport compiler option [C#]"
  - "/errorreport compiler option [C#]"
ms.assetid: bd0e7493-b79d-4369-9c3f-ba26ebdfbedf
caps.latest.revision: 35
caps.handback.revision: 35
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /errorreport (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

使用此选项可以方便地向 Microsoft 报告 C\# 内部编译器错误。  
  
> [!NOTE]
>  在 Windows Vista 和 Windows Server 2008 上，为 Visual Studio 做出的错误报告设置不会替代通过 Windows 错误报告 \(WER\) 做出的设置。  WER 设置始终优先于 Visual Studio 的错误报告设置。  
  
## 语法  
  
```  
/errorreport:{ none | prompt | queue | send }  
```  
  
## 参数  
 **none**  
 不收集有关内部编译器错误的报告，或不向 Microsoft 发送报告。  
  
 **prompt**  
 当您收到内部编译器错误时，提示您发送报告。  在开发环境中编译应用程序时，**prompt** 是默认值。  
  
 **queue**  
 对错误报告进行排队。  当使用管理凭据登录时，可以报告自上次登录以来出现的任何故障。  如果每三天出现一次以上故障，则将不提示发送故障报告。  在命令行编译应用程序时，**queue** 是默认值。  
  
 **send**  
 自动向 Microsoft 发送内部编译器错误报告。  若要启用此选项，必须先同意 Microsoft 数据收集策略。  首次在计算机上指定 **\/errorreport:send** 时，编译器消息将引导您访问包含 Microsoft 数据收集策略的网站。  
  
 此选项取决于注册表设置。  有关在注册表中如何设置相应值的信息，请参见 MSDN 网站上 [How to Turn on Automatic Error Reporting in Visual Studio 2008 Command\-line Tools（如何在 Visual Studio 2008 的命令行工具中打开自动错误报告）](http://go.microsoft.com/fwlink/?LinkID=184695)。  
  
## 备注  
 当编译器无法处理源代码文件时，将导致内部编译器错误 \(ICE\)。  当发生 ICE 时，编译器不生成输出文件或可用来修复代码的任何有用的诊断。  
  
 在以前的版本中，当收到 ICE 时，最好联系 Microsoft 产品支持服务以报告问题。  现在通过使用 **\/errorreport**，您可以向 Visual C\# 团队提供 ICE 信息。  错误报告有助于改进将来的编译器版本。  
  
 用户发送报告的能力取决于计算机和用户策略权限。  
  
 调试器有关错误的更多信息，参见[Dr. Watson 的说明 \(Drwtsn32.exe\) 的工具窗口](http://go.microsoft.com/fwlink/?LinkId=147286)。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  有关详细信息，请参阅[“项目设计器”\-\>“生成”页 \(C\#\)](/visual-studio/ide/reference/build-page-project-designer-csharp)。  
  
2.  单击**“生成”**属性页。  
  
3.  单击“高级”按钮。  
  
4.  修改**“内部编译器错误报告”**属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参阅 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.ErrorReport%2A>。  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)