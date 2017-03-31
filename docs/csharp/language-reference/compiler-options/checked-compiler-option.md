---
title: "-checked（C# 编译器选项）| Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /checked
dev_langs:
- CSharp
helpviewer_keywords:
- checked compiler option [C#]
- -checked compiler option [C#]
- /checked compiler option [C#]
ms.assetid: fb7475d3-e6a6-4e6d-b86c-69e7a74c854b
caps.latest.revision: 20
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
ms.openlocfilehash: c6cfc54c2dbd3e14d874d7684fdc75a972260cc3
ms.lasthandoff: 03/13/2017

---
# <a name="checked-c-compiler-options"></a>/checked（C# 编译器选项）
**/checked** 选项指定，不在 [checked](../../../csharp/language-reference/keywords/checked.md) 或 [unchecked](../../../csharp/language-reference/keywords/unchecked.md) 关键字的范围内、并且产生的值超出数据类型范围的整数算法语句是否将导致运行时异常。  
  
## <a name="syntax"></a>语法  
  
```  
/checked[+ | -]  
```  
  
## <a name="remarks"></a>备注  
 `checked` 或 `unchecked` 关键字范围内的整数算法语句不受“/checked”****选项的影响。  
  
 如果不在 `checked` 或 `unchecked` 关键字范围内的整数算法语句产生的值超出数据类型范围，并且编译中使用了 **/checked+** (**/checked**)，则该语句将在运行时导致异常。 如果编译中使用的是 **/checked-**，则该语句在运行时不会导致异常。  
  
 该选项的默认值为 **/checked-**。 使用 **/checked-** 的一个方案是生成大型应用程序。 有时使用自动化工具生成此类应用程序，这种工具可以将 **/checked** 自动设置为 +。 可通过指定 **/checked-** 替代工具的全局默认值。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的“属性”****页。 有关详细信息，请参阅 [“项目设计器”->“生成”页 (C#)](https://docs.microsoft.com/visualstudio/ide/reference/build-page-project-designer-csharp)。  
  
2.  单击“生成”****属性页。  
  
3.  单击 **“高级”** 按钮。  
  
4.  修改“检查算术溢出/下溢”****属性。  
  
 有关以编程方式访问此编译器选项的信息，请参阅 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.CheckForOverflowUnderflow%2A>。  
  
## <a name="example"></a>示例  
 以下命令编译 `t2.cs`。 命令中 `/checked` 的使用指定，任何不在 `checked` 或 `unchecked` 关键字范围内以及导致数据类型以外值的结果的文件中的整数算术语句，会在运行时引发异常。  
  
```  
csc t2.cs /checked  
```  
  
## <a name="see-also"></a>另请参阅  
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [NIB 如何：修改项目属性和配置设置](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)
