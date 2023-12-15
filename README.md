# libchai: 汉字编码输入方案算法工具集

目前，本仓库试验性地实现了单字、词组的基本指标评测及爬山、退火两种优化算法。

## 使用

压缩包解压后，根目录中有两个文件：`libchai.exe` 是 Windows 系统上的可执行文件，而 `libchai` 是 macOS 系统上的可执行文件，请根据您的系统选用。

### 输入格式解释及示例

压缩包中有以下的示例文件：

- `config.yaml`: 方案文件，由[汉字自动拆分系统](https://chaifen.app/)生成的方案文件；
- `elements.txt`: 拆分表文件，每个字一行，每行的内容依次为汉字、制表符和以空格分隔的；这个文件也可由自动拆分系统生成；
- `assets/character_frequency.txt`：字频文件，每个字一行，每行的内容为以制表符分隔的字和字频；
- `assets/word_frequency.txt`：词频文件，每个字一行，每行的内容为以制表符分隔的词和词频；
- `assets/equivalence.txt`：当量文件，每个按键组合一行，每行的内容为以制表符分隔的按键组合和当量；

### 双击运行

您可以双击您对应平台上的可执行文件，该文件将依次读取上述几个文件，并根据其中的内容执行优化。如要运行您自己的方案，或选用您自己的字词频，替换相应文件即可。

### 命令行运行

若在命令行运行，可指定方案文件和拆分表文件的路径。例如

```bash
./libchai config.yaml -e elements.txt
```

完整的使用说明可用 `./libchai --help` 查看。

## 开发

需要首先运行 `make assets` 下载相关数据资源。然后 `cargo run` 即可编译运行。

## 构建和部署

在任何平台上只需要 `make build` 或者 `cargo build` 即可编译。

在 `.cargo/config` 中有一个 `target.x86_64-pc-windows-gnu` 目标，是给 macOS 交叉编译 Windows 可执行文件用的，如果不做交叉编译或者不是为 Windows 平台编译的话可以忽略。

`make package` 命令在 macOS 上运行的时候可以同时编译当前平台（x86_64 或 arm64）以及 Windows 的可执行文件，并打包为一个 zip 压缩文件，便于发布。
