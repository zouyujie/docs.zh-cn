---
title: "/filealign (C# Compiler Options) | Microsoft Docs"
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
  - "/filealign"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/alignment compiler option [C#]"
  - "filealign compiler option [C#]"
  - "-filealign compiler option [C#]"
  - "/sections compiler option [C#]"
  - "alignment compiler option [C#]"
  - "sections compiler option [C#]"
  - "-sections compiler option [C#]"
  - "/filealign compiler option [C#]"
  - "file sharing [C#]"
  - "-alignment compiler option [C#]"
  - "section alignment [C#]"
ms.assetid: 15cf1c98-3798-4ced-9f08-60619308a073
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /filealign (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

**\/filealign** 选项使您可以指定输出文件中的节大小。  
  
## 语法  
  
```  
/filealign:number  
```  
  
## 参数  
 `number`  
 指定输出文件中节大小的值。  有效值为 512、1024、2048、4096 和 8192。  这些值以字节为单位。  
  
## 备注  
 每个节将在是 **\/filealign** 值的倍数的边界上对齐。  没有固定的默认值。  如果未指定 **\/filealign**，则公共语言运行时在编译时将选取一个默认值。  
  
 通过指定节的大小，可以影响输出文件的大小。  修改节的大小可能对将在较小设备上运行的程序有用。  
  
 使用 [DUMPBIN](/visual-cpp/build/reference/dumpbin-options) 查看有关输出文件中的节信息。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“生成”**属性页。  
  
3.  单击**“高级”**按钮。  
  
4.  修改**“文件对齐”**属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参见 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.FileAlignment%2A>。  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)