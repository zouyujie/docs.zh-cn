# <a name="using-the-preview3-folder-and-sub-folders"></a>使用 preview3 文件夹和子文件夹

此文件夹是匹配“工具”文件夹的顶层节点，但包含 .NET Core 工具预览版 3 发布的增量。

此单独的并行文件夹结构的目的是提供预览版 3 发布相关内容的位置，当在发布站点中提供版本切换时，可以相对容易地将这些内容合并到主结构中。

此节点下的内容应为较小的文档集，表示来自长期支持 (LTS) 发布和最新发布的增量。 

## <a name="structure"></a>结构

有两种情况可以为此发布增添新内容：

* 对现有文档的更改
    - 将现有内容复制到此结构下的并行文件夹中。 进行更改，并将修改后的文件添加到预览版 3 发布的 TOC。
* 新建文档
    - 将新文档放在正确的位置，并将其添加到预览版 3 发布的节点下的 TOC。 

所有当前发布的文件应在主题顶部附近添加以下内容：

[!include[current release track](../includes/warning.md)]

我们创建了一个包含以下语法的代码段：

```markdown
[!include[current release track](../../includes/warning.md)]
```

### <a name="link-instructions"></a>链接说明

在这两种情况下，提供从当前发布到 LTS 页（或父级 index.md）的链接以作导航。
考虑提供从 LTS 页（或父级 index.md）到新的当前发布内容页面的链接。

## <a name="future-considerations"></a>未来的注意事项

最终目标是将不同的发布作为[文档存储库](https://github.com/dotnet/docs)中的分支进行展现。 在支持发布方案之前，我们将对每个当前发布使用不同的顶层文件夹。 

到时，我们可将每个当前发布合并到主 [docs](../docs) 文件夹中，合并 TOC 节点，并作为单独的文档集发布。 可能需要将修改合并到 LTS 版本的文件和当前发布的文件中，但我们应该能够相对容易地找到这些更改。


<!--HONumber=Jan17_HO3-->


