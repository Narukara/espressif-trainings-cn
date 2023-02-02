# 准备工作

本章包含了有关课程材料、所需硬件的信息，以及一个安装指南。

## 我们使用的图标和格式

我们使用图标来标记书中不同种类的信息：
* ✅ 需要采取行动
* ❗️ 警告，需要特别关注的细节
* 🔎 深入某个主题的知识，但您不需要了解这些知识即可继续
* 💬 Descriptions for Accessibility

> 注释示例：像这样的注释包含了有用的信息

## 需要的硬件

- Rust ESP 开发板，可以在 Mouser、Aliexpress 上购买。[完整的供应商名单](https://github.com/esp-rs/esp-rust-board)。
- 用于连接开发板和 PC 的 USB-C 线缆
- 联入互联网的 Wi-Fi 接入点

不需要额外的调试器硬件。

## 确保工作配置
❗️ 自 2022 年 3 月起，我们不会为 MS Windows 提供完整的设置说明。

❗️ 如果您正在参加由 Ferrous Systems 开展的培训，我们强烈建议您至少提前一个工作日按照本章中的说明为培训做好准备。如果您遇到任何问题或需要任何类型的支持，请联系[我们](training@ferrous-systems.com)。

❗️ 如果您正在使用 [ESP32-C3-DevKitC-02](https://docs.espressif.com/projects/esp-idf/en/latest/esp32c3/hw-reference/esp32c3/user-guide-devkitc-02.html)，一些引脚和从机地址会有所不同。这与 [advanced/i2c-sensor-reading/](/advanced/i2c-sensor-reading/solution/src/) 和 [advanced/i2c-driver/](/advanced/i2c-driver/solution/src/) 中的解答有关，其中用于 ESP32-C3-DevKitC-02 的引脚和从机地址已被注释。

## 配套材料

- [官方 esp-rs book](https://esp-rs.github.io/book/introduction.html) 