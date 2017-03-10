---
title: "=&gt; 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "=>_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "lambda 运算符 [C#]"
  - "=> 运算符 [C#]"
  - "lambda 表达式 [C#], => 运算符"
ms.assetid: 8c899251-dafa-4594-bec7-243b39072880
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# =&gt; 运算符（C# 参考）
`=>` 标记称作 lambda 运算符。  该标记在 lambda 表达式中用来将左侧的输入变量与右侧的 lambda 体分离。  Lambda 表达式是与匿名方法类似的内联表达式，但更加灵活；在以方法语法表示的 LINQ 查询中广泛使用了 Lambda 表达式。  有关更多信息，请参见[Lambda 表达式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)。  
  
 下面的示例演示两种查找并显示最短的字符串的长度在字符数组中的字符串。  该示例的第一部分将 lambda 表达式 \(`w => w.Length`\) `words` 于数组的每个元素都使用 <xref:System.Linq.Enumerable.Min%2A> 方法查找最小长度。  为了进行比较，该示例的第二部分演示一个较长的解决方案使用查询语法执行相同操作。  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
## 备注  
 `=>` 运算符具有与赋值运算符 \(`=`\) 相同的优先级，并且是右结合运算符。  
  
 可以显式指定输入变量的类型或让编译器推断类型；仍，该变量是强类型在编译时。  当指定类型时，必须将该类型括号中的名称和变量名，如下例所示。  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
## 示例  
 下面的代码演示如何编写采用两个参数标准查询运算符 <xref:System.Linq.Enumerable.Where%2A?displayProperty=fullName> 的超加载的 lambda 表达式。  由于 lambda 表达式具有多个参数，必须括在括号中的参数。  第二个参数，`index`，表示当前元素的索引集合中的。  `Where` 表达式返回长度小于其在数组的索引位置小于的任何字符串。  
  
```c#  
static void Main(string[] args)  
{  
    string[] digits = { "zero", "one", "two", "three", "four", "five",   
            "six", "seven", "eight", "nine" };  
  
    Console.WriteLine("Example that uses a lambda expression:");  
    var shortDigits = digits.Where((digit, index) => digit.Length < index);  
    foreach (var sD in shortDigits)  
    {  
        Console.WriteLine(sD);  
    }  
  
    // Compare the following code, which arrives at the same list of short  
    // digits but takes more work to get there.  
    Console.WriteLine("\nExample that uses a for loop:");  
    List<string> shortDigits2 = new List<string>();  
    for (var i = 0; i < digits.Length; i++)  
    {  
        if (digits[i].Length < i)  
            shortDigits2.Add(digits[i]);  
    }  
  
    foreach (var d in shortDigits2)  
    {  
        Console.WriteLine(d);  
    }  
    // Output:  
    // Example that uses a lambda expression:  
    // five  
    // six  
    // seven  
    // eight  
    // nine  
  
    // Example that uses a for loop:  
    // five  
    // six  
    // seven  
    // eight  
    // nine  
}  
```  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [Lambda 表达式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)