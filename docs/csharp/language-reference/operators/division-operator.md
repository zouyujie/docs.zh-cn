---
title: "/ 运算符（C# 参考）| Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- / operator [C#]
- division operator [C#]
ms.assetid: d155e496-678f-4efa-bebe-2bd08da2c5af
caps.latest.revision: 21
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
ms.openlocfilehash: 387be8c240001557722b4a30b785637c72c9be37
ms.lasthandoff: 03/13/2017

---
# <a name="-operator-c-reference"></a>/ 运算符（C# 参考）
除法运算符 (`/`) 将其第一操作数除以第二操作数。 所有数值类型都具有预定义的除法运算符。  
  
## <a name="remarks"></a>备注  
 用户定义的类型可以重载 `/` 运算符（请参阅[运算符](../../../csharp/language-reference/keywords/operator.md)）。 重载 `/` 运算符将隐式地重载 [/= operator](division-assignment-operator.md)。  
  
 两个整数相除，其结果始终为整数。 例如，7 除以 3 得 2。 要确定 7 除以 3 的余数，请使用余数运算符 ([%](../../../csharp/language-reference/operators/modulus-operator.md))。 要获得有理数或分数形式的商，请将被除数或除数设为类型 `float` 或类型 `double`。 如果通过将数字置于小数点右侧的方式以十进制表示被除数或除数，则可以隐式地分配类型，如以下示例所示。  
  
## <a name="example"></a>示例  
 [!code-cs[csRefOperators#42](../../../csharp/language-reference/operators/codesnippet/CSharp/division-operator_1.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 运算符](../../../csharp/language-reference/operators/index.md)

