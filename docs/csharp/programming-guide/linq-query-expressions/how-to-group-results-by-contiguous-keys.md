---
redirect_url: /dotnet/articles/csharp/linq/group-results-by-contiguous-keys
caps.handback.revision: 11
---
# 如何：按连续键对结果进行分组（C# 编程指南）
下面的示例演示如何将元素归到不同的块区中，块区表示连续键的子序列。  例如，假设您有下面的键值对序列：  
  
|键|值|  
|-------|-------|  
|A|We|  
|A|think|  
|A|that|  
|B|Linq|  
|C|为|  
|A|really|  
|B|cool|  
|B|\!|  
  
 将按照下面的顺序创建以下各组：  
  
1.  We, think, that  
  
2.  Linq  
  
3.  为  
  
4.  really  
  
5.  cool, \!  
  
 此解决方案作为扩展方法实现，扩展方法是线程安全的且以流的方式返回其结果。  也就是说，它在移动通过源序列的过程中生成自己的各个组。  与 `group` 或 `orderby` 运算符不同，它可以在整个序列读取完毕之前就开始将组返回给调用方。  
  
 线程安全性是通过在迭代源序列的过程中创建每个组或块区的副本来实现的，如源代码注释中所述。  如果源序列包含一个由连续项组成的很大的序列，则公共语言运行时可能会引发 <xref:System.OutOfMemoryException>。  
  
## 示例  
 下面的示例显示了此扩展方法及使用它的客户端代码。  
  
 [!code-cs[cscsrefContiguousGroups#1](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/how-to-group-results-by-_1.cs)]  
  
 若要在您的项目中使用此扩展方法，请将 `MyExtensions` 静态类复制到一个新的或现有源代码文件中，并在必要时，为该类所在的命名空间添加一条 `using` 指令。  
  
## 请参阅  
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Classification of Standard Query Operators by Manner of Execution](../../../visual-basic/programming-guide/concepts/linq/classification-of-standard-query-operators-by-manner-of-execution.md)