---
title: "#杂注校验和（C# 参考）| Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- '#pragma checksum'
dev_langs:
- CSharp
helpviewer_keywords:
- '#pragma checksum [C#]'
ms.assetid: 3673e4ca-6098-4ec1-890f-8fceb2a794a2
caps.latest.revision: 11
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5daf71faea5736036e9e3e0178e84ea03c314ff6
ms.lasthandoff: 03/13/2017

---
# <a name="pragma-checksum-c-reference"></a>#杂注校验和（C# 参考）
为源文件生成校验和，以帮助调试校验 [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] 页。  
  
## <a name="syntax"></a>语法  
  
```  
#pragma checksum "filename" "{guid}" "checksum bytes"  
```  
  
#### <a name="parameters"></a>参数  
 `"filename"`  
 需要监视更改或更新的文件的名称。  
  
 `"{guid}"`  
 文件的全局唯一标识符 (GUID)。  
  
 `"checksum_bytes"`  
 表示校验和字节的十六进制数字的字符串。 必须是偶数个十六进制数字。 奇数个十六进制数字会导致编译时警告，指令会被忽略。  
  
## <a name="remarks"></a>备注  
 Visual Studio 调试器使用校验和确保它可始终找到正确的源。 编译器为源文件计算校验和，然后将输出发出到程序数据库 (PDB) 文件。 调试器随后使用 PDB 针对它为源文件计算的校验和进行比较。  
  
 此解决方案不适合 [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] 项目，因为计算的校验和用于生成的源文件，而不是 .aspx 文件。 为了解决此问题，`#pragma checksum` 为 [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] 页提供了校验和支持。  
  
 在 [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] 中创建 [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] 项目时，生成的源文件包含从其生成源的 .aspx 文件的校验和。 编译器随后将此信息写入 PDB 文件中。  
  
 如果编译器在文件中未遇到 `#pragma checksum` 指令，则它会计算校验和并将值写入 PDB 文件中。  
  
## <a name="example"></a>示例  
  
```  
class TestClass  
{  
    static int Main()  
    {  
        #pragma checksum "file.cs" "{3673e4ca-6098-4ec1-890f-8fceb2a794a2}" "{012345678AB}" // New checksum  
    }  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 预处理器指令](../../../csharp/language-reference/preprocessor-directives/index.md)
