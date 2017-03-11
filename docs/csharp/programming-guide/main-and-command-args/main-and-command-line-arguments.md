---
redirect_url: /dotnet/articles/csharp/programming-guide/main-and-command-args/
caps.handback.revision: 30
---
# Main() 和命令行参数（C# 编程指南）
`Main`方法是 C\# 控制台应用程序或窗口应用程序的入口点。  （库和服务不要求将 `Main` 方法作为入口点。）  应用程序启动时，`Main` 方法是第一个调用的方法。  
  
 C\# 程序中只能有一个入口点。  如果您有多个类都包含 `Main` 方法，则必须使用 **\/main** 编译器选项编译您的程序，以指定用作入口点的 `Main` 方法。  有关更多信息，请参见[\/main \(Specify Location of Main Method\)](../../../csharp/language-reference/compiler-options/main-compiler-option.md)。  
  
 [!code-cs[csProgGuideMain#17](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/main-and-command-line-ar_1.cs)]  
  
## 概述  
  
-   `Main` 方法是 .exe 程序的入口点，程序控制流在该处开始和结束。  
  
-   `Main` 在类或结构内声明。  `Main` 必须是 [静态](../../../csharp/language-reference/keywords/static.md)，且不应该是 [公开](../../../csharp/language-reference/keywords/public.md)。  （在前面的示例中，它接受默认访问级别 [private](../../../csharp/language-reference/keywords/private.md)。）但不要求封闭类或结构是静态的。  
  
-   `Main` 的返回类型有两种：`void` 或 `int`。  
  
-   所声明的 `Main` 方法可以具有包含命令行实参的 `string[]` 形参，也可以不具有这样的形参。  使用 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 创建 Windows 窗体应用程序时，可以手动添加形参，也可以使用 <xref:System.Environment> 类获取命令行实参。  形参读取为零索引的命令行参数。与 C 和 C\+\+ 不同，程序的名称视为第一个命令行参数。  
  
## 本节内容  
  
-   [命令行参数](../../../csharp/programming-guide/main-and-command-args/command-line-arguments.md)  
  
-   [如何：显示命令行参数](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)  
  
-   [如何：使用 foreach 访问命令行参数](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)  
  
-   [Main\(\) 返回值](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [Command\-line Building With csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [在 C\# 程序内部](../../../csharp/programming-guide/inside-a-program/index.md)   
 [\<paveover\>C\# Sample Applications](http://msdn.microsoft.com/zh-cn/9a9d7aaa-51d3-4224-b564-95409b0f3e15)