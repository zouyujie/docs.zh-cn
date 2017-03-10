---
title: "如何：在 LINQ 外部使用 Lambda 表达式（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "lambda 表达式 [C#], LINQ 外部"
ms.assetid: 2b519274-6ee4-4455-ab2e-aed67dbfd07c
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# 如何：在 LINQ 外部使用 Lambda 表达式（C# 编程指南）
Lambda 表达式并不只限于在 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 查询中使用。  可以在需要委托值的任何地方（也就是在可以使用匿名方法的任何地方）使用这些表达式。  下面的示例演示如何在 Windows 窗体事件处理程序中使用 Lambda 表达式。  请注意，输入的类型（<xref:System.Object> 和 <xref:System.Windows.Forms.MouseEventArgs>）由编译器推理，因此不必在 Lambda 输入参数中显式给定。  
  
## 示例  
  
```  
public partial class Form1 : Form  
{  
    public Form1()  
    {  
        InitializeComponent();  
        // Use a lambda expression to define an event handler.  
       this.Click += (s, e) => { MessageBox.Show(((MouseEventArgs)e).Location.ToString());};  
    }  
}  
```  
  
## 请参阅  
 [Lambda 表达式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)