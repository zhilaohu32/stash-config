# Stash 配置

主配置配合私密覆写使用。仓库只保存不含真实订阅地址的配置和示例；静态 IP 节点及策略组已移除。

## 导入和更新

1. 复制 `local.example.stoverride`，填写自己的订阅地址，并按需调整订阅集和私人规则。示例地址不能直接使用。
2. 将填写后的文件保存为 GitHub Secret Gist，文件名以 `.stoverride` 结尾，复制文件的 Raw 链接。**Secret Gist 不是严格私有：知道链接的人就可能读取内容。**请像保护订阅地址一样保护链接；如不能接受此风险，请改用本地覆写。
3. 在 Stash 中导入主配置，再导入并启用覆写；停用重复的旧覆写，避免配置冲突。入口及更新方式以当前 Stash 版本为准。
4. 在每台设备的 Stash 中打开 `beans` 的 Tailscale 登录入口，分别完成认证。检查订阅节点和策略组选择，测试普通网站及内网设备访问。已有设备可能保留旧的策略选择，需要手动调整。
5. 更新订阅时修改 Gist 文件，再在 Stash 更新覆写。不要把填有真实订阅地址的文件提交到公开仓库。

## 配置说明

- `Stash.yaml` 提供 DNS、策略组和公共规则；覆写提供订阅集及 `beans` 节点。
- `Manual` 和地区组用于选择线路；业务策略组可按需选择。地区组依据节点名称筛选，不含地区标识的节点可能不会自动纳入。
- 覆写的规则保留默认合并方式，避免替换主配置的全部规则；请在 Stash 中核实合并后的优先级。
- Tailscale 节点保留原有设置，不在共享模板中填写 `auth-key` 或固定 `hostname`。子网路由、MagicDNS、直连和中继的实际效果取决于设备、网络与 Tailscale 设置，需要分别测试。
- 在 Apple TV 使用 Fallback DNS 时，还应检查 Stash 网络设置中的对应开关。

本次修改已进行 YAML 语法检查，尚未在 Stash 客户端实测。应用前请备份现有配置，导入后检查业务分流与 Tailscale 连通性。

基础配置和业务规则源自 [Repcz/Tool](https://github.com/Repcz/Tool)，GFWList 域名列表源自 [Loyalsoldier/clash-rules](https://github.com/Loyalsoldier/clash-rules)。
