---
title: "无法发出程序集：&lt;错误消息&gt; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30145"
  - "bc30145"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30145"
ms.assetid: 2e7eb2b9-eda6-4bdb-95cc-72c7f0be7528
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 无法发出程序集：&lt;错误消息&gt;
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

此[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器会调用程序集链接器（Al.exe，也称为 Alink）来生成一个具有清单的程序集，而该链接器会在创建该程序集的发出阶段报告一个错误。  
  
 **错误 ID：**BC30145  
  
### 更正此错误  
  
1.  检查引用的错误信息并参考 [Al.exe Tool Errors and Warnings](http://msdn.microsoft.com/zh-cn/7f125d49-0a03-47a6-9ba9-d61a679a7d4b) 主题，以获得进一步的解释和建议。  
  
2.  使用 [Al.exe（程序集链接器）](../Topic/Al.exe%20\(Assembly%20Linker\).md) 或 [Sn.exe（强名称工具）](../Topic/Sn.exe%20\(Strong%20Name%20Tool\).md)，尝试手动对程序集进行签名。  
  
3.  如果仍然出现错误，则收集有关该情况的信息并通知 Microsoft 产品支持服务。  
  
### 手动对程序集进行签名  
  
1.  使用 [Sn.exe（强名称工具）](../Topic/Sn.exe%20\(Strong%20Name%20Tool\).md) 创建公钥\/私钥对文件。  
  
     此文件的扩展名为 .snk。  
  
2.  从项目中删除生成错误的 COM 引用。  
  
3.  从 Windows**“开始”**菜单，指向**“程序”**，指向**“Microsoft Visual Studio 2008”**，指向**“Visual Studio 工具”**，然后单击**“Visual Studio 2008 命令提示”**。  
  
4.  移动到要放置程序集包装的目录。  
  
5.  键入以下代码。  
  
    ```  
    tlbimp <path to COM reference file> /out:<output assembly name> /keyfile:<path to .snk file>  
    ```  
  
     下面是你可能会输入的代码的示例。  
  
    ```  
    tlbimp c:\windows\system32\msi.dll /out:Interop.WindowsInstaller.dll /keyfile:"c:\documents and settings\mykey.snk"  
    ```  
  
     如果路径或文件包含空格，则使用双引号 \("\)。  
  
6.  在 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 中，添加对刚创建的文件的 .NET 程序集引用。  
  
## 请参阅  
 [Al.exe（程序集链接器）](../Topic/Al.exe%20\(Assembly%20Linker\).md)   
 [Al.exe Tool Errors and Warnings](http://msdn.microsoft.com/zh-cn/7f125d49-0a03-47a6-9ba9-d61a679a7d4b)   
 [Sn.exe（强名称工具）](../Topic/Sn.exe%20\(Strong%20Name%20Tool\).md)   
 [如何：创建公钥\/私钥对](../Topic/How%20to:%20Create%20a%20Public-Private%20Key%20Pair.md)   
 [与我们交流](/visual-studio/ide/talk-to-us)