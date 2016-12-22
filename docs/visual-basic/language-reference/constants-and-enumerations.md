---
title: "常量和枚举 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "常量"
  - "常量, 列表"
  - "枚举 [Visual Basic]"
ms.assetid: 309c0ad5-83e4-4f96-99ea-83cd95107417
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 常量和枚举 (Visual Basic)
[!INCLUDE[vs2017banner](../../csharp/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 为开发人员提供许多预定义的常量和枚举。  常数存储那些在整个应用程序的执行过程中保持不变的值。  枚举提供一种使用成组的相关常数以及将常数值与名称相关联的方便途径。  
  
## 常量  
  
### 条件编译常数  
 下表列出了可用于条件编译的预定义常数。  
  
|||  
|-|-|  
|**常量**|**说明**|  
|`CONFIG`|一个字符串，与**“配置管理器”**中的**“活动的解决方案配置”**框的当前设置相对应。|  
|`DEBUG`|可以在**“项目属性”**对话框中设置的 `Boolean` 值。  默认情况下，项目的“调试”配置定义 `DEBUG`。  如果定义了 `DEBUG`，则 <xref:System.Diagnostics.Debug> 类方法会将生成的输出结果显示在**“输出”**窗口中。  如果未定义该值，则不会编译 <xref:System.Diagnostics.Debug> 类方法，也不会生成调试输出。|  
|`TARGET`|一个字符串，表示项目的输出类型或命令行 **\/target** 选项的设置。  `TARGET` 的可能值是：<br /><br /> -   "winexe"（对于 Windows 应用程序）。<br />-   "exe"（对于控制台应用程序）。<br />-   "library"（对于类库）。<br />-   "module"（对于模块）。<br />-   在 [!INCLUDE[vsprvs](../../csharp/includes/vsprvs_md.md)] 集成开发环境中可以设置 **\/target** 选项。  有关更多信息，请参见 [\/target](../../visual-basic/reference/command-line-compiler/target.md)。|  
|`TRACE`|可以在**“项目属性”**对话框中设置的 `Boolean` 值。  默认情况下，项目的所有配置都定义 `TRACE`。  如果定义了 `TRACE`，则 <xref:System.Diagnostics.Trace> 类方法会将生成的输出结果显示在**“输出”**窗口中。  如果未定义该值，则不会编译 <xref:System.Diagnostics.Trace> 类方法，也不会生成任何 `Trace` 输出。|  
|`VBC_VER`|以 *major*.*minor* 格式表示 [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 版本的数字。  [!INCLUDE[vbprvblong](../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)] 的版本号为 8.0。|  
  
### 输出和显示常数  
 当调用输出和显示函数时，可以在代码中使用下列常数来代替实际值。  
  
|||  
|-|-|  
|**常量**|**说明**|  
|`vbCrLf`|回车\/换行组合符。|  
|`vbCr`|回车符。|  
|`vbLf`|换行符。|  
|`vbNewLine`|换行符。|  
|`vbNullChar`|null 字符。|  
|`vbNullString`|与零长度字符串 \(""\) 不同；用于调用外部过程。|  
|`vbObjectError`|错误号。  用户定义的错误号应当大于此值。  例如：<br /><br /> `Err.Raise(Number) = vbObjectError + 1000`|  
|`vbTab`|Tab 字符。|  
|`vbBack`|退格字符。|  
|`vbFormFeed`|在 Microsoft Windows 中不使用。|  
|`vbVerticalTab`|在 Microsoft Windows 中无用。|  
  
## 枚举  
 下表列出并描述了由 [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 提供的枚举。  
  
|||  
|-|-|  
|Enumeration|说明|  
|<xref:Microsoft.VisualBasic.AppWinStyle>|指示在调用 <xref:Microsoft.VisualBasic.Interaction.Shell%2A> 函数时用于被调用程序的窗口样式。|  
|<xref:Microsoft.VisualBasic.AudioPlayMode>|指示在调用音频方法时如何播放声音。|  
|<xref:Microsoft.VisualBasic.ApplicationServices.BuiltInRole>|指示在调用 <xref:Microsoft.VisualBasic.ApplicationServices.User.IsInRole%2A> 方法时检查的角色类型。|  
|<xref:Microsoft.VisualBasic.CallType>|指示在调用 <xref:Microsoft.VisualBasic.Interaction.CallByName%2A> 函数时调用的过程类型。|  
|<xref:Microsoft.VisualBasic.CompareMethod>|指示当调用比较函数时如何比较字符串。|  
|<xref:Microsoft.VisualBasic.DateFormat>|指示在调用 <xref:Microsoft.VisualBasic.Strings.FormatDateTime%2A> 函数时如何显示日期。|  
|<xref:Microsoft.VisualBasic.DateInterval>|指示在调用与日期相关的函数时如何确定日期间隔和设置日期间隔的格式。|  
|<xref:Microsoft.VisualBasic.FileIO.DeleteDirectoryOption>|指定当要删除的目录中含有文件或目录时应采取的操作。|  
|<xref:Microsoft.VisualBasic.DueDate>|指示在调用财务方法时付款何时到期。|  
|<xref:Microsoft.VisualBasic.FileIO.FieldType>|指示文本字段是分隔的还是固定宽度的。|  
|<xref:Microsoft.VisualBasic.FileAttribute>|指示当调用文件访问函数时要使用的文件特性。|  
|<xref:Microsoft.VisualBasic.FirstDayOfWeek>|指示在调用与日期相关的函数时使用的每周的第一天。|  
|<xref:Microsoft.VisualBasic.FirstWeekOfYear>|指示在调用与日期相关的函数时使用的每年的第一周。|  
|<xref:Microsoft.VisualBasic.MsgBoxResult>|指示在 <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> 函数返回的消息框上所按的按钮。|  
|<xref:Microsoft.VisualBasic.MsgBoxStyle>|指示在调用 <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> 函数时要显示的按钮。|  
|<xref:Microsoft.VisualBasic.OpenAccess>|指示调用文件访问函数时如何打开文件。|  
|<xref:Microsoft.VisualBasic.OpenMode>|指示调用文件访问函数时如何打开文件。|  
|<xref:Microsoft.VisualBasic.OpenShare>|指示调用文件访问函数时如何打开文件。|  
|<xref:Microsoft.VisualBasic.FileIO.RecycleOption>|指定文件是应永久删除还是放入“回收站”中。|  
|<xref:Microsoft.VisualBasic.FileIO.SearchOption>|指定是搜索所有目录还是仅搜索顶级目录。|  
|<xref:Microsoft.VisualBasic.TriState>|指示 `Boolean` 值或在调用数字格式的函数时是否应使用默认值。|  
|<xref:Microsoft.VisualBasic.FileIO.UICancelOption>|指定当用户在操作中单击**“取消”**时应采取的操作。|  
|<xref:Microsoft.VisualBasic.FileIO.UIOption>|指定在复制、删除或移动文件或目录时是否显示进度对话框。|  
|<xref:Microsoft.VisualBasic.VariantType>|指示由 <xref:Microsoft.VisualBasic.Information.VarType%2A> 函数返回的变量对象的类型。|  
|<xref:Microsoft.VisualBasic.VbStrConv>|指示在调用 <xref:Microsoft.VisualBasic.Strings.StrConv%2A> 函数时要执行哪种类型的转换。|  
  
## 请参阅  
 [Visual Basic 语言参考](../../visual-basic/language-reference/index.md)   
 [Visual Basic](../../visual-basic/index.md)   
 [常量概述](../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [枚举概述](../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)