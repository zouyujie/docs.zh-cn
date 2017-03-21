---
title: "How to: Set Environment Variables for the Visual Studio Command Line | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "cs.build.commandline"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "csc.exe, command-line builds"
  - "Visual C#, command-line builds"
  - "command-line compilers, Visual C#"
  - "Vsvars32.bat"
  - "builds [C#], command-line"
  - "compilers, invoking from command line"
  - "Vcvars32.bat file"
  - "command line [C#], building from"
  - "Visual C# compiler, enabling"
  - "compiling source code, from command line"
ms.assetid: 7ec09480-5612-4f6a-8d00-ad90ea9bca5d
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# How to: Set Environment Variables for the Visual Studio Command Line
vsvars32.bat 文件设置适当的环境变量以启用命令行生成。  有关 vsvars32.bat 的详细信息，请参阅[知识库文章 Q248802](http://go.microsoft.com/fwlink/?LinkId=225042)。  
  
 如果安装了当前版本 Visual Studio 的计算机上也安装了 Visual Studio 的早期版本，则你不应该在同一命令提示符窗口中运行不同版本的 vsvars32.bat 或 vcvars32.bat。  
  
### 若要运行 VSVARS32.BAT  
  
1.  从“开始”菜单，打开“VS2012 开发者命令提示”。  
  
2.  更改为安装目录的 Program Files\\Microsoft Visual Studio *Version*\\Common7\\Tools 或 Program Files \(x86\)\\Microsoft Visual Studio *Version*\\Common7\\Tools 子目录。  
  
3.  通过键入 VSVARS32 运行 VSVARS32.bat。  
  
    > [!CAUTION]
    >  VSVARS32.bat 在各个计算机间可能大不相同。  不要使用另一台计算机中的 VSVARS32.bat 替换丢失或损坏的 VSVARS32.bat 文件。  而是应重新运行安装程序以替换丢失的文件。  
  
## 请参阅  
 [Command\-line Building With csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)