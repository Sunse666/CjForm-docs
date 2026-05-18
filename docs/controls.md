# 控件参考

CJForm 提供 25+ 种自绘控件，涵盖基础输入、数据展示、布局容器等类别。

---

## 基础控件

### Button 按钮

```cj
let btn = Button("Click Me",
    Position.abs(400.0, 300.0), 120.0, 36.0,
    "Microsoft YaHei", 14.0, SizeScale.scalable(), Anchor.Center,
    ButtonStyle.fromTheme(), { => println("clicked!") })

// 使用样式表
let btn = Button.styled("btn", "Click Me",
    Position.abs(400.0, 300.0), 120.0, 36.0,
    ButtonStyle.fromTheme(), { => println("clicked!") })
```

| 参数 | 类型 | 说明 |
|------|------|------|
| `text` | String | 按钮文字 |
| `position` | Position | 位置 |
| `width` | Float32 | 宽度 |
| `height` | Float32 | 高度 |
| `fontFamily` | String | 字体 |
| `fontSize` | Float32 | 字号 |
| `sizeScale` | SizeScale | 缩放模式 |
| `anchor` | Anchor | 锚点 |
| `style` | ButtonStyle | 样式 |
| `onClick` | `() -> Unit` | 点击回调 |

**ButtonStyle：**

| 工厂方法 | 说明 |
|----------|------|
| `ButtonStyle.fromTheme()` | 主题默认样式（实心填充） |
| `ButtonStyle.outlined()` | 描边样式 |
| `ButtonStyle.bordered(width, color)` | 自定义边框样式 |
| `ButtonStyle.custom(bg, textColor, borderRadius, borderWidth, borderColor)` | 完全自定义 |

---

### Label 标签

```cj
let label = Label("Hello World",
    Position.abs(20.0, 40.0), Theme.colors().textPrimary)

// 完整参数
let label = Label("Title", pos, color,
    "Microsoft YaHei", 16.0, SizeScale.fixed(), Anchor.CenterLeft)
```

| 方法 | 说明 |
|------|------|
| `setText(text)` | 动态更新文字 |

---

### TextBox 文本输入

```cj
let textBox = TextBox(
    Position.abs(0.0, 0.0), 200.0, 28.0,
    "Microsoft YaHei", 14.0, SizeScale.scalable(),
    TextBoxStyle.fromTheme(), "Placeholder...")

// 使用样式表
let textBox = TextBox.styled("input",
    Position.abs(0.0, 0.0), 200.0, 28.0,
    TextBoxStyle.fromTheme(), "Enter text...")
```

| 方法 | 说明 |
|------|------|
| `setPasswordMode(true/false)` | 密码模式（显示 •••） |
| `setText(text)` | 设置文本 |
| `getText()` | 获取文本 |

---

### TextEdit 多行编辑器

```cj
let editor = TextEdit.styled("input", "Consolas", 14.0, TextEditStyle.fromTheme())
editor.setText("Welcome to CJForm TextEdit!\n\nType here...")
```

支持功能：

| 快捷键 | 功能 |
|--------|------|
| ++ctrl+z++ | 撤销 |
| ++ctrl+y++ | 重做 |
| ++ctrl+a++ | 全选 |
| ++ctrl+c++ | 复制 |
| ++ctrl+x++ | 剪切 |
| ++ctrl+v++ | 粘贴 |
| ++home++ / ++end++ | 行首 / 行尾 |
| ++arrow-left++ ++arrow-right++ ++arrow-up++ ++arrow-down++ | 光标移动 |

---

## 选择控件

### CheckBox 多选框

```cj
let cb = CheckBox("Enable notifications",
    Position.abs(0.0, 0.0),
    "Microsoft YaHei", 13.0, SizeScale.scalable(),
    CheckBoxStyle.fromTheme(), true)  // true = 默认勾选

// 使用样式表
let cb = CheckBox.styled("btn", "Enable notifications",
    Position.abs(0.0, 0.0),
    CheckBoxStyle.fromTheme(), true)
```

---

### RadioButton + RadioGroup 单选按钮

```cj
let group = RadioGroup()

let rb1 = RadioButton.styled("btn", "Option A",
    Position.abs(0.0, 0.0), RadioButtonStyle.fromTheme())
let rb2 = RadioButton.styled("btn", "Option B",
    Position.abs(0.0, 0.0), RadioButtonStyle.fromTheme())

group.add(rb1)
group.add(rb2)
group.setOnSelectionChanged({ idx =>
    println("Selected: ${idx}")
})
```

---

### Slider 滑块

```cj
let slider = Slider.styled("input",
    Position.abs(0.0, 0.0), 200.0,
    SliderStyle.fromTheme(), 0.0, 100.0, 65.0)
// min=0.0, max=100.0, 初始值=65.0
```

---

### ToggleSwitch 开关

```cj
let toggle = ToggleSwitch(true, ToggleSwitchStyle.fromTheme())
// true = 默认开启
```

---

### SpinBox 数字步进器

```cj
let spin = SpinBox(0.0, 120.0, 25.0, 1.0, true)
// min=0.0, max=120.0, 初始值=25.0, 步长=1.0, 整数模式=true

spin.setOnValueChanged({ v => println("Value: ${v}") })
```

---

### ComboBox 下拉选择

```cj
let combo = ComboBox()
let items = ArrayList<String>()
items.add("Dark Theme")
items.add("Light Theme")
combo.setItems(items)
combo.setLayoutFrame(LayoutFrame(950.0, 36.0, 120.0, 30.0))
combo.setParentWindow(win)
combo.setOnSelectionChanged({ idx, label =>
    println("Selected: ${label}")
})
```

---

### ProgressBar 进度条

```cj
ProgressBar(0.0, 100.0, 72.0, ProgressBarStyle.fromTheme())
// min=0.0, max=100.0, 当前值=72.0
```

---

## 布局容器

### VBox 垂直布局

```cj
let vbox = VBox(spacing, padding)
vbox.add(widget, LayoutParams.fixed(900.0, 24.0))
```

### HBox 水平布局

```cj
let hbox = HBox(spacing, padding)
hbox.add(leftPanel, LayoutParams.fixed(420.0, 600.0).withWeight(0.4))
hbox.add(rightPanel, LayoutParams.fill().withWeight(0.6))
```

### GroupBox 分组框

```cj
let group = GroupBox("User Settings")
let inner = VBox(8.0, 12.0)
inner.add(label, LayoutParams.fixed(900.0, 28.0))
group.setContent(inner)
```

### SplitPane 分割面板

```cj
let split = SplitPane(true)  // true = 垂直分割
split.setLeft(leftPanel)
split.setRight(rightPanel)
```

### ScrollArea 滚动区域

```cj
let scroll = ScrollArea()
let vbox = VBox(10.0, 20.0)
// ... 添加内容到 vbox ...
scroll.setContent(vbox)
```

滚动条自动显隐，支持平滑滚动。

---

## 视图控件

### ListView 列表视图

```cj
let listView = ListView(28.0)  // 行高
let items = ArrayList<String>()
for (i in 0..200) {
    items.add("Item #${i + 1}")
}
listView.setData(items)
```

---

### TreeView 树形视图

```cj
let treeView = TreeView()

let root = TreeNode("src/")
root.expanded = true

let child = TreeNode("button.cj")
root.addChild(child)

treeView.addNode(root)
```

| TreeNode 属性 | 类型 | 说明 |
|---------------|------|------|
| `text` | String | 节点文本 |
| `expanded` | Bool | 是否展开 |
| `addChild(node)` | — | 添加子节点 |

---

### TableView 表格视图

```cj
let tableView = TableView()
tableView.addColumn(TableColumn("#", 50.0, false, false, 1))
tableView.addColumn(TableColumn("Name", 180.0, true, true, 0))

let rowData = ArrayList<ArrayList<String>>()
for (row in data) {
    let row = ArrayList<String>()
    row.add("01")
    row.add("Item")
    rowData.add(row)
}
tableView.setData(rowData)
```

