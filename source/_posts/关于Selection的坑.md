---
title: 关于UnityEditor.Selection的坑
date: 2020-04-05 15:38:19
categories: Unity
tags: [Unity,UnityEditor,Editor]
---

# 问题介绍
在使用UnityEditor.Selection.objects的时候在Project面板的双栏布局下的左侧面板中选中文件夹，会出现明明已经选中了，但是Selection.objects得到的是空的。

![](/images/postsimages/Unity/Selection/Selection双栏布局选中.png)

# 解决方法

经过调试发现使用Selection.assetGUIDs可以兼容这种情况

```csharp
foreach (var obj in Selection.assetGUIDs)
{
    string path = AssetDatabase.GUIDToAssetPath(obj);
    //如果是文件夹才处理
    if (Directory.Exists(path))
    {
        var characterName = Path.GetFileName(path).ToLower();
        animatorGenerator.GenerateController(path, characterName);
    }
}
```


