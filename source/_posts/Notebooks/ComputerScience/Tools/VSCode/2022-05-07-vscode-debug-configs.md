
---
title: VSCode debug配置文件设置
date: 2022-05-07
author: 陌上人如玉
comments:
description:
keywords:
top_img:
cover:
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
tags: 
categories:
  VSCode
---
# 基础设置
## 设置运行目录
```JSON
{
  "cwd": "${workspaceRoot}",   // 工作目录
  "cwd": "${fileDirname}"  // 父目录
}
```
## 设置参数
```json
args=["--do_train","--do_eval"]
```
## 设置环境变量
```json
"env":{ "PYTHONUNBUFFERED":"1", 
        "CUDA_VISIBLE_DEVICES":"5"}
```
# 配置python调试单独文件
可实现类似pycharm中为每个文件定义单独的调试配置
```json
{
            "name": "umtner-MT",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "cwd": "${workspaceFolder}/umtner",
            "console": "integratedTerminal",
            "justMyCode": true,
            "args": ["--do_train","--do_eval", # 设置参数
            "--model_id=2",
            "--dataset_id=0",
            "--num_train_epochs=1"],
            # 设置环境变量
            "env":{ "PYTHONUNBUFFERED":"1", 
                    "CUDA_VISIBLE_DEVICES":"5"}
        }
```
# 配置C++开发环境
## Windows

[参考1](https://www.jianshu.com/p/febbf1e975b6?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation)

[参考2](https://www.cnblogs.com/bpf-1024/p/11597000.html)

- launch.json

```Bash
{
    "version": "0.2.0",
    "configurations": [              
        {
            "name": "C++ Launch (GDB)",                 // 配置名称，将会在启动配置的下拉菜单中显示
            "type": "cppdbg",                           // 配置类型，这里只能为cppdbg
            "request": "launch",                        // 请求配置类型，可以为launch（启动）或attach（附加）
            "launchOptionType": "Local",                // 调试器启动类型，这里只能为Local
            "targetArchitecture": "x86",                // 生成目标架构，一般为x86或x64，可以为x86, arm, arm64, mips, x64, amd64, x86_64
            "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",                   // 将要进行调试的程序的路径
            "miDebuggerPath":"c:\\MinGW64\\bin\\gdb.exe", // miDebugger的路径，注意这里要与MinGw的路径对应
            "args": [],     // 程序调试时传递给程序的命令行参数，一般设为空即可
            "stopAtEntry": false,                       // 设为true时程序将暂停在程序入口处，一般设置为false
            "cwd": "${workspaceRoot}",                  // 调试程序时的工作目录，一般为${workspaceRoot}即代码所在目录
            "externalConsole": true,                    // 调试时是否显示控制台窗口，一般设置为true显示控制台
            "preLaunchTask": "g++"　　                  // 调试会话开始前执行的任务，一般为编译程序，c++为g++, c为gcc
        }
    ]
}
tasks.json

```
- tasks.json

```JSON
{
    "version": "2.0.0",
    "tasks": [
        {
            "type": "shell",
            "label": "g++",
            "command": "C:\\MinGW64\\bin\\g++.exe",
            "args": [
                "-g",
                "${file}",
                "-o",
                "${fileDirname}\\${fileBasenameNoExtension}.exe"
            ],
            "options": {
                "cwd": "C:\\MinGW64\\bin"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": "build"
        }
    ]
}
```

## MacOS(clang++)

[参考](https://juejin.cn/post/6877168348690710535)

- task.json

```JSON
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "clang++ build",
            "command": "clang++",
            "args": [
                "-o",
                "${fileBasenameNoExtension}", // 执行文件名称
                "${fileBasenameNoExtension}.cpp", // 需要执行的源文件
                "-g",
                "-v"
            ],
            "type": "shell",
            "presentation": {
                "echo": true,
                "reveal": "always",
                "panel": "shared"
            },
            "problemMatcher": {
                "owner": "cpp",
                "fileLocation": [
                    "relative",
                    "${workspaceRoot}"
                ],
                "pattern": {
                    "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning|error):\\s+(.*)$",
                    "file": 1,
                    "line": 2,
                    "column": 3,
                    "severity": 4,
                    "message": 5
                }
            }
        }
    ]
}



```
- launch.json

```JSON
{
    "version": "2.0.0",
    "configurations": [
        {
            "name": "C++ Launch",
            "type": "lldb",
            // "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}/${fileBasenameNoExtension}", // main 跟 tasks.json 中的执行文件名称配置一致
            "preLaunchTask": "clang++ build",
            "internalConsoleOptions": "openOnSessionStart",// 不删除，debug时不会自动跳转到terminal
            "logging": {
                "moduleLoad": false,
                "programOutput": true,
                "trace": false
            },
            "showDisplayString": false,
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceRoot}",
            "environment": [],
            "externalConsole": false, // set true to enable keyboard input
            "MIMode": "lldb"
        }
    ]
}



```
- c_cpp_properties.json

不是必须的

```JSON
{
    "configurations": [
        {
            "name": "Mac",
            "includePath": [
                "${workspaceFolder}/**",
                "/Library/Developer/CommandLineTools/usr/include/c++/v1",
                "/usr/local/include",
                "/Library/Developer/CommandLineTools/usr/lib/clang/10.0.0/include", //这里可能需要修改指定的版本
                "/Library/Developer/CommandLineTools/usr/include",
                "/usr/include"
            ],
            "defines": [],
            "macFrameworkPath": [
                "/System/Library/Frameworks",
                "/Library/Frameworks"
            ],
            "compilerPath": "/usr/bin/clang",
            "cStandard": "c11",
            "cppStandard": "c++11",
            "intelliSenseMode": "macos-clang-x64"
        }
    ],
    "version": 4
}
```



## MacOS(简版g++)

- tasks.json

```JSON
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "g++ build",
            "type": "shell",
            "command": "g++",
            "args": [
                "-o",
                "${fileBasenameNoExtension}", // 执行文件名称
                "${fileBasenameNoExtension}.cpp", // 需要执行的源文件
                "-g", //只是编译器，在编译的时候，产生调试信息。
                "-v"     
            ],
        }
    ]
}


```
- launch.json

```JSON
{
    "version": "2.0.0",
    "configurations": [
        {
            "name": "C++ Launch",
            "type": "lldb",
            "request": "launch",
            "program": "${fileDirname}/${fileBasenameNoExtension}", // main 跟 tasks.json 中的执行文件名称配置一致
            "preLaunchTask": "g++ build", //需要和tasks.json文件中的任务名一致
            "targetArchitecture": "x64",                // 生成目标架构，一般为x86或x64，可以为x86, arm, arm64, mips, x64, amd64, x86_64
            "args": [],     // 程序调试时传递给程序的命令行参数，一般设为空即可
            "cwd": "${workspaceRoot}",
            "environment": [],
            "externalConsole": false, // 调试时是否显示控制台窗口，一般设置为true显示控制台
            "MIMode": "lldb"
        }
    ]
}


```


