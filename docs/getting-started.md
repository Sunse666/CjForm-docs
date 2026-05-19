# 快速开始

## 环境要求

- **Windows 10 / 11** 64 位
- **仓颉工具链**（cjc >= 1.0.5）

## 克隆项目

```bash
git clone https://github.com/Sunse666/CjForm.git MyApp
cd MyApp
```

## 运行

```bash
cjpm run
```

你会看到一个控件画廊窗口，展示所有可用控件。

## 项目结构

```
MyApp/
├── src/
│   └── main.cj          # 控件演示入口
├── cjform/              # CJForm 库
│   ├── cjpm.toml
│   └── src/
│       ├── window.cj    # 窗口、事件循环、渲染
│       ├── widget.cj    # Widget 接口
│       ├── canvas.cj    # 绘制抽象
│       ├── ffi_safe.cj  # 安全 FFI 封装
│       ├── focus_manager.cj # Focusable 接口 + 焦点管理
│       ├── theme.cj     # 主题系统
│       ├── style_sheet.cj # 样式表
│       └── ...          # 30+ 控件文件
├── bridge/              # C++ 桥接（9 个模块）
├── bridge.dll           # 预编译桥接 DLL
├── cjpm.toml
└── README.md
```

## 第一个程序

修改 `src/main.cj`：

```cj
package myapp

import cjform.*

main(): Int64 {
    Theme.setCurrent(Theme.dark())

    let win = Window("Hello CJForm", 800, 600)
    win.setBackgroundColor(Theme.colors().bgSecondary)

    let btn = Button("Click Me",
        Position.abs(400.0, 300.0), 120.0, 36.0,
        "Microsoft YaHei", 14.0, SizeScale.scalable(), Anchor.Center,
        ButtonStyle.fromTheme(), { => println("clicked!") })

    // 统一回调 API — 也支持后置设置
    btn.onClick() { println("clicked!") }

    win.addWidget(btn)  // 统一入口替代 addButton / addLabel / addTextBox 等

    win.show()
    win.run()
    Int64(0)
}
```

## 运行示例

```bash
# 控件演示
cjpm run

# 翻牌记忆游戏
cd examples/memory_game
cjpm run
```

## 编译 bridge.dll（可选）

仓库已提供预编译的 `bridge.dll` 及导入库 `libbridge.dll.a`。如需自行编译：

```bash
cd bridge
mkdir build && cd build
cmake .. -G "MinGW Makefiles"
cmake --build . --config Release
cp bridge.dll ../../ && cp libbridge.dll.a ../../
```

需要安装 MinGW-w64 和 CMake。

## 下一步

继续阅读 [基本使用](basics.md) 了解窗口、布局和事件处理。
