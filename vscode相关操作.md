vscode相关操作

1.1快捷键

| 快捷键           | 功能               | 快捷键          | 功能             |
| ---------------- | ------------------ | --------------- | ---------------- |
| 'ctrl' + '+/-'   | 放大/缩小          | F1=ctrl+shift+p | vscode extension |
| ctrl+[           | 代码行缩进         | alt+shift+F     | 代码格式化       |
| ctrl+d           | 选中单词           | ctrl+F          | 查找             |
| ctrl+d 、ctrl+F2 | 选中所有，同时修改 |                 |                  |

```js
<!-- 锚点 ：-->
<a href="text1.html#p1">段落1 </a>
<a name="p1">111</a>
```

debug快捷键：

- Continue / Pause F5
- Step Over F10
- Step Into F11
- Step Out Shift+F11
- Restart Ctrl+Shift+F5
- Stop Shift+F5

1.2配置文件

.vscode/launch.json

- type - 调试器类型；
- request - 支持launch(启动)和attach（附加）。它们处理两种不同的工作流和开发人员；
- name - 该调试的名称，可以配置环境的下拉列表里看到；
- program - 启动调试时运行的文件， 即入口文件， 或者程序的可执行命令；
- args - 传递给调试程序的参数，接收数组；
- console - 调试窗口选择调试控制台或者终端，可选值internalConsole（vscode集成的调试控制台），integratedTerminal（vscode 集成终端）， externalTerminal（弹出系统默认终端）

```js
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "type": "chrome",
            "request": "launch",
            "name": "Launch Chrome against localhost",
            "file": "${file}", 
            //"url": "http://localhost:8080",
            // "file":"${workspaceFolder}"
            "webRoot": "${workspaceFolder}"
        },
        {
            "type":"node-terminal",
            "name":"JavaScript Debug Terminal",
            "request":"launch",
            "cwd":"${workspaceFolder}"
        }
    ]
}
```

1.3 vscode编辑器插件

- 代码美化 Beautify

- 代码检查工具 ESLint
- 必备调试工具 Debugger for Chrome
- 万能语言运行环境 Code Runner
- 代码拼写检查 Code Spell Checker

1.4 Visual Studio Debugging Windows: 

- variables
- watch
- call stack
- breakpoints