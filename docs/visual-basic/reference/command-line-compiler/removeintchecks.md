---
title: "/removeintchecks | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "removeintchecks"
  - "/removeintchecks"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/removeintchecks 编译器选项 [Visual Basic]"
  - "removeintchecks 编译器选项 [Visual Basic]"
  - "-removeintchecks 编译器选项 [Visual Basic]"
ms.assetid: c1835bd5-1e38-4fba-bd2f-6984774765d4
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /removeintchecks
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

打开或关闭整数操作的溢出错误检查。  
  
## 语法  
  
```  
/removeintchecks[+ | -]  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`+`  &#124; `-`|可选。  `/removeintchecks-` 选项导致编译器检查所有计算整数溢出检查。  默认值为 `/removeintchecks-`。<br /><br /> 指定 `/removeintchecks` 或 `/removeintchecks+` 可禁止错误检查，并可以让整数计算速度更快。  但是，如果没有进行错误检查而且数据类型容量被超出，那么将会存储错误的结果，而不会显示错误信息。|  
  
||  
|-|  
|在 Visual Studio 集成开发环境中设置 \/removeintchecks|  
|1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.  单击**“编译”**选项卡。<br />3.  单击**“高级”**按钮。<br />4.  修改**“不做整数溢出检查”**框中的值。|  
  
## 示例  
 下面的代码编译 `Test.vb` 并关闭整数溢出错误检查。  
  
```  
vbc /removeintchecks+ test.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)