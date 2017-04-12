---
title: "保持 Visual Studio (Visual Basic 中) 中的对象 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: get-started-article
dev_langs:
- VB
ms.assetid: f1d0b562-e349-4dce-ab5f-c05108467030
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0ff6320aee65850b8b445f445f80b4bbe2c9c254
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-persisting-an-object-in-visual-studio-visual-basic"></a>演练︰ 保持在 Visual Studio (Visual Basic 中) 中的对象
虽然可以在设计时对象的属性设置为默认值，但是在运行时输入的所有值都都将丢失时销毁该对象。 您可以使用序列化对象的实例之间保持数据，这样就可以将值存储并实例化该对象在下次检索它们。  
  
> [!NOTE]
>  在 Visual Basic 中，存储简单数据，如名称或编号，您可以使用`My.Settings`对象。 有关详细信息，请参阅[My.Settings 对象](../../../../visual-basic/language-reference/objects/my-settings-object.md)。  
  
 在本演练中，您将创建一个简单`Loan`对象，并将其数据写入文件。 然后重新创建对象时，将从文件中检索数据。  
  
> [!IMPORTANT]
>  此示例创建一个新文件，如果该文件不存在。 如果应用程序必须创建一个文件，该应用程序必须`Create`文件夹的权限。 通过使用访问控制列表设置权限。 如果该文件已存在，该应用程序仅需要`Write`权限时，较小者的权限。 如有可能，会在部署期间，创建该文件，并仅授予更安全`Read`到单个文件 （而不是对文件夹具有创建权限） 的权限。 此外，它是更安全，将数据写入到比到根文件夹或 Program Files 文件夹的用户文件夹。  
  
