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

### Sync
```
github vscode_sync tokens
5e4223ea2bda79306336bff91ec48d7211fb9ae9
vscode setting_sync
cbd6ceb4b179735d5ec9155f71faef96
```

### 设置字体
```
settings中设置Editor: Font Family
DejaVu Sans Mono,book
```