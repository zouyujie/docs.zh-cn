---
redirect_url: /dotnet/articles/csharp/linq/join-by-using-composite-keys
caps.handback.revision: 8
---
# 如何：使用复合键进行联接（C# 编程指南）
此示例演示如何执行想要使用多个键来定义匹配的联接操作。  使用组合键来完成此操作。  以匿名类型或包含要比较的值的命名类型的形式来创建组合键。  如果将跨方法边界传递查询变量，请使用为该键重写 <xref:System.Object.Equals%2A> 和 <xref:System.Object.GetHashCode%2A> 的命名类型。  属性的名称以及属性出现的顺序在每个键中必须相同。  
  
## 示例  
 下面的示例演示如何使用组合键来联接来自三个表中的数据：  
  
```  
var query = from o in db.Orders  
    from p in db.Products  
    join d in db.OrderDetails   
        on new {o.OrderID, p.ProductID} equals new {d.OrderID,         d.ProductID} into details  
        from d in details  
        select new {o.OrderID, p.ProductID, d.UnitPrice};  
```  
  
 组合键上的类型推理取决于这些键中属性的名称，以及属性的出现顺序。  如果源序列中属性的名称不同，您必须在键中分配新名称。  例如，如果 `Orders` 表和 `OrderDetails` 表各自为它们的列使用不同的名称，则您将通过在匿名类型中分配相同的名称来创建组合键：  
  
```  
join...on new {Name = o.CustomerName, ID = o.CustID} equals   
    new {Name = d.CustName, ID = d.CustID }  
```  
  
 还可以在 `group` 子句中使用组合键。  
  
## 编译代码  
  
-   若要编译并运行此代码，请按下面的步骤进行操作：  
  
-   打开[如何：连接到 Northwind 数据库](../Topic/How%20to:%20Connect%20to%20the%20Northwind%20Database.md)，并按照说明进行操作来设置项目并创建数据库连接。  有关更多信息，请参见 [如何：安装示例数据库](../Topic/How%20to:%20Install%20Sample%20Databases.md)。  
  
-   在 samples.cs 中创建一个新的空方法，该方法采用名为 db 的 Northwind 输入参数（与该文件中的其他方法类似）。  将此示例中的代码粘贴到方法体中。  
  
-   修改 program.cs 以从 `Main` 中调用该新方法。  
  
-   按 F5 编译并运行查询。  
  
## 请参阅  
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [join 子句](../../../csharp/language-reference/keywords/join-clause.md)   
 [group 子句](../../../csharp/language-reference/keywords/group-clause.md)