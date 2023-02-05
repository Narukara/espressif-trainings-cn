# 项目结构

## esp-rs crates

不像大多数其他嵌入式平台，Espressif 支持 Rust 标准库。其中最值得关注的是，你可以任意使用大小可变的集合，例如 `Vec` 或 `HashMap`，以及基于 `Box` 的通用堆存储。你还可以自由地创建新线程，并使用 `Arc` 和 `Mutex` 等同步原语在它们之间安全地共享数据。尽管如此，内存在嵌入式系统上仍然是一种稀缺资源，因此需要注意不要耗尽它——尤其是，使用线程的代价可能会很高。

Espressif 的开源物联网开发框架 [esp-idf](https://github.com/espressif/esp-idf) 提供了 WiFi、HTTP 客户端/服务器、MQTT、OTA 更新、日志记录等服务。esp-idf 主要是用 C 编写的，因此将它以规范的、分离的 crate 的形式提供给 Rust：

- 一个 `sys` crate 提供了实际的 `unsafe` bindings（[esp-idf-sys](https://github.com/esp-rs/esp-idf-sys)）
- 一个高级的 crate 提供了安全易用的 Rust 抽象（[esp-idf-svc](https://github.com/esp-rs/esp-idf-svc/)）

最后一部分是底层硬件访问，仍以分离的形式提供：

- [esp-idf-hal](https://github.com/esp-rs/esp-idf-hal) 实现了硬件无关的 [embedded-hal](https://github.com/rust-embedded/embedded-hal) traits，例如模数转换、数字 I/O 引脚、SPI 通信。正如它的名字所暗示的，它依赖于 `esp-idf`。
- 如果需要直接操作寄存器，[esp32c3](https://github.com/esp-rs/esp32c3) 提供由 svd2rust 生成的外设访问 crate。

`esp-rs` book 的 [ecosystem 章节](https://esp-rs.github.io/book/overview/using-the-standard-library.html) 提供了更多信息。

### 构建工具链

🔎 作为项目构建的一部分，`esp-idf-sys` 会下载基于 C 的 Espressif 工具链 [esp-idf](https://github.com/espressif/esp-idf)。下载位置是可配置的，为了节省硬盘空间和下载时间，本课程中的所有示例和练习都被设置为使用一个单一的`全局`工具链，安装在 `~/.espressif` 中。 关于其他可选的配置，请参阅 `esp-idf-sys` 的 [README](https://github.com/esp-rs/esp-idf-sys#configuration) 中的 `ESP_IDF_TOOLS_INSTALL_DIR` 参数。

## Package 布局

与使用 `cargo new` 创建的常规 Rust 项目相比，我们还需要一些额外的文件和参数。本课程中的示例和练习都已经配置好，要创建新项目，建议使用基于 [cargo-generate](./03_2_cargo_generate.md) 向导的方法。

🔎 本页的其余部分是可选知识，在你希望更改项目的某些方面时可以派上用场。

### `Cargo.toml`

本课程是围绕 `native` 构建系统编写的。另外也可以使用 `PlatformIO`/`pio`，但目前已弃用。

```toml
[features]
default = ["native"]
native = ["esp-idf-sys/native"]
```

必须设置一些构建依赖项：

```toml
[build-dependencies]
embuild = "0.28"
anyhow = "1"
```

### 额外的配置文件

- `build.rs` - [Cargo 构建脚本](https://doc.rust-lang.org/cargo/reference/build-scripts.html)。这里设置构建所需的环境变量。
- `.cargo/config.toml` - 设置目标架构并控制构建细节。如果有需要的话，可以在此处覆盖 `ESP_IDF_TOOLS_INSTALL_DIR`。
- `sdkconfig.defaults` - 覆盖 `esp-idf` 的特定参数，例如堆栈大小或日志级别。
