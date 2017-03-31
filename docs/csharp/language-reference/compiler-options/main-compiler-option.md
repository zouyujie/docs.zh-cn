---
title: "/main（C# 编译器选项）| Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /main
dev_langs:
- CSharp
helpviewer_keywords:
- -main compiler option [C#]
- main compiler option [C#]
- /main compiler option [C#]
ms.assetid: 975cf4d5-36ac-4530-826c-4aad0c7f2049
caps.latest.revision: 14
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
ms.openlocfilehash: fa8c02a6521b65e2cc4f7c8d779c1091ce399fba
ms.lasthandoff: 03/13/2017

---
# <a name="main-c-compiler-options"></a>/main（C# 编译器选项）
如果多个类包含 **Main** 方法，此选项将指定包含程序入口点的类。  
  
## <a name="syntax"></a>语法  
  
```  
/main:class  
```  
  
## <a name="arguments"></a>自变量  
 `class`  
 此类型包含 **Main** 方法。  
  
## <a name="remarks"></a>备注  
 如果编译包含具有 [Main](../../../csharp/programming-guide/main-and-command-args/index.md) 方法的多个类型，则可以指定哪个类型包含你想用作程序入口点的 **Main** 方法。  
  
 此选项用于编译 .exe 文件。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的“属性”****页。  
  
2.  单击“应用程序”****属性页。  
  
3.  修改“启动对象”****属性。  
  
     若要以编程方式设置此编译器选项，请参阅 <xref:VSLangProj80.ProjectProperties3.StartupObject%2A>。  
  
## <a name="example"></a>示例  
 编译 `t2.cs` 和 `t3.cs`，指出 **Main** 方法可在 `Test2` 中找到：  
  
```  
csc t2.cs t3.cs /main:Test2  
```  
  
## <a name="see-also"></a>请参阅  
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [NIB 如何：修改项目属性和配置设置](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)
