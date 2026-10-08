# AB Unlock Code（网页版）

根据设备的 MAC 地址和序列号（SN）计算小米设备解锁码的网页工具。

本项目是 AstroBox NG 插件 [ab-unlockcode](https://github.com/leset0ng/ab-unlockcode) 的网页移植版，算法与界面逻辑和原插件完全一致。

## 原项目

- 地址：<https://github.com/leset0ng/ab-unlockcode>
- 原项目为 AstroBox NG 插件（Rust 编写），本仓库仅含与其功能对等的单文件网页实现。

## 使用方法

直接用浏览器打开 `index.html` 即可，无需联网、无需部署、纯本地计算：

1. 输入 MAC 地址（例如 `00:11:22:33:44:55`）
2. 输入序列号 SN（例如 `SN123456789`）
3. S5 / 10P 及以后设备请打开「新版算法」开关
4. 点击「计算解锁码」

也可将 `index.html` 部署到任意静态托管（GitHub Pages、Cloudflare Pages 等）在线使用。

## 算法

```text
unlock_code = SHA256(upper(去分隔符的 MAC) + upper(SN) + "XIAOMI")
code = 前 10 个字节分别对 0xA 取模后拼接成的 10 位数字
```

- 新版算法将拼接顺序换为 `SN + MAC + "XIAOMI"`，适用于 S5 / 10P 及以后设备。
- MAC 输入会自动去除 `:`、`：`（中文冒号）、`-`、空格、`.` 等分隔符，并转换为大写；SN 会去除首尾空格并转换为大写。

## 一致性

网页版的计算逻辑已对照原插件的 Rust 实现逐一校验，相同输入下输出逐位一致。
