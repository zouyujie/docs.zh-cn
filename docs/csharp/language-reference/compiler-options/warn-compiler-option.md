---
title: "/warn (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/warn"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "warning level [C#]"
  - "/w compiler option [C#]"
  - "-w compiler option [C#]"
  - "-warn compiler option [C#]"
  - "/warn compiler option [C#]"
  - "w compiler option [C#]"
  - "warn compiler option [C#]"
ms.assetid: 5f80ff59-4991-4382-9f9a-77da18446e71
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# /warn (C# Compiler Options)
**\/warn** 选项指定编译器要显示的警告等级。  
  
## 语法  
  
```  
/warn:option  
```  
  
## 参数  
 `option`  
 您希望为编译显示的警告等级：较小的数字只显示高严重度的警告；数字越大，显示的警告越多。  有效值为 0 到 4：  
  
|警告等级|含义|  
|----------|--------|  
|0|关闭所有警告消息的显示。|  
|1|显示严重的警告消息。|  
|2|显示等级 1 警告以及某些不太严重的警告，如关于隐藏类成员的警告。|  
|3|显示等级 2 警告以及某些不太严重的警告，例如有关总是计算为 `true` 或 `false` 的表达式的警告。|  
|4（默认）|显示所有等级 3 警告以及信息性警告。|  
  
## 备注  
 若要获得有关错误或警告的信息，可以在帮助索引中查找错误代码。  有关获得错误或警告信息的其他方式，请参见[C\# Compiler Errors](../../../csharp/language-reference/compiler-messages/index.md)。  
  
 使用 [\/warnaserror](../../../csharp/language-reference/compiler-options/warnaserror-compiler-option.md) 可将所有的警告都视为错误。  可以使用 [\/nowarn](../../../csharp/language-reference/compiler-options/nowarn-compiler-option.md) 禁用某些警告。  
  
 **\/w** 是 **\/warn** 的缩写形式。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“生成”**属性页。  
  
3.  修改**“警告等级”**属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参见 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.WarningLevel%2A>。  
  
## 示例  
 编译 `in.cs` 并让编译器仅显示等级 1 警告：  
  
```  
csc /warn:1 in.cs  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)