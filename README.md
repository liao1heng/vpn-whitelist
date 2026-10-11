# VPN 基础白名单

基础列表：[whitelist.txt](whitelist.txt)。客户端固定读取 `https://raw.githubusercontent.com/liao1heng/vpn-whitelist/main/whitelist.txt`，后台启动或手动重载时更新。

- 一行一条；空行忽略。
- 含 `#` 的整行不加载，可在行首加 `#` 禁用规则。
- `example.com` 精确匹配；`*.example.com` 匹配本域及子域。
- IPv4地址（如`8.8.8.8`）与CIDR网段（如`142.250.0.0/15`）可和域名混写，一行一条。单IP等价于/32，网段规范化后去重。需要升级支持网段的客户端；旧版会保留上次有效缓存。
- 基础列表保留 `ifconfig.me`，并包含从旧 VPN 同步的 Google、YouTube、GitHub、OpenAI 及 `ip.cn` 显式域名。本机追加规则写入 `whitelist.custom.txt`，与基础列表合并去重；自定义不能删除基础规则。
- GitHub 读取失败时客户端沿用有效缓存；修改后在客户端重载 TXT。

此仓库仅存公开白名单，不保存服务器账号、设备凭据或私钥。IPv6仍全局禁用，不接受IPv6规则；默认全网段、本机和隧道保留网段不可加入。

## 旧 VPN 同步记录

2026-10-11 从本机 `vpn` 命令实际调用的运行脚本提取 `DNS_FIX_DOMAINS` 中全部 19 个域名，另加入旧 `whitelist.json` 路由分组明确标注的 `ip.cn`。保留原有 `ifconfig.me`，去重后共 21 条精确域名规则；没有自动扩展为通配符。

随后按用户要求增加IPv4/CIDR支持，并同步旧 `whitelist.json` 全部34条IP/网段规则，当前共55条。网段会覆盖范围内全部目标（包括共享CDN站点和明确列出的DNS地址），不再局限于单个域名；未自动增加其他网段。客户端断开时保留网段失败屏障，升级前的旧客户端不会加载这些新增网段。
