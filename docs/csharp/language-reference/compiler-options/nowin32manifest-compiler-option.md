---
title: "-nowin32manifest（C# 编译器选项）| Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /nowin32manifest
dev_langs:
- CSharp
helpviewer_keywords:
- nowin32manifest compiler option [C#]
- -nowin32manifest compiler option [C#]
- /nowin32manifest compiler option [C#]
ms.assetid: 6f06365b-b87b-46a2-b187-b3bfeaf4862d
caps.latest.revision: 15
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
ms.openlocfilehash: ce96938ee00df7bfae742369673f75f8d39abd12
ms.lasthandoff: 03/13/2017

---
# <a name="nowin32manifest-c-compiler-options"></a>/nowin32manifest（C# 编译器选项）
使用 **/nowin32manifest** 选项可指示编译器不将任何应用程序清单嵌入到可执行文件中。  
  
## <a name="syntax"></a>语法  
  
```  
/nowin32manifest  
```  
  
## <a name="remarks"></a>备注  
 使用此选项时，除非在 Win32 资源文件或以后的生成步骤中提供应用程序清单，否则应用程序会受到 Windows Vista 上虚拟化的影响。  
  
 在 Visual Studio 的“应用程序属性”****页中，通过在“清单”下拉列表中选择“创建不带清单的应用程序”选项来设置此选项********。 有关详细信息，请参阅[“项目设计器”->“应用程序”页 (C#)](https://docs.microsoft.com/visualstudio/ide/reference/application-page-project-designer-csharp)。  
  
 有关创建清单的详细信息，请参阅 [/win32manifest（C# 编译器选项）](../../../csharp/language-reference/compiler-options/win32manifest-compiler-option.md)。  
  
## <a name="see-also"></a>请参阅  
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [NIB 如何：修改项目属性和配置设置](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)
