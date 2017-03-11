---
title: "演练：在 Visual Basic 中实现 IEnumerable(Of T) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "控制流"
  - "控制流 [Visual Basic]"
  - "可枚举接口"
  - "循环结构, 优化性能"
ms.assetid: c60d7589-51f2-4463-a2d5-22506bbc1554
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# 演练：在 Visual Basic 中实现 IEnumerable(Of T)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

<xref:System.Collections.Generic.IEnumerable%601> 接口由可以以一次一项的方式返回值序列的类实现。  一次返回一项数据的好处在于，无需将整个数据集加载到内存中进行处理。  而只需为加载的单个数据项提供足够的内存。  实现 `IEnumerable(T)` 接口的类可用在 `For Each` 循环或 LINQ 查询中。  
  
 例如，假设应用程序必须读取一个大型文本文件，并从该文件中返回符合特定搜索条件的每一行。  应用程序使用 LINQ 查询从该文件中返回符合指定条件的行。  若要使用 LINQ 查询来查询文件的内容，应用程序可以将文件的内容加载到一个数组或集合中。  但是，将整个文件加载到数组或集合会占用太多不必要的内存。  LINQ 查询可以改为使用可枚举类来查询文件内容，仅返回符合搜索条件的值。  仅返回一些匹配值的查询所占用的内存将会少得多。  
  
 可以创建实现 <xref:System.Collections.Generic.IEnumerable%601> 接口的类将源数据公开为可枚举数据。  实现 `IEnumerable(T)` 接口的类需要另一个实现 <xref:System.Collections.Generic.IEnumerator%601> 接口的类，以便循环访问源数据。  使用这两个类，可以按顺序以特定类型的形式返回数据项。  
  
 在本演练中，将创建一个实现 `IEnumerable(Of String)` 接口的类以及一个实现 `IEnumerator(Of String)` 接口的类，以便一次从文本文件中读取一行。  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
## 创建可枚举类  
  
||  
|-|  
|创建可枚举类项目|  
|1.  在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的**“文件”**菜单上，指向**“新建”**，然后单击**“项目”**。<br />2.  在**“新建项目”**对话框的**“项目类型”**窗格中，确保选中**“Windows”**。  在**“模板”**窗格中，选择**“类库”**。  在**“名称”**框中键入 `StreamReaderEnumerable`，然后单击**“确定”**。  将显示新项目。<br />3.  在**“解决方案资源管理器”**中右击 Class1.vb 文件，然后选择**“重命名”**。  将该文件重命名为 `StreamReaderEnumerable.vb`，然后按 Enter。  重命名该文件后，会相应地将类重命名为 `StreamReaderEnumerable`。  此类将实现 `IEnumerable(Of String)` 接口。<br />4.  右击 StreamReaderEnumerable 项目，指向**“添加”**，然后单击**“新建项”**。  选择**“类”**模板。  在**“名称”**框中键入 `StreamReaderEnumerator.vb`，然后单击**“确定”**。|  
  
 此项目中的第一个类是可枚举类，该类将实现 `IEnumerable(Of String)` 接口。  此泛型接口实现 <xref:System.Collections.IEnumerable> 接口，并保证此类的使用方可以访问类型化为 `String` 的值。  
  
||  
|-|  
|添加用于实现 IEnumerable 的代码|  
|1.  打开 StreamReaderEnumerable.vb 文件。<br />2.  在 `Public Class StreamReaderEnumerable` 后面的行上键入以下内容，然后按 Enter。<br />     [!code-vb[VbVbalrIteratorWalkthrough#1](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/visualbasic/VbVbalrIteratorWalkthrough/StreamReaderIterator.vb#1)]<br />     [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 自动用 `IEnumerable(Of String)` 接口所需的成员填充该类。<br />3.  此可枚举类将以一次一行的方式读取文本文件中的行。  向该类中添加以下代码，以便公开以文件路径作为输入参数的公共构造函数。<br />     [!code-vb[VbVbalrIteratorWalkthrough#2](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/visualbasic/VbVbalrIteratorWalkthrough/StreamReaderIterator.vb#2)]<br />4.  `IEnumerable(Of String)` 接口的 <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 方法实现将返回 `StreamReaderEnumerator` 类的新实例。  `IEnumerable` 接口的 `GetEnumerator` 方法实现可以设置为 `Private`，因为只需公开 `IEnumerable(Of String)` 接口的成员。  用以下代码替换 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 为 `GetEnumerator` 方法生成的代码。<br />     [!code-vb[VbVbalrIteratorWalkthrough#3](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/visualbasic/VbVbalrIteratorWalkthrough/StreamReaderIterator.vb#3)]|  
  
||  
|-|  
|添加用于实现 IEnumerator 的代码|  
|1.  打开 StreamReaderEnumerator.vb 文件。<br />2.  在 `Public Class StreamReaderEnumerator` 后面的行上键入以下内容，然后按 Enter。<br />     [!code-vb[VbVbalrIteratorWalkthrough#4](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/visualbasic/VbVbalrIteratorWalkthrough/StreamReaderIterator.vb#4)]<br />     [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 自动用 `IEnumerator(Of String)` 接口所需的成员填充该类。<br />3.  枚举器类打开文本文件，执行文件 I\/O 从该文件读取行。  向该类添加以下代码，以便公开以文件路径作为输入参数的公共构造函数，并打开文本文件进行读取。<br />     [!code-vb[VbVbalrIteratorWalkthrough#5](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/visualbasic/VbVbalrIteratorWalkthrough/StreamReaderIterator.vb#5)]<br />4.  `IEnumerator(Of String)` 和 `IEnumerator` 接口的 `Current` 属性都以 `String` 的形式返回文本文件的当前项。  `IEnumerator` 接口的 `Current` 属性实现可以设置为 `Private`，因为只需公开 `IEnumerator(Of String)` 接口的成员。  用以下代码替换 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 为 `Current` 属性生成的代码。<br />     [!code-vb[VbVbalrIteratorWalkthrough#6](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/visualbasic/VbVbalrIteratorWalkthrough/StreamReaderIterator.vb#6)]<br />5.  `IEnumerator` 接口的 `MoveNext` 方法定位到文本文件的下一项并更新 `Current` 属性所返回的值。  如果不再有要读取的项，则 `MoveNext` 方法返回 `False`；否则，`MoveNext` 方法返回 `True`。  将以下代码添加到 `MoveNext` 方法中。<br />     [!code-vb[VbVbalrIteratorWalkthrough#7](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/visualbasic/VbVbalrIteratorWalkthrough/StreamReaderIterator.vb#7)]<br />6.  `IEnumerator` 接口的 `Reset` 方法指示迭代器指向文本文件的开头并清除当前项的值。  将以下代码添加到 `Reset` 方法中。<br />     [!code-vb[VbVbalrIteratorWalkthrough#8](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/visualbasic/VbVbalrIteratorWalkthrough/StreamReaderIterator.vb#8)]<br />7.  `IEnumerator` 接口的 `Dispose` 方法保证在销毁迭代器之前释放所有非托管资源。  `StreamReader` 对象所用的文件句柄是非托管资源，必须在迭代器实例销毁之前关闭。  用以下代码替换 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 为 `Dispose` 方法生成的代码。<br />     [!code-vb[VbVbalrIteratorWalkthrough#9](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/visualbasic/VbVbalrIteratorWalkthrough/StreamReaderIterator.vb#9)]|  
  
## 使用示例迭代器  
 您可以在代码中将可枚举类用在需要实现 `IEnumerable` 的对象的控制结构中（如 `For Next` 循环或 LINQ 查询）。  下面的示例演示 LINQ 查询中的 `StreamReaderEnumerable`。  
  
 [!code-vb[VbVbalrIteratorWalkthrough#10](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/visualbasic/VbVbalrIteratorWalkthrough/Module1.vb#10)]  
  
## 请参阅  
 [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [控制流](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [循环结构](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [For Each...Next 语句](../../../../visual-basic/language-reference/statements/for-each-next-statement.md)