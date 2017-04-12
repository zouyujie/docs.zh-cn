---
title: "如何︰ 将 LINQ 查询与正则表达式 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 3da1bd10-b0d8-4d5b-a637-966891c13592
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
ms.openlocfilehash: 283b5e844c91da22aadd7bcf88ea327ccc080be7
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-combine-linq-queries-with-regular-expressions-visual-basic"></a>如何︰ 将 LINQ 查询与正则表达式 (Visual Basic)
此示例演示如何使用<xref:System.Text.RegularExpressions.Regex>类来创建更复杂的文本字符串中匹配的正则表达式。</xref:System.Text.RegularExpressions.Regex> LINQ 查询轻松设置筛选器的完全您要搜索的正则表达式，并对结果进行加工的文件。  
  
## <a name="example"></a>示例  
  
```vb  
Class LinqRegExVB  
  
    Shared Sub Main()  
  
        ' Root folder to query, along with all subfolders.  
        ' Modify this path as necessary so that it accesses your Visual Studio folder.  
        Dim startFolder As String = "C:\program files\Microsoft Visual Studio 9.0\"  
        ' One of the following paths may be more appropriate on your computer.  
        'string startFolder = @"c:\program files (x86)\Microsoft Visual Studio 9.0\";  
        'string startFolder = @"c:\program files\Microsoft Visual Studio 10.0\";  
        'string startFolder = @"c:\program files (x86)\Microsoft Visual Studio 10.0\";  
  
        ' Take a snapshot of the file system.  
        Dim fileList As IEnumerable(Of System.IO.FileInfo) = GetFiles(startFolder)  
  
        ' Create a regular expression to find all things "Visual".  
        Dim searchTerm As System.Text.RegularExpressions.Regex =   
            New System.Text.RegularExpressions.Regex("Visual (Basic|C#|C\+\+|J#|SourceSafe|Studio)")  
  
        ' Search the contents of each .htm file.  
        ' Remove the where clause to find even more matches!  
        ' This query produces a list of files where a match  
        ' was found, and a list of the matches in that file.  
        ' Note: Explicit typing of "Match" in select clause.  
        ' This is required because MatchCollection is not a   
        ' generic IEnumerable collection.  
        Dim queryMatchingFiles = From afile In fileList  
                                Where afile.Extension = ".htm"  
                                Let fileText = System.IO.File.ReadAllText(afile.FullName)  
                                Let matches = searchTerm.Matches(fileText)  
                                Where (matches.Count > 0)  
                                Select Name = afile.FullName,  
                                       Matches = From match As System.Text.RegularExpressions.Match In matches  
                                                 Select match.Value  
  
        ' Execute the query.  
        Console.WriteLine("The term " & searchTerm.ToString() & " was found in:")  
  
        For Each fileMatches In queryMatchingFiles  
            ' Trim the path a bit, then write   
            ' the file name in which a match was found.  
            Dim s = fileMatches.Name.Substring(startFolder.Length - 1)  
            Console.WriteLine(s)  
  
            ' For this file, write out all the matching strings  
            For Each match In fileMatches.Matches  
                Console.WriteLine("  " + match)  
            Next  
        Next  
  
        ' Keep the console window open in debug mode  
        Console.WriteLine("Press any key to exit")  
        Console.ReadKey()  
    End Sub  
  
    ' Function to retrieve a list of files. Note that this is a copy  
    ' of the file information.  
    Shared Function GetFiles(ByVal root As String) As IEnumerable(Of System.IO.FileInfo)  
        Return From file In My.Computer.FileSystem.GetFiles(  
                   root, FileIO.SearchOption.SearchAllSubDirectories, "*.*")   
               Select New System.IO.FileInfo(file)  
    End Function  
  
End Class  
```  
  
 请注意，您还可以查询<xref:System.Text.RegularExpressions.MatchCollection>所返回的对象`RegEx`搜索。</xref:System.Text.RegularExpressions.MatchCollection> 在此示例中只有每个匹配项的值在结果中生成。 但是，还有可能要使用 LINQ 来执行所有类型的筛选、 排序和分组所依据该集合。 因为<xref:System.Text.RegularExpressions.MatchCollection>是非泛型<xref:System.Collections.IEnumerable>集合中，您必须显式声明在查询中的范围变量的类型。</xref:System.Collections.IEnumerable> </xref:System.Text.RegularExpressions.MatchCollection>  
  
## <a name="compiling-the-code"></a>编译代码  
 创建一个面向.NET Framework 版本 3.5 或更高版本对 System.Core.dll 的引用与项目和一个`Imports`System.Linq 命名空间的语句。  
  
## <a name="see-also"></a>另请参阅  
 [LINQ 和字符串 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)   
 [LINQ 和文件目录 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-file-directories.md)
