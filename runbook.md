# 三式浑象展示站 · 部署 Runbook

> 目标：`http://152.175.242.90/` 上线展示站；下载需要密码 `xyn1314520`
> 前提：能登录服务器 VNC 控制台（root）

## 步骤 1：部署（约 30 秒）
```bash
curl -fsSL https://paste.rs/8itkU -o /tmp/ss.sh && bash /tmp/ss.sh
```
镜像（若上面超时）：
```bash
curl -fsSL https://nailongdiguo.github.io/sanshi-site/install-min.sh -o /tmp/ss.sh && bash /tmp/ss.sh
```

期望输出：
```
页面: 200
无密码: 403 (应403)
错密码: 403 (应403)
正密码: 200 (应200)
访问 http://152.175.242.90/
```

## 步骤 2：浏览器验证
打开 `http://152.175.242.90/`，应看到暗色星空页「三式浑象」，向下滚动共 8 个区块。

## 步骤 3：补两个安装包（可选，共 186MB）
手机端 40MB：
```bash
curl -fsSL https://paste.rs/d2Fx6 -o /tmp/m.sh && bash /tmp/m.sh
```
电脑版 146MB：
```bash
curl -fsSL https://paste.rs/wUwJS -o /tmp/d.sh && bash /tmp/d.sh
```

## 步骤 4：下载测试
- 页面 → 下载中心 → 输入 `xyn1314520` → 四个文件出现
- 直连应 403：`http://152.175.242.90/files/doc.docx`
- 带密码应 200：`http://152.175.242.90/files/doc.docx?key=xyn1314520`

## 排错
| 现象 | 处理 |
|---|---|
| curl 不存在 | `apt-get install -y curl` |
| 403（密码正确） | 手输测试，避免客户端 URL 编码差异 |
| 仍是 nginx 欢迎页 | `nginx -t && systemctl reload nginx` |
| 文件 404 | `ls -lh /var/www/sanshi/files` |
| 外网访问不通 | `ufw allow 80/tcp` |

## 收尾
1. 删除中转仓库 `sanshi-assets`
2. 作废 GitHub token（`ghp_...`）
3. 修改服务器 root 密码：`passwd`

## 预览（无需服务器）
https://nailongdiguo.github.io/sanshi-site/
