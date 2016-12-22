---
title: "C# 运算符 | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "cs.operators"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "寻址运算符 [C#]"
  - "算术运算符 [C#]"
  - "赋值运算符 [C#]"
  - "按位运算符 [C#]"
  - "布尔运算符 [C#]"
  - "表达式 [C#], 运算符"
  - "间接寻址运算符 [C#]"
  - "关键字 [C#], 运算符"
  - "逻辑运算符 [C#]"
  - "运算符 [C#]"
  - "关系运算符 [C#]"
  - "移位运算符 [C#]"
  - "Visual C#, 运算符"
ms.assetid: 0301e31f-22ad-49af-ac3c-d5eae7f0ac43
caps.latest.revision: 40
caps.handback.revision: 38
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# C# 运算符
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

C\# 提供了许多运算符，这些运算符是指定要在表达式中执行哪些操作（数学、索引、函数调用等等）的符号。  在应用于用户定义类型之前，你可以对许多运算符进行[重载](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md)以更改其含义。  
  
 针对整型类型的运算（如 `==`、`!=`、`<`、`>`、`&`、                  `|` ）通常可用于枚举 \(`enum`\) 类型。  
  
 以下章节按最高优先级到最低优先级的顺序列示 C\# 运算符。  各章节内运算符的优先级相同。  
  
## 主要运算符  
 以下是具有最高优先级的运算符。  请注意，你可以单击运算符转到包含示例的详细页面。  
  
 [x.y](../../../csharp/language-reference/operators/member-access-operator.md) － 成员访问。  
  
 [x?.y](../../../csharp/language-reference/operators/null-conditional-operators.md) － null 条件成员访问。  如果左边操作数为 null，则返回 null。  
  
 [f\(x\)](../../../csharp/language-reference/operators/invocation-operator.md) － 函数调用。  
  
 [a&#91;x&#93;](../../../csharp/language-reference/operators/index-operator.md) － 聚合对象索引。  
  
 [a?&#91;x&#93;](../../../csharp/language-reference/operators/null-conditional-operators.md) － null 条件索引。  如果左边操作数为 null，则返回 null。  
  
 [x\+\+](../../../csharp/language-reference/operators/increment-operator.md) － 后缀递增。  先返回 x 值，然后用加 1（通常加整数 1）后的 x 值更新存储位置。  
  
 [x\-\-](../../../csharp/language-reference/operators/decrement-operator.md) － 后缀递减。  先返回 x 值，然后用减 1（通常减整数 1）后的 x 值更新存储位置。  
  
 [New](../../../csharp/language-reference/keywords/new-operator.md) － 类型实例化。  
  
 [Typeof](../../../csharp/language-reference/keywords/typeof.md) － 返回表示操作数的 System.Type 对象。  
  
 [Checked](../../../csharp/language-reference/keywords/checked.md) － 对整数运算启用溢出检查。  
  
 [Unchecked](../../../csharp/language-reference/keywords/unchecked.md) － 对整数运算禁用溢出检查。  这是默认的编译器行为。  
  
 [default\(T\)](../../../csharp/programming-guide/generics/default-keyword-in-generic-code.md) － 返回类型 T 的默认初始化值，T 为引用类型时返回 null，T 为数值类型时返回零，T 为结构类型时返回填充为零\/null 的成员。  
  
 [Delegate](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md) － 声明并返回一个委托实例。  
  
 [Sizeof](../../../csharp/language-reference/keywords/sizeof.md) － 返回类型操作数的大小（以字节为单位）。  
  
 [\-\>](../../../csharp/language-reference/operators/dereference-operator.md) － 取消指针引用与成员访问相结合。  
  
## 一元运算符  
 这些运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击运算符转到包含示例的详细页面。  
  
 [\+x](../../../csharp/language-reference/operators/addition-operator.md) － 返回 x 值。  
  
 [\-x](../../../csharp/language-reference/operators/subtraction-operator.md) － 数值求反。  
  
 [\!x](../../../csharp/language-reference/operators/logical-negation-operator.md) － 逻辑求反。  
  
 [~x](../../../csharp/language-reference/operators/bitwise-complement-operator.md) － 按位求补。  
  
 [\+\+x](../../../csharp/language-reference/operators/increment-operator.md) － 前缀递增。  先用加 1（通常加整数 1）后的 x 值更新存储位置，然后返回 x 值。  
  
 [\-\-x](../../../csharp/language-reference/operators/decrement-operator.md) － 前缀递减。  先用减 1（通常减整数 1）后的 x 值更新存储位置，然后返回 x 值。  
  
 [\(T\)x](../../../csharp/language-reference/operators/invocation-operator.md) － 类型转换。  
  
 [Await](../../../csharp/language-reference/keywords/await.md) － 等待 `Task`。  
  
 [&x](../../../csharp/language-reference/operators/and-operator.md) － 地址。  
  
 [\*x](../../../csharp/language-reference/operators/multiplication-operator.md) － 取消引用。  
  
## 乘法运算符  
 这些运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击运算符转到包含示例的详细页面。  
  
 [x \* y](../../../csharp/language-reference/operators/multiplication-operator.md) － 乘法。  
  
 [x \/ y](../../../csharp/language-reference/operators/division-operator.md) － 除法。  如果操作数均为整数，则结果为整数，舍去小数（例如，`-7 / 2 is -3`）。  
  
 [x % y](../../../csharp/language-reference/operators/modulus-operator.md) － 取模。  如果操作数均为整数，则返回 x 除以 y 后的余数。  如果 `q = x / y` 且 `r = x % y`，则 `x = q * y + r`。  
  
## 加法运算符  
 这些运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击运算符转到包含示例的详细页面。  
  
 [x \+ y](../../../csharp/language-reference/operators/addition-operator.md) － 加法。  
  
 [x – y](../../../csharp/language-reference/operators/subtraction-operator.md) － 减法。  
  
## 移位运算符  
 这些运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击运算符转到包含示例的详细页面。  
  
 [x \<\< y](../Topic/%3C%3C%20Operator%20\(C%23%20Reference\).md) － 向左移位，右边移出的空位补零。  
  
 [x \>\> y](../../../csharp/language-reference/operators/right-shift-operator.md) － 向右移位。  如果左操作数是 `int` 或 `long`，则左位数补符号位。  如果左操作数是 `uint` 或 `ulong`，则左位数补零。  
  
## 关系和类型测试运算符  
 这些运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击运算符转到包含示例的详细页面。  
  
 [x \< y](../../../csharp/language-reference/operators/less-than-operator.md) － 小于（如果 x 小于 y，则为 true）。  
  
 [x \> y](../../../csharp/language-reference/operators/greater-than-operator.md) － 大于（如果 x 大于 y，则为 true）。  
  
 [x \<\= y](../../../csharp/language-reference/operators/less-than-equal-operator.md) － 小于等于。  
  
 [x \>\= y](../../../csharp/language-reference/operators/greater-than-equal-operator.md) － 大于等于。  
  
 [Is](../../../csharp/language-reference/keywords/is.md) － 类型兼容性。  如果求值后的左操作数可以转换为右操作数中指定的类型（静态类型），则返回 true。  
  
 [As](../../../csharp/language-reference/keywords/as.md) － 类型转换。  返回左操作数并转换为右操作数中指定的类型（静态类型），但 `as` 返回 `null`，其中 `(T)x` 会引发异常。  
  
## 相等运算符  
 这些运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击运算符转到包含示例的详细页面。  
  
 [x \=\= y](../../../csharp/language-reference/operators/equality-comparison-operator.md) － 相等。  默认情况下，对于 `string` 以外的引用类型，此运算符返回引用相等（标识测试）。  但是，类型可以重载 `==`，因此，如果你想测试标识，最好对 `object` 使用 `ReferenceEquals` 方法。  
  
 [x \!\= y](../../../csharp/language-reference/operators/not-equal-operator.md) － 不相等。  请参阅有关 `==` 的注释。  如果某个类型重载 `==`，则它必须重载 `!=`。  
  
## 逻辑 AND 运算符  
 此运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击该运算符转到包含示例的详细页面。  
  
 [x & y](../../../csharp/language-reference/operators/and-operator.md) － 逻辑或位 AND。  与整数类型一起使用，并且通常允许 `enum` 类型。  
  
## 逻辑 XOR 运算符  
 此运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击该运算符转到包含示例的详细页面。  
  
 [x ^ y](../../../csharp/language-reference/operators/xor-operator.md) － 逻辑或位 XOR。  通常可以将此运算符与整数类型和 `enum` 类型一起使用。  
  
## 逻辑 OR 运算符  
 此运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击该运算符转到包含示例的详细页面。  
  
 [x &#124; y](../../../csharp/language-reference/operators/or-operator.md) － 逻辑或位 OR。  与整数类型一起使用，并且通常允许 `enum` 类型。  
  
## 条件 AND 运算符  
 此运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击该运算符转到包含示例的详细页面。  
  
 [x && y](../../../csharp/language-reference/operators/conditional-and-operator.md) － 逻辑 AND。  如果第一个操作数为 false，则 C\# 不对第二个操作数求值。  
  
## 条件 OR 运算符  
 此运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击该运算符转到包含示例的详细页面。  
  
 [x &#124;&#124; y](../Topic/%7C%7C%20Operator%20\(C%23%20Reference\).md) － 逻辑 OR。  如果第一个操作数为 true，则 C\# 不对第二个操作数求值。  
  
## Null 合并运算符  
 此运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击该运算符转到包含示例的详细页面。  
  
 [x ?? y](../../../csharp/language-reference/operators/null-conditional-operator.md) － 如果不为 `null`，则返回 `x`；否则返回 `y`。  
  
## 条件运算符  
 此运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击该运算符转到包含示例的详细页面。  
  
 [t ? x : y](../Topic/?:%20Operator%20\(C%23%20Reference\).md) － 如果测试 `t` 为 true，则求值并返回 `x`；否则，求值并返回 `y`。  
  
## 赋值和 Lambda 运算符  
 这些运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击运算符转到包含示例的详细页面。  
  
 [x \= y](../../../csharp/language-reference/operators/assignment-operator.md) － 赋值。  
  
 [x \+\= y](../../../csharp/language-reference/operators/addition-assignment-operator.md) － 递增。  `x` 值加 `y` 值，结果存储在 `x` 中，并返回新值。  如果 `x` 指定 `event`，则 `y` 必须是 C\# 作为事件处理程序添加的相应函数。  
  
 [x \-\= y](../../../csharp/language-reference/operators/subtraction-assignment-operator-1.md) － 递减。  `x` 值减 `y` 值，结果存储在 `x` 中，并返回新值。  如果 `x` 指定 `event`，则 `y` 必须是 C\# 作为事件处理程序删除的相应函数  
  
 [x \*\= y](../../../csharp/language-reference/operators/multiplication-assignment-operator.md) － 乘法赋值。  `x` 值乘以 `y` 值，结果存储在 `x` 中，并返回新值。  
  
 [x \/\= y](../../../csharp/language-reference/operators/subtraction-assignment-operator.md) － 除法赋值。  `x` 值除以 `y` 值，结果存储在 `x` 中，并返回新值。  
  
 [x %\= y](../../../csharp/language-reference/operators/modulus-assignment-operator.md) － 取模赋值。  `x` 值除以 `y` 值，余数存储在 `x` 中，并返回新值。  
  
 [x &\= y](../../../visual-basic/language-reference/operators/and-assignment-operator.md) － AND 赋值。  `y` 值和 `x` 值相与，结果存储在 `x` 中，并返回新值。  
  
 [x &#124;\= y](../../../csharp/language-reference/operators/or-assignment-operator.md) － OR 赋值。  `y` 值和 `x` 值相或，结果存储在 `x` 中，并返回新值。  
  
 [x ^\= y](../../../csharp/language-reference/operators/xor-assignment-operator.md) － XOR 赋值。  `y` 值和 `x` 值相异或，结果存储在 `x` 中，并返回新值。  
  
 [x \<\<\= y](../../../csharp/language-reference/operators/left-shift-assignment-operator.md) － 左移赋值。  将 `x` 值向左移动 `y` 位，结果存储在 `x` 中，并返回新值。  
  
 [x \>\>\= y](../../../csharp/language-reference/operators/right-shift-assignment-operator.md) － 右移赋值。  将 `x` 值向右移动 `y` 位，结果存储在 `x` 中，并返回新值。  
  
 [\=\>](../../../csharp/language-reference/operators/lambda-operator.md) － lambda 声明。  
  
## 算术溢出  
 算术运算符（[\+](../../../csharp/language-reference/operators/addition-operator.md)、[\-](../../../csharp/language-reference/operators/subtraction-operator.md)、[\*](../../../csharp/language-reference/operators/multiplication-operator.md)、[\/](../../../csharp/language-reference/operators/division-operator.md)）产生的结果可能会超出所涉数值类型的可能值的范围。  详细信息应参考特定运算符的相关章节，而一般情况下：  
  
-   整数算术溢出或者引发 <xref:System.OverflowException>，或者放弃结果的最高有效位。  整数被零除总是引发 `DivideByZeroException`。  
  
-   浮点算术溢出或被零除从不引发异常，因为浮点类型基于 IEEE 754，因此可以表示无穷大和 NaN（非数值）。  
  
-   [小数](../../../csharp/language-reference/keywords/decimal.md)算术溢出总是引发 <xref:System.OverflowException>。  小数被零除总是引发 <xref:System.DivideByZeroException>。  
  
 当发生整数溢出时，产生的结果取决于执行上下文，该上下文可为 [checked 或 unchecked](../../../csharp/language-reference/keywords/checked-and-unchecked.md)。  在 checked 上下文中引发 <xref:System.OverflowException>。  在 unchecked 上下文中，放弃结果的最高有效位并继续执行。  因此，C\# 让你有机会选择处理或忽略溢出。  
  
 除算术运算符以外，整型类型之间的转换也会导致溢出（例如，将 [long](../../../csharp/language-reference/keywords/long.md) 转换为 [int](../../../csharp/language-reference/keywords/int.md)）并受 checked 或 unchecked 执行的限制。  但是，位运算符和移位运算符永远不会导致溢出。  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\#](../../../csharp/csharp.md)   
 [可重载运算符](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)