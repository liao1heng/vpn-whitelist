# VPN 基础白名单

基础列表：[whitelist.txt](whitelist.txt)。客户端固定读取 `https://raw.githubusercontent.com/liao1heng/vpn-whitelist/main/whitelist.txt`，后台启动或手动重载时更新。

- 一行一条；空行忽略。
- 含 `#` 的整行不加载，可在行首加 `#` 禁用规则。
- `example.com` 精确匹配；`*.example.com` 匹配本域及子域。
- 默认只有 `ifconfig.me`。本机追加规则写入 `whitelist.custom.txt`，与基础列表合并去重；自定义不能删除基础规则。
- GitHub 读取失败时客户端沿用有效缓存；修改后在客户端重载 TXT。

此仓库仅存公开域名列表，不保存服务器账号、设备凭据或私钥。
