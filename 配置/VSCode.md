[TOC]

### 屏蔽文件
```
settings.json
{
     //-------- Search configuration --------

    // Configure glob patterns for excluding files and folders in searches. Inherits all glob patterns from the files.exclude setting.
    "search.exclude": {
        "**/node_modules": true,
        "**/bower_components": true
    },

    //-------- Files configuration --------

    // Configure glob patterns for excluding files and folders.
    "files.exclude": {
        "**/.git": true,
        "**/.svn": true,
        "**/.DS_Store": true,
        "**/node_modules": true,
        "**/iOS": true
    }
}
```

### 设置Python目录
```
settings.json
"python.pythonPath": "D:\\Anaconda3\\envs\\test\\python.exe"
```


### 设置字体
```
settings中设置Editor: Font Family
DejaVu Sans Mono,book
```