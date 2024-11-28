>在一千次重新学习如何配置后，决定做个记录

# 使用${workspaceFolder}/.vscode/settings.json
以构建cling时使用的配置为例：
```js
{
    "cmake.sourceDirectory": "${workspaceFolder}/llvm-project/llvm/", // 会作为 -S 参数传递给命令行
    "cmake.buildDirectory": "${workspaceFolder}/cling-build",         // 会作为 -B 参数传递给命令行
    "cmake.configureSettings": {
        // 以 -D${key}=${value} 方式传递给命令行
        "LLVM_TARGETS_TO_BUILD": "host;NVPTX", 
        "LLVM_ENABLE_PROJECTS": "clang",
        "LLVM_EXTERNAL_PROJECTS": "cling",
        "LLVM_EXTERNAL_CLING_SOURCE_DIR": "${workspaceFolder}/cling/",
        "CMAKE_EXPORT_COMPILE_COMMANDS": "ON"
    },
    "cmake.configureArgs": [
        // 也可以直接这里传入
        "-DCMAKE_BUILD_TYPE=Release",
    ],
    "cmake.buildArgs": [
        // --build 时会传入
        "--parallel",
    ],
    "clangd.arguments": [
        // compile_commands.json path:
        "--compile-commands-dir=${workspaceFolder}/cling-build",
    ],
}
```

# 使用${workspaceFolder}/cmakePresets.json
``#TODO``