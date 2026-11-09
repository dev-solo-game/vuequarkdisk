# 夸克网盘 MoviePilot 插件（QuarkSync 稳定架构定制版）

使 MoviePilot 存储原生支持夸克网盘（Quark Pan）。

## 特性与优化亮点

基于官方 `vuequarkdisk` 插件重构，全面对齐 **QuarkSync** 架构：
1. **彻底解除 `x-oss-hash-ctx` 依赖**：去除了旧版安卓协议的哈希寄存器限制，采用官方 PC/Web 桌面端 `aliyun-sdk-js/6.6.1` 规范，杜绝哈希不匹配导致的 OSS 上传失败。
2. **根除 API 频控与 Connection Reset**：采用平滑分片调度与退避重试机制，避免并发高频请求导致被夸克服务端 WAF 发送 TCP RST 切断。
3. **动态分片策略**：大文件自动采用 16MB ~ 32MB 分片，API 调用量减少 80% 以上，显著提升千兆与家庭宽带上传稳定性。
4. **保留 MoviePilot 媒体库闭环**：上传完成自动轮询云盘可见性并获取 `fileid`，无缝衔接刮削与文件入库。

## 安装方法

运行打包脚本生成 ZIP：
```bash
node build-zip.js
```
在 MoviePilot 的【插件】页面点击右上角“手动安装”并上传生成的 `vuequarkdisk.zip` 即可。

## 许可证
MIT
