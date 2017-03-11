---
title: "在命令行上使用 csc.exe 生成 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "生成 [C#]"
  - "命令行 [C#]"
ms.assetid: 66e70056-dd20-453c-a9b3-507e0478b015
caps.latest.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 28
---
# 在命令行上使用 csc.exe 生成
通过在命令提示符处键入 C# 编译器的可执行文件名称 (csc.exe)，可调用该编译器。  
  
 如果您使用 **Visual Studio 命令提示符** 窗口中，为您设置所有必要的环境变量。 在 Windows 7 中，您可以访问该窗口 **启动** 菜单上，通过打开 Microsoft Visual Studio *版本*\Visual Studio Tools 文件夹。 在 Windows 8 中，Visual Studio 命令提示符称为 **VS2012 的开发人员命令提示**, ，并且可以从开始屏幕中搜索找到它。  
  
 如果使用标准命令提示符窗口，则必须调整路径，然后才能从计算机的任意子目录调用 csc.exe。 您还必须运行 vsvars32.bat 来设置适当的环境变量以支持命令行生成操作。 有关 vsvars32.bat，包括有关如何查找并运行它，说明的详细信息请参阅 [如何︰ 设置环境变量的 Visual Studio 命令行](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)。  
  
 如果您只有一台计算机上使用 [!INCLUDE[winsdklong](../../../csharp/language-reference/compiler-options/includes/winsdklong-md.md)], ，则可以使用 C# 编译器在 **SDK 命令提示**, ，打开 **Microsoft.NET Framework SDK** 菜单选项。  
  
 也可以使用 MSBuild 以编程方式生成 C# 程序。 有关详细信息，请参阅 [MSBuild](/visual-studio/msbuild/msbuild1)。  
  
 Csc.exe 可执行文件通常位于 microsoft.net \framework\\*版本* Windows 目录下的文件夹。 根据每台计算机上的具体配置，此位置可能有所不同。 如果计算机上安装了不止一个版本的 .NET Framework，您将发现此文件的多个版本。 有关此类安装的详细信息，请参阅 [确定哪个版本的.NET Framework 是安装](http://msdn.microsoft.com/zh-cn/1a87cc6a-1c4b-4c38-b878-faa9b3beae3c)。  
  
> [!TIP]
>  通过使用 Visual Studio IDE 生成项目时，可以显示 **csc** 命令，并在其关联的编译器选项 **输出** 窗口。 若要显示此信息，请按照中的说明 [How to︰ 视图中，保存和配置生成日志文件](../Topic/How%20to:%20View,%20Save,%20and%20Configure%20Build%20Log%20Files.md) 若要更改的日志数据的详细信息级别 **正常** 或 **详细**。 重新生成项目后，搜索 **输出** 窗口 **csc** 即可找到所调用的 C# 编译器。  
  
 **本主题中**  
  
-   [命令行语法规则](#vcconcommand-linebuildinganchor1)  
  
-   [示例命令行](#vcconcommand-linebuildinganchor2)  
  
-   [C# 编译器和 c + + 编译器输出之间的差异](#vcconcommand-linebuildinganchor3)  
  
##  <a name="a-namevcconcommand-linebuildinganchor1a-rules-for-command-line-syntax-for-the-c-compiler"></a><a name="vcconcommand-linebuildinganchor1"></a> 对于 C# 编译器的命令行语法规则  
 在解释操作系统命令行上给出的参数时，C# 编译器使用以下规则︰  
  
-   参数用空白分隔，空白可以是一个空格或制表符。  
  
-   插入符号 (^) 未被识别为转义符或者分隔符。 在传递给程序中的 argv 数组之前，该字符是由操作系统中的命令行分析器处理。  
  
-   括在双引号 ("string") 的字符串解释为单个参数，无论其中包含在内的空白。 带引号的字符串可以嵌入在自变量内。  
  
-   双精度的引号前面加上反斜杠 (\\") 被解释为原义双引号字符 （"）。  
  
-   反斜杠按其原义解释，除非它们紧位于双引号之前。  
  
-   如果偶数个反斜杠后跟双引号，每对反斜杠，argv 数组中放置一个反斜杠，双引号被解释为字符串分隔符。  
  
-   如果奇数个反斜杠后跟双引号，一个反斜杠放置在每对反斜杠，argv 数组中且双引号字符"转义"由剩余的反斜杠。 这将导致义双引号字符 （"） 添加到 argv 中。  
  
##  <a name="a-namevcconcommand-linebuildinganchor2a-sample-command-lines-for-the-c-compiler"></a><a name="vcconcommand-linebuildinganchor2"></a> C# 编译器的示例命令行  
  
-   编译生成 File.exe File.cs:  
  
    ```  
    csc File.cs   
    ```  
  
-   编译生成 File.dll File.cs:  
  
    ```  
    csc /target:library File.cs  
    ```  
  
-   编译 File.cs 并创建 My.exe:  
  
    ```  
    csc /out:My.exe File.cs  
    ```  
  
-   定义 DEBUG 符号和编译所有 C# 文件在当前目录中，进行了优化。 输出为 File2.exe:  
  
    ```  
    csc /define:DEBUG /optimize /out:File2.exe *.cs  
    ```  
  
-   编译所有 C# 中的文件生成 File2.dll 的调试版本的当前目录。 显示没有徽标和警告︰  
  
    ```  
    csc /target:library /out:File2.dll /warn:0 /nologo /debug *.cs  
    ```  
  
-   编译所有 C# 文件 Something.xyz (DLL) 到当前目录中︰  
  
    ```  
    csc /target:library /out:Something.xyz *.cs  
    ```  
  
##  <a name="a-namevcconcommand-linebuildinganchor3a-differences-between-c-compiler-and-c-compiler-output"></a><a name="vcconcommand-linebuildinganchor3"></a> C# 编译器和 c + + 编译器输出之间的差异  
 调用 C# 编译器时，不会创建任何对象 (.obj) 文件，而是直接创建输出文件。 因此，C# 编译器不需要链接器。  
  
## <a name="see-also"></a>另请参阅  
 [C# 编译器选项](../../../csharp/language-reference/compiler-options/index.md)   
 [按字母顺序列出的 C# 编译器选项](../../../csharp/language-reference/compiler-options/listed-alphabetically.md)   
 [按类别列出的 C# 编译器选项](../../../csharp/language-reference/compiler-options/listed-by-category.md)   
 [Main （） 和命令行参数](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md)   
 [命令行参数](../../../csharp/programming-guide/main-and-command-args/command-line-arguments.md)   
 [如何︰ 显示命令行参数](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)   
 [如何︰ 访问命令行参数使用 foreach](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)   
 [Main （） 返回值](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)