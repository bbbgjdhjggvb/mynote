#### launch.json
```
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "lldb",
            "request": "launch",
            "name": "Debug",
            "program": "${workspaceFolder}/build/${fileBasenameNoExtension}",
            "args": [],
            "cwd": "${workspaceFolder}",
            "preLaunchTask": "build c++"
        }
    ]
}
```

#### task.json
```
{
    "version": "2.0.0",
    "options": {
        "cwd": "${workspaceFolder}/build",
    },
    "tasks": [
        {
            "type": "shell",
            "label": "cmake",
            "command":"cmake",
            "args": [
                "DCMAKE_EXPORT_COMPILE_COMMANDS=1",
                ".."
            ]
        },
        {
            "label": "make",
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "command":"make",
            "args": [

            ]
        },
        {
            "label": "build c++",
            "dependsOrder": "sequence",
            "dependsOn": [
                "cmake",
                "make"
            ]
        }
    ]
}
```