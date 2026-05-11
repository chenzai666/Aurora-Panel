# Aurora Panel

Aurora Panel 是一个基于 GOST 的可视化转发管理面板。

## 界面风格

- 默认采用 Claude 风格的浅色优先设计语言
- 配色以中性色与语义色为主，避免高饱和干扰色
- 后台管理页与移动端页面保持统一的视觉体系
- 支持深浅色主题切换，组件风格保持一致

## 仓库与镜像

- GitHub: `https://github.com/chenzai666/Aurora-Panel`
- 镜像版本: `v1.4.3`

## 快速部署

### 面板端（推荐）

```bash
curl -L https://raw.githubusercontent.com/chenzai666/Aurora-Panel/refs/heads/main/panel_install.sh -o panel_install.sh && chmod +x panel_install.sh && ./panel_install.sh
```

### 节点端

```bash
curl -L https://raw.githubusercontent.com/chenzai666/Aurora-Panel/refs/heads/main/install.sh -o install.sh && chmod +x install.sh && ./install.sh
```

## 手动部署

### 1) 下载部署文件

```bash
curl -L https://raw.githubusercontent.com/chenzai666/Aurora-Panel/refs/heads/main/docker-compose-v4.yml -o docker-compose-v4.yml
curl -L https://raw.githubusercontent.com/chenzai666/Aurora-Panel/refs/heads/main/gost.sql -o gost.sql
```

### 2) 创建环境变量文件

```bash
cat > .env << 'EOF'
DB_NAME=gost
DB_USER=gost
DB_PASSWORD=your_db_password
JWT_SECRET=your_jwt_secret
BACKEND_PORT=6365
FRONTEND_PORT=6366
EOF
```

### 3) 启动

```bash
docker compose -f docker-compose-v4.yml up -d
```

### 4) 旧版本升级

如果你是从旧版本升级，请执行一次以下 SQL：

```sql
ALTER TABLE node ADD COLUMN inx int(10) NOT NULL DEFAULT 0;
ALTER TABLE tunnel ADD COLUMN inx int(10) NOT NULL DEFAULT 0;
```

## Release

- 当前版本：`v1.4.3`
- 下载地址：`https://github.com/chenzai666/Aurora-Panel/releases/tag/v1.4.3`

## 默认管理员账号

- 用户名：`admin_user`
- 密码：`admin_user`

首次登录后请立即修改默认密码。

## 免责声明

本项目仅用于合法场景下的学习与研究。使用本项目带来的风险（服务异常、数据损失、法律责任等）由使用者自行承担。
