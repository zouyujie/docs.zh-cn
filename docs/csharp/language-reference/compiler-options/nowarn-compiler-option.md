---
title: "-nowarn（C# 编译器选项）| Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /nowarn
dev_langs:
- CSharp
helpviewer_keywords:
- nowarn compiler option [C#]
- /nowarn compiler option [C#]
- -nowarn compiler option [C#]
ms.assetid: 6dcbc5e8-ae67-4566-9df3-f63cfdd9c4e4
caps.latest.revision: 24
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
ms.openlocfilehash: 34152b6e7247ac112bcc9c725402b8c9a5d631ed
ms.lasthandoff: 03/13/2017

---
# <a name="nowarn-c-compiler-options"></a>/nowarn（C# 编译器选项）
**/nowarn** 选项使你可以禁止编译器显示一个或多个警告。 使用逗号分隔多个警告编号。  
  
## <a name="syntax"></a>语法  
  
```  
/nowarn:number1[,number2,...]  
```  
  
## <a name="arguments"></a>自变量  
 `number1`, `number2`  
 希望编译器禁止显示的警告编号。  
  
## <a name="remarks"></a>备注  
 只应指定警告标识符的数值部分。 例如，如果要禁止显示 CS0028，则可以指定 `/nowarn:28`。  
  
 编译器会以无提示方式忽略传递给 `/nowarn` 的警告编号，这些编号在早期版本中有效，但已从编译器中移除。 例如，CS0679 在 Visual Studio .NET 2002 的编译器中有效，但是在后来已移除。  
  
 无法通过 `/nowarn` 选项禁止显示以下警告：  
  
-   编译器警告（等级 1）CS2002  
  
-   编译器警告（等级 1）CS2023  
  
-   编译器警告（等级 1）CS2029  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的“属性” **** 页。 有关详细信息，请参阅[“项目设计器”->“生成”页 (C#)](https://docs.microsoft.com/visualstudio/ide/reference/build-page-project-designer-csharp)。  
  
2.  单击“生成”****属性页。  
  
3.  修改“禁止显示警告”****属性。  
  
 有关如何以编程方式设置此编译器的信息，请参阅 <xref:VSLangProj80.ProjectProperties3.DelaySign%2A>。  
  
## <a name="see-also"></a>请参阅  
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [NIB 如何：修改项目属性和配置设置](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [C# 编译器错误](../../../csharp/language-reference/compiler-messages/index.md)
