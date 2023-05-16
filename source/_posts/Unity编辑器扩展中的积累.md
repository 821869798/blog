---
title: Unity编辑器扩展中的积累
date: 2020-05-16 11:38:19
categories: Unity
tags: [Unity,UnityEditor]
---


### 自定义序列化优化，支持为空
> 序列化优化

- 使用SerializeField + Serializable 序列化的自定义对象一定不会为空，并且会把所以属性序列化出来
- 可以SerializeReference + Serializable序列化的方式。
- 使用FindPropertyRelative("xxx").managedReferenceValue = new xxx()的方式初始化
- 可以使用[HideReferenceObjectPicker]来隐藏选择类的下拉框
### Odin自定义序列化无法识别保存的坑
> 使用OdinEditor+OdinValueDrawer扩展Inspector后不识别序列化保存的问题解决办法

```csharp
public override void OnInspectorGUI()
 {
     serializedObject.Update();
     EditorGUI.BeginChangeCheck();

     //自定义代码

     if (EditorGUI.EndChangeCheck())
    {
        Undo.RegisterCompleteObjectUndo(target, "Modify Binding:" + target.name);
        serializedObject.ApplyModifiedProperties();
    }
 }
```