> [!IMPORTANT]
>  此示例将数据存储二进制文件中。 这些格式不应该用于敏感数据，如密码或信用卡信息。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请单击 **“工具”** 菜单上的 **“导入和导出设置”** 。 有关详细信息，请参阅[在 Visual Studio 中自定义开发设置](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## <a name="creating-the-loan-object"></a>创建贷款对象  
 第一步是创建`Loan`类以及测试应用程序使用的类。  
  
### <a name="to-create-the-loan-class"></a>若要创建 Loan 类  
  
1.  创建一个新的类库项目并将其命名为"LoanClass"。 有关详细信息，请参阅[创建解决方案和项目](http://docs.microsoft.com/visualstudio/ide/creating-solutions-and-projects)。  
  
2.  在**解决方案资源管理器**，打开 Class1 文件的快捷菜单并选择**重命名**。 文件重命名为`Loan`，然后按 enter 键。 重命名该文件也进行重命名为该类`Loan`。  
  
3.  向类中添加以下公共成员︰  
  
    ```vb  
    Public Class Loan  
        Implements System.ComponentModel.INotifyPropertyChanged  
  
        Public Property LoanAmount As Double  
        Public Property InterestRate As Double  
        Public Property Term As Integer  
  
        Private p_Customer As String  
        Public Property Customer As String  
            Get  
                Return p_Customer  
            End Get  
            Set(ByVal value As String)  
                p_Customer = value  
                RaiseEvent PropertyChanged(Me,  
                  New System.ComponentModel.PropertyChangedEventArgs("Customer"))  
            End Set  
        End Property  
  
        Event PropertyChanged As System.ComponentModel.PropertyChangedEventHandler _  
          Implements System.ComponentModel.INotifyPropertyChanged.PropertyChanged  
  
        Public Sub New(ByVal loanAmount As Double,  
                       ByVal interestRate As Double,  
                       ByVal term As Integer,  
                       ByVal customer As String)  
  
            Me.LoanAmount = loanAmount  
            Me.InterestRate = interestRate  
            Me.Term = term  
            p_Customer = customer  
        End Sub  
    End Class  
    ```  
  
 您还需要创建一个简单的应用程序使用`Loan`类。  
  
### <a name="to-create-a-test-application"></a>若要创建的测试应用程序  
  
1.  若要在将 Windows 窗体应用程序项目添加到您的解决方案，**文件**菜单上，选择**添加**，**新项目**。  
  
2.  在**添加新项目**对话框框中，选择**Windows 窗体应用程序**，然后输入`LoanApp`作为名称的项目，然后再单击**确定**以关闭对话框。  
  
3.  在**解决方案资源管理器**，选择 LoanApp 项目。  
  
4.  在**项目**菜单上，选择**设为启动项目**。  
  
5.  在“项目” **** 菜单上，选择“添加引用” ****。  
  
6.  在**添加引用**对话框框中，选择**项目**选项卡，然后选择 LoanClass 项目。  
  
7.  单击“确定” **** 关闭对话框。  
  
8.  在设计器中，添加了四个<xref:System.Windows.Forms.TextBox>控件添加到窗体。</xref:System.Windows.Forms.TextBox>  
  
9. 在代码编辑器中，添加以下代码：  
  
    ```vb  
    Private WithEvents TestLoan As New LoanClass.Loan(10000.0, 0.075, 36, "Neil Black")  
  
    Private Sub Form1_Load() Handles MyBase.Load  
        TextBox1.Text = TestLoan.LoanAmount.ToString  
        TextBox2.Text = TestLoan.InterestRate.ToString  
        TextBox3.Text = TestLoan.Term.ToString  
        TextBox4.Text = TestLoan.Customer  
    End Sub  
    ```  
  
10. 添加事件处理程序`PropertyChanged`事件到该窗体使用下面的代码︰  
  
    ```vb  
    Public Sub CustomerPropertyChanged(  
          ByVal sender As Object,  
          ByVal e As System.ComponentModel.PropertyChangedEventArgs  
        ) Handles TestLoan.PropertyChanged  
  
        MsgBox(e.PropertyName & " has been changed.")  
    End Sub  
    ```  
  
 此时，您可以生成并运行该应用程序。 请注意，默认值从`Loan`类显示在文本框中。 尝试从 7.5 利率值更改为 7.1 中，然后关闭该应用程序并再次运行 — 值会恢复为默认值为 7.5。  
  
 在现实生活中，利率更改定期，但并不一定每次运行该应用程序。 而不是让用户在每次应用程序运行时都更新利率，则最好保持最新的应用程序实例之间的利率。 在下一步，您将执行就是这样通过向贷款类中添加序列化。  
  
## <a name="using-serialization-to-persist-the-object"></a>使用序列化对象进行持久化  
 才能持久地保存贷款类的值，则必须先将标记的类具有`Serializable`属性。  
  
### <a name="to-mark-a-class-as-serializable"></a>若要将标记为可序列化类  
  
-   更改 Loan 类的类声明，如下所示︰  
  
    ```vb  
    <Serializable()>  
    Public Class Loan  
    ```  
  
 `Serializable`特性告知编译器，在类中的所有内容都可以保存到文件。 因为`PropertyChanged`事件处理由 Windows 窗体对象，它不能被序列化。 `NonSerialized`属性可以用来标记不应持久化的类成员。  
  
### <a name="to-prevent-a-member-from-being-serialized"></a>若要防止成员正在序列化  
  
-   更改的声明`PropertyChanged`事件，如下所示︰  
  
    ```vb  
    <NonSerialized()>  
    Event PropertyChanged As System.ComponentModel.PropertyChangedEventHandler _  
      Implements System.ComponentModel.INotifyPropertyChanged.PropertyChanged  
    ```  
  
 下一步是将序列化代码添加到 LoanApp 应用程序。 为了将该类序列化并将其写入到文件，将使用<xref:System.IO>和<xref:System.Xml.Serialization>命名空间。</xref:System.Xml.Serialization> </xref:System.IO> 为了避免键入完全限定的名称，可以添加对必要的类库的引用。  
  
### <a name="to-add-references-to-namespaces"></a>若要添加到命名空间的引用  
  
-   将以下语句添加到顶部`Form1`类︰  
  
    ```vb  
    Imports System.IO  
    Imports System.Runtime.Serialization.Formatters.Binary  
    ```  
  
     在这种情况下，将使用二进制格式化程序将对象保存为二进制格式。  
  
 下一步是添加代码以创建对象时，从该文件对象反序列化。  
  
### <a name="to-deserialize-an-object"></a>反序列化对象  
  
1.  将一个常量添加到序列化的数据文件的名称的类。  
  
    ```vb  
    Const FileName As String = "..\..\SavedLoan.bin"  
    ```  
  
2.  修改中的代码`Form1_Load`事件过程，如下所示︰  
  
    ```vb  
    Private WithEvents TestLoan As New LoanClass.Loan(10000.0, 0.075, 36, "Neil Black")  
  
    Private Sub Form1_Load() Handles MyBase.Load  
        If File.Exists(FileName) Then  
            Dim TestFileStream As Stream = File.OpenRead(FileName)  
            Dim deserializer As New BinaryFormatter  
            TestLoan = CType(deserializer.Deserialize(TestFileStream), LoanClass.Loan)  
            TestFileStream.Close()  
        End If  
  
        AddHandler TestLoan.PropertyChanged, AddressOf Me.CustomerPropertyChanged  
  
        TextBox1.Text = TestLoan.LoanAmount.ToString  
        TextBox2.Text = TestLoan.InterestRate.ToString  
        TextBox3.Text = TestLoan.Term.ToString  
        TextBox4.Text = TestLoan.Customer  
    End Sub  
    ```  
  
     请注意，首先必须检查该文件存在。 如果存在，则创建<xref:System.IO.Stream>类来读取二进制文件和一个<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>类将转换该文件。</xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> </xref:System.IO.Stream> 您还需要从流类型转换为贷款对象类型。  
  
 接下来，您必须添加代码以在文本框中输入的数据保存`Loan`类，并且你必须序列化到文件的类。  
  
### <a name="to-save-the-data-and-serialize-the-class"></a>若要保存的数据和序列化类  
  
-   添加以下代码到`Form1_FormClosing`事件过程︰  
  
    ```vb  
    Private Sub Form1_FormClosing() Handles MyBase.FormClosing  
        TestLoan.LoanAmount = CDbl(TextBox1.Text)  
        TestLoan.InterestRate = CDbl(TextBox2.Text)  
        TestLoan.Term = CInt(TextBox3.Text)  
        TestLoan.Customer = TextBox4.Text  
  
        Dim TestFileStream As Stream = File.Create(FileName)  
        Dim serializer As New BinaryFormatter  
        serializer.Serialize(TestFileStream, TestLoan)  
        TestFileStream.Close()  
    End Sub  
    ```  
  
 此时，您可以再次生成并运行该应用程序。 最初，默认值显示在文本框中。 尝试更改的值并在第四个文本框中输入的名称。 关闭该应用程序，然后再次运行它。 请注意，新值现在显示在文本框中。  
  
## <a name="see-also"></a>另请参阅  
 [序列化 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/index.md)   
 [Visual Basic 编程指南](../../../../visual-basic/programming-guide/index.md)
