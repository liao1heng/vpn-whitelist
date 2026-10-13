# VPN 基础白名单

基础列表：[whitelist.txt](whitelist.txt)。客户端固定读取 `https://raw.githubusercontent.com/liao1heng/vpn-whitelist/main/whitelist.txt`，后台启动或手动重载时更新。

- 一行一条；空行忽略。
- 含 `#` 的整行不加载，可在行首加 `#` 禁用规则。
- `example.com` 精确匹配；`*.example.com` 匹配本域及子域。
- IPv4地址（如`8.8.8.8`）与CIDR网段（如`142.250.0.0/15`）可和域名混写，一行一条。单IP等价于/32，网段规范化后去重。需要升级支持网段的客户端；旧版会保留上次有效缓存。
- 基础列表保留 `ifconfig.me`，并包含从旧 VPN 同步的 Google、YouTube、GitHub、OpenAI 及 `ip.cn` 显式域名。本机追加规则写入 `whitelist.custom.txt`，与基础列表合并去重；自定义不能删除基础规则。
- 韩国 Google 使用 `*.google.co.kr`，包含 `google.co.kr`、`www.google.co.kr`、`accounts.google.co.kr` 及其他子域名；登录与静态资源继续由已有的 `*.google.com`、`*.googleapis.com`、`*.gstatic.com` 和 `*.googleusercontent.com` 覆盖。更新后在客户端点“重载TXT”，并重新打开原登录页面。
- 按用户提供的Cloud Code/Code Assist请求地址，单独列出`cloudcode-pa.googleapis.com`；该域名同时已由`*.googleapis.com`覆盖。更新后重载TXT并重新启动报错的应用；仅追加域名不能证明连接故障已解决。
- ChatGPT 网页另需 `chatgpt.com`（与旧入口 `chat.openai.com` 不同），以及登录和网页资源域名。新增 `auth.openai.com`、`*.chatgpt.com`、`*.oaistatic.com`、`*.oaiusercontent.com`；通配规则含主域名及子域名。参考 [OpenAI Docs 中列举的 ChatGPT、认证及资源端点](https://learn.chatgpt.com/docs/enterprise/govcloud-configuration)。这是域名分流规则，实际浏览器是否经过本客户端的受管解析仍需在使用端验证。
- Anthropic / Claude 使用官方网络要求中的六组主域名与子域名：`anthropic.com`、`claude.ai`、`claude.com`、`claude.app`、`claudeusercontent.com`、`claudemcpcontent.com`。这里的 `*.example.com` 同时匹配主域名和子域名；第三方登录、插件及外部内容域名需按实际访问补充。来源：[Claude Desktop 网络要求](https://code.claude.com/docs/en/desktop#network-access-requirements)。
- GitHub 读取失败时客户端沿用有效缓存；修改后在客户端重载 TXT。

此仓库仅存公开白名单，不保存服务器账号、设备凭据或私钥。IPv6仍全局禁用，不接受IPv6规则；默认全网段、本机和隧道保留网段不可加入。

## 旧 VPN 同步记录

2026-10-11 从本机 `vpn` 命令实际调用的运行脚本提取 `DNS_FIX_DOMAINS` 中全部 19 个域名，另加入旧 `whitelist.json` 路由分组明确标注的 `ip.cn`。保留原有 `ifconfig.me`，去重后共 21 条精确域名规则；没有自动扩展为通配符。

随后按用户要求增加IPv4/CIDR支持，并同步旧 `whitelist.json` 全部34条IP/网段规则，当时共55条。网段会覆盖范围内全部目标（包括共享CDN站点和明确列出的DNS地址），不再局限于单个域名；未自动增加其他网段。随后新增6条 Anthropic / Claude 规则和4条 ChatGPT 网页规则，当时共65条；补齐Google和登录资源后，2026-10-13加入韩国Google，当前共42条域名、34条IPv4地址/网段，合计76条。客户端主动断开或确认掉线后撤回本项目规则，允许新请求使用原IPv4路径；升级前的旧客户端不会加载新增网段。
