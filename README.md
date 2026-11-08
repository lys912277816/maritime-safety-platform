# 全球航运安全态势与决策分析

全球重要航道、主要港口、真实 AIS 船位及接收轨迹、新闻热度、历史风险关注区域和可解释的航线决策分析。白色界面，适配桌面、平板和手机。

©上海交通大学智慧航运与现代物流课题组

## GitHub Pages 发布

`publish/` 包含可直接发布的完整网页，底图、样式和脚本已嵌入 `index.html`，无需安装后端或配置 AIS 密钥。将 `publish/index.html`、`publish/.nojekyll` 与 `publish/README.md` 放到 GitHub 仓库根目录，然后在仓库 Settings → Pages 选择 **Deploy from a branch → main → /(root)**。

发布成功后，GitHub 的 Pages 设置页会给出实际访问链接。尚未完成账号登录及发布时，不应把推测的 github.io 地址作为已上线链接。

## 数据与更新

网页调用既有固定数据服务：
<https://maritime-safety-review-20261108.jqy1316281374.chatgpt.site/>。

GitHub Pages 只托管界面，本机采集端继续接收 AIS 和新闻，每10秒同步到云端；网页每10秒轮询。电脑须保持开机联网并运行采集与同步程序。停止同步超过1分钟，页面标记数据延迟。AIS 密钥不进入 GitHub、网页或云端快照，公开页面不能管理本机密钥。

真实 AIS 为最新最多400艘采样及每船最近8个轨迹点，受上游接收覆盖影响。新闻为近24小时有限来源采样，当前在线来源以页面状态为准；港口与航道是静态参考，风险评分和航线分析是情景基线与规则判断。

## 重建

需要 Node.js 18.16 及以上版本：

```sh
npm ci
npm run build
```

编辑 `src/lib/api.ts` 可修改公开数据服务地址，也可在构建时通过 `VITE_API_ORIGIN` 指定。发布前应确认该数据服务支持所用 GitHub Pages 来源的跨域读取与航线分析。