| TableColumn 参数 | 类型 | 说明 |
|------------------|------|------|
| `title` | String | 列标题 |
| `width` | Float32 | 列宽 |
| `resizable` | Bool | 是否可调整宽度 |
| `sortable` | Bool | 是否可排序 |
| `alignment` | Int32 | 对齐（0=左, 1=中, 2=右） |

---

### TabView 标签页

```cj
let tabView = TabView()
tabView.addTab("Basic", basicPage)
tabView.addTab("Advanced", advancedPage)
tabView.setLayoutFrame(LayoutFrame(0.0, 70.0, 1050.0, 650.0))
```

---

## 菜单与弹出

### MenuBar 菜单栏

```cj
let bar = MenuBar()
bar.setParentWindow(win)

let fileMenu = MenuItem("File", { => () })
fileMenu.addChild(MenuItem("New", { => println("New") }, "", true))
fileMenu.addChild(MenuItem("Save", { => println("Save") }, "Ctrl+S", true))
fileMenu.addChild(MenuItem.separator())
fileMenu.addChild(MenuItem("Exit", { => println("Exit") }, "", true))

bar.addItem(fileMenu)
```

| MenuItem 参数 | 类型 | 说明 |
|---------------|------|------|
| `label` | String | 菜单项文字 |
| `action` | `() -> Unit` | 点击回调 |
| `shortcut` | String | 快捷键提示 |
| `enabled` | Bool | 是否可用 |

`MenuItem.separator()` 创建分隔线。

---

### ContextMenu 右键菜单

```cj
let menu = ContextMenu()
menu.addItem(MenuItem("Copy", { => copy() }, "Ctrl+C", true))
win.setContextMenu(menu)
```

---

### Popover 弹出框

用于创建弹出提示或气泡菜单。

---

### Tooltip 工具提示

```cj
// tooltip 由系统自动管理，悬停指定时间后显示
```

---

## 其他控件

### Image 图片

```cj
let img = Image("awa.png")
```

---

### Separator 分隔线

```cj
Separator(true, SeparatorStyle.fromTheme())
// true = 水平线, false = 垂直线
```

---

### MessageBox 消息框

```cj
MessageBox.show("Title", "Message text", MBType.Info)
```

| MBType | 说明 |
|--------|------|
| `MBType.Info` | 信息 |
| `MBType.Warning` | 警告 |
| `MBType.Error` | 错误 |
| `MBType.Question` | 询问 |

---

## 样式结构体速查

所有控件都有对应的 Style 结构体，遵循统一模式：

| 控件 | Style 结构体 | `isThemeBased` |
|------|-------------|----------------|
| Button | `ButtonStyle` | 是 |
| Label | 通过 `Color` 参数 | 否 |
| TextBox | `TextBoxStyle` | 是 |
| TextEdit | `TextEditStyle` | 是 |
| CheckBox | `CheckBoxStyle` | 是 |
| RadioButton | `RadioButtonStyle` | 是 |
| Slider | `SliderStyle` | 是 |
| ToggleSwitch | `ToggleSwitchStyle` | 是 |
| SpinBox | `SpinBoxStyle` | 是 |
| ComboBox | `ComboBoxStyle` | 是 |
| ProgressBar | `ProgressBarStyle` | 是 |
| TabView | `TabViewStyle` | 是 |
| TableView | `TableViewStyle` | 是 |
| ListView | `ListViewStyle` | 是 |
| TreeView | `TreeViewStyle` | 是 |
| ScrollArea | `ScrollAreaStyle` | 是 |
| GroupBox | `GroupBoxStyle` | 是 |
| SplitPane | `SplitPaneStyle` | 是 |
| MenuBar | `MenuBarStyle` | 是 |
| ContextMenu | `ContextMenuStyle` | 是 |
| Popover | `PopoverStyle` | 是 |
| Separator | `SeparatorStyle` | 是 |

每个 Style 结构体均提供 `fromTheme()` 静态方法获取主题默认样式。
