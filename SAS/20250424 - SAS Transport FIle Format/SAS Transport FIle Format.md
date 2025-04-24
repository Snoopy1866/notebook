# XPT V5 vs V8 格式对比

| 对比项目       | V5       | V8         |
| -------------- | -------- | ---------- |
| 变量名长度     | 8 字节   | 32 字节    |
| 变量标签长度   | 40 字符  | 256 字符   |
| 字符型变量长度 | 200 字节 | 32767 字节 |
| 后缀名         | `.xpt`   | `.v8xpt`   |

> [!NOTE]
>
> `.v8xpt` 是 SAS 推荐的命名约定，但不同指导原则对后缀名的要求不同：
>
> - 《药物临床试验数据递交指导原则（试行）》（2020 年 7 月 20 日）要求后缀名统一为 `.xpt`；
> - 《医疗器械临床试验数据递交要求注册审查指导原则（2021 年第 91 号）》没有对后缀名作要求；
> - 《体外诊断试剂临床试验数据递交要求注册审查指导原则》（2021 年第 91 号）没有对后缀名作要求。

# SAS 数据集导出 XPT 文件

```sas
%loc2xpt(filespec = filespec, libref = libref, memlist = memlist, format = format)
```

其中：

- `filespec` 可以是带引号的文件路径，或者一个文件引用 _fileref_
- `format` 指定传输文件的格式，可选 `V5`, `V8`, `AUTO`，当指定 `AUTO` 时，如果数据集不包含超出 `V5` 限制的变量，则导出 `V5` 格式，否则导出 `V8` 或 `V9` 格式。
  > A V5 transport file is written when you specify AUTO and yourdata set contains no long variable names, long labels, or character variables more than 200 bytes. A V8 or V9 transport file is written when you specify AUTO and your data set contains long variable names,long labels, or character variables more than 200 bytes.

> [!NOTE]
>
> `V9 transport file` 是什么？我认为应该和 V8 是一样的，只是在 SAS V9 上生成就叫 V9，在 SAS V8 上生成就叫 V8？

# XPT 文件读取为 SAS 数据集

```sas
%xpt2loc(filespec = filespec, libref = libref, memlist = memlist)
```
