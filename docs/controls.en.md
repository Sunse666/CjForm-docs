# Widget Reference

CJForm provides 25+ custom-drawn widgets across categories: basic input, data display, layout containers, and more.

---

## Basic Widgets

### Button

```cj
let btn = Button("Click Me",
    Position.abs(400.0, 300.0), 120.0, 36.0,
    "Microsoft YaHei", 14.0, SizeScale.scalable(), Anchor.Center,
    ButtonStyle.fromTheme(), { => println("clicked!") })

// With StyleSheet
let btn = Button.styled("btn", "Click Me",
    Position.abs(400.0, 300.0), 120.0, 36.0,
    ButtonStyle.fromTheme(), { => println("clicked!") })
```

| Parameter | Type | Description |
|------|------|------|
| `text` | String | Button label |
| `position` | Position | Position |
| `width` | Float32 | Width |
| `height` | Float32 | Height |
| `fontFamily` | String | Font family |
| `fontSize` | Float32 | Font size |
| `sizeScale` | SizeScale | Scale mode |
| `anchor` | Anchor | Anchor point |
| `style` | ButtonStyle | Visual style |
| `onClick` | `() -> Unit` | Click callback |

**ButtonStyle factories:**

| Factory | Description |
|----------|------|
| `ButtonStyle.fromTheme()` | Default theme style (solid fill) |
| `ButtonStyle.outlined()` | Outlined style |
| `ButtonStyle.bordered(width, color)` | Custom border style |
| `ButtonStyle.custom(bg, textColor, borderRadius, borderWidth, borderColor)` | Fully custom |

---

### Label

```cj
let label = Label("Hello World",
    Position.abs(20.0, 40.0), Theme.colors().textPrimary)

// Full signature
let label = Label("Title", pos, color,
    "Microsoft YaHei", 16.0, SizeScale.fixed(), Anchor.CenterLeft)
```

| Method | Description |
|------|------|
| `setText(text)` | Update text dynamically |

---

### TextBox

```cj
let textBox = TextBox(
    Position.abs(0.0, 0.0), 200.0, 28.0,
    "Microsoft YaHei", 14.0, SizeScale.scalable(),
    TextBoxStyle.fromTheme(), "Placeholder...")

// With StyleSheet
let textBox = TextBox.styled("input",
    Position.abs(0.0, 0.0), 200.0, 28.0,
    TextBoxStyle.fromTheme(), "Enter text...")
```

| Method | Description |
|------|------|
| `setPasswordMode(true/false)` | Password mode (shows •••) |
| `setText(text)` | Set text |
| `getText()` | Get text |

---

### TextEdit (Multi-line Editor)

```cj
let editor = TextEdit.styled("input", "Consolas", 14.0, TextEditStyle.fromTheme())
editor.setText("Welcome to CJForm TextEdit!\n\nType here...")
```

Supported features:

| Shortcut | Action |
|--------|------|
| ++ctrl+z++ | Undo |
| ++ctrl+y++ | Redo |
| ++ctrl+a++ | Select All |
| ++ctrl+c++ | Copy |
| ++ctrl+x++ | Cut |
| ++ctrl+v++ | Paste |
| ++home++ / ++end++ | Line start / end |
| ++arrow-left++ ++arrow-right++ ++arrow-up++ ++arrow-down++ | Cursor movement |

---

## Selection Widgets

### CheckBox

```cj
let cb = CheckBox("Enable notifications",
    Position.abs(0.0, 0.0),
    "Microsoft YaHei", 13.0, SizeScale.scalable(),
    CheckBoxStyle.fromTheme(), true)  // true = checked by default

// With StyleSheet
let cb = CheckBox.styled("btn", "Enable notifications",
    Position.abs(0.0, 0.0),
    CheckBoxStyle.fromTheme(), true)
```

---

### RadioButton + RadioGroup

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

### Slider

```cj
let slider = Slider.styled("input",
    Position.abs(0.0, 0.0), 200.0,
    SliderStyle.fromTheme(), 0.0, 100.0, 65.0)
// min=0.0, max=100.0, initial=65.0
```

---

### ToggleSwitch

```cj
let toggle = ToggleSwitch(true, ToggleSwitchStyle.fromTheme())
// true = on by default
```

---

### SpinBox (Number Stepper)

```cj
let spin = SpinBox(0.0, 120.0, 25.0, 1.0, true)
// min=0.0, max=120.0, initial=25.0, step=1.0, integer=true

spin.setOnValueChanged({ v => println("Value: ${v}") })
```

---

### ComboBox

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

### ProgressBar

```cj
ProgressBar(0.0, 100.0, 72.0, ProgressBarStyle.fromTheme())
// min=0.0, max=100.0, current=72.0
```

---

## Layout Containers

### VBox (Vertical Layout)

```cj
let vbox = VBox(spacing, padding)
vbox.add(widget, LayoutParams.fixed(900.0, 24.0))
```

### HBox (Horizontal Layout)

```cj
let hbox = HBox(spacing, padding)
hbox.add(leftPanel, LayoutParams.fixed(420.0, 600.0).withWeight(0.4))
hbox.add(rightPanel, LayoutParams.fill().withWeight(0.6))
```

### GroupBox

```cj
let group = GroupBox("User Settings")
let inner = VBox(8.0, 12.0)
inner.add(label, LayoutParams.fixed(900.0, 28.0))
group.setContent(inner)
```

### SplitPane

```cj
let split = SplitPane(true)  // true = vertical split
split.setLeft(leftPanel)
split.setRight(rightPanel)
```

### ScrollArea

```cj
let scroll = ScrollArea()
let vbox = VBox(10.0, 20.0)
// ... add content to vbox ...
scroll.setContent(vbox)
```

Scrollbars auto-hide and support smooth scrolling.

---

## View Widgets

### ListView

```cj
let listView = ListView(28.0)  // row height
let items = ArrayList<String>()
for (i in 0..200) {
    items.add("Item #${i + 1}")
}
listView.setData(items)
```

---

### TreeView

```cj
let treeView = TreeView()

let root = TreeNode("src/")
root.expanded = true

let child = TreeNode("button.cj")
root.addChild(child)

treeView.addNode(root)
```

| TreeNode property | Type | Description |
|---------------|------|------|
| `text` | String | Node text |
| `expanded` | Bool | Whether expanded |
| `addChild(node)` | — | Add child node |

---

### TableView

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

| TableColumn param | Type | Description |
|------------------|------|------|
| `title` | String | Column header |
| `width` | Float32 | Column width |
| `resizable` | Bool | Whether resizable |
| `sortable` | Bool | Whether sortable |
| `alignment` | Int32 | Alignment (0=left, 1=center, 2=right) |

---

### TabView

```cj
let tabView = TabView()
tabView.addTab("Basic", basicPage)
tabView.addTab("Advanced", advancedPage)
tabView.setLayoutFrame(LayoutFrame(0.0, 70.0, 1050.0, 650.0))
```

---

## Menus & Popups

### MenuBar

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

| MenuItem param | Type | Description |
|---------------|------|------|
| `label` | String | Menu label |
| `action` | `() -> Unit` | Click callback |
| `shortcut` | String | Shortcut hint |
| `enabled` | Bool | Whether enabled |

`MenuItem.separator()` creates a separator line.

---

### ContextMenu

```cj
let menu = ContextMenu()
menu.addItem(MenuItem("Copy", { => copy() }, "Ctrl+C", true))
win.setContextMenu(menu)
```

---

### Popover

Used for creating popup hints or bubble menus.

---

### Tooltip

Tooltips are automatically managed by the system and shown after a hover timeout.

---

## Other Widgets

### Image

```cj
let img = Image("awa.png")
```

---

### Separator

```cj
Separator(true, SeparatorStyle.fromTheme())
// true = horizontal, false = vertical
```

---

### MessageBox

```cj
MessageBox.show("Title", "Message text", MBType.Info)
```

| MBType | Description |
|--------|------|
| `MBType.Info` | Information |
| `MBType.Warning` | Warning |
| `MBType.Error` | Error |
| `MBType.Question` | Question |

---

## Style Struct Quick Reference

All widgets have corresponding Style structs following a unified pattern:

| Widget | Style Struct | `isThemeBased` |
|------|-------------|----------------|
| Button | `ButtonStyle` | Yes |
| Label | Via `Color` param | No |
| TextBox | `TextBoxStyle` | Yes |
| TextEdit | `TextEditStyle` | Yes |
| CheckBox | `CheckBoxStyle` | Yes |
| RadioButton | `RadioButtonStyle` | Yes |
| Slider | `SliderStyle` | Yes |
| ToggleSwitch | `ToggleSwitchStyle` | Yes |
| SpinBox | `SpinBoxStyle` | Yes |
| ComboBox | `ComboBoxStyle` | Yes |
| ProgressBar | `ProgressBarStyle` | Yes |
| TabView | `TabViewStyle` | Yes |
| TableView | `TableViewStyle` | Yes |
| ListView | `ListViewStyle` | Yes |
| TreeView | `TreeViewStyle` | Yes |
| ScrollArea | `ScrollAreaStyle` | Yes |
| GroupBox | `GroupBoxStyle` | Yes |
| SplitPane | `SplitPaneStyle` | Yes |
| MenuBar | `MenuBarStyle` | Yes |
| ContextMenu | `ContextMenuStyle` | Yes |
| Popover | `PopoverStyle` | Yes |
| Separator | `SeparatorStyle` | Yes |

Each Style struct provides a `fromTheme()` static method for the theme default.
