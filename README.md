# VPN 基础白名单

基础列表：[whitelist.txt](whitelist.txt)。客户端固定读取 `https://raw.githubusercontent.com/liao1heng/vpn-whitelist/main/whitelist.txt`，后台启动或手动重载时更新。

- 一行一条；空行忽略。
- 含 `#` 的整行不加载，可在行首加 `#` 禁用规则。
- `example.com` 精确匹配；`*.example.com` 匹配本域及子域。
- 基础列表保留 `ifconfig.me`，并包含从旧 VPN 同步的 Google、YouTube、GitHub、OpenAI 及 `ip.cn` 显式域名。本机追加规则写入 `whitelist.custom.txt`，与基础列表合并去重；自定义不能删除基础规则。
- GitHub 读取失败时客户端沿用有效缓存；修改后在客户端重载 TXT。

此仓库仅存公开域名列表，不保存服务器账号、设备凭据或私钥。

## 旧 VPN 同步记录

2026-10-11 从本机 `vpn` 命令实际调用的运行脚本提取 `DNS_FIX_DOMAINS` 中全部 19 个域名，另加入旧 `whitelist.json` 路由分组明确标注的 `ip.cn`。保留原有 `ifconfig.me`，去重后共 21 条精确域名规则；没有自动扩展为通配符。

旧 `whitelist.json` 的 34 条规则是 IP 地址或 CIDR 网段，当前客户端 TXT 仅支持域名，不能直接加载这些网段。因此本次同步覆盖全部明确列出的域名，并不等同于复制旧 VPN 的全部 IP 路由覆盖范围；共享 CDN、DNS 地址及仅由网段覆盖的其他站点不因此纳入域名白名单。
