---
title: "#pragma checksum（C# 参考） | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "#pragma checksum"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#pragma 校验和 [C#]"
ms.assetid: 3673e4ca-6098-4ec1-890f-8fceb2a794a2
caps.latest.revision: 11
caps.handback.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# #pragma checksum（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

生成源文件的校验和，以帮助调试 [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] 页。  
  
## 语法  
  
```  
#pragma checksum "filename" "{guid}" "checksum bytes"  
```  
  
#### 参数  
 `"filename"`  
 要求监视更改或更新的文件的名称。  
  
 `"{guid}"`  
 文件的全局唯一标识符 \(GUID\)。  
  
 `"checksum_bytes"`  
 十六进制数的字符串，表示校验和的字节。  必须是偶数位的十六进制数。  奇数位的十六进制数字会导致编译时警告，然后指令被忽略。  
  
## 备注  
 Visual Studio 调试器使用校验和来确保找到的总是正确的源。  编译器计算源文件的校验和，然后将输出发出到程序数据库 \(PDB\) 文件。  最后，调试器使用 PDB 来比较它为源文件计算的校验和。  
  
 此解决方案不适用于 [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] 项目，因为算出的校验和是生成的源文件的校验和，而不是 .aspx 文件的校验和。  为解决此问题，`#pragma checksum` 为 [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] 页提供了校验和支持。  
  
 在 [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] 中创建 [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] 项目时，生成的源文件包含 .aspx 文件（从该文件生成源文件）的校验和。  然后，编译器将此信息写入 PDB 文件。  
  
 如果编译器在该文件中没有遇到 `#pragma checksum` 指令，它将计算校验和，然后将算出的值写入 PDB 文件。  
  
## 示例  
  
```  
class TestClass  
{  
    static int Main()  
    {  
        #pragma checksum "file.cs" "{3673e4ca-6098-4ec1-890f-8fceb2a794a2}" "{012345678AB}" // New checksum  
    }  
}  
```  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 预处理器指令](../../../csharp/language-reference/preprocessor-directives/index.md)