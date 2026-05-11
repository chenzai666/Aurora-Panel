# Aurora Panel

Aurora Panel 是一个基于 GOST 的可视化转发管理面板，包含前端、后端、节点程序与一键安装脚本。

## 核心能力

- 支持 TCP / UDP 转发
- 支持端口转发与隧道转发
- 支持用户、隧道、节点管理
- 支持账号级与隧道级流量控制
- 支持限速策略与到期策略
- 支持节点监控、隧道管理拖拽排序

## 仓库与镜像

- GitHub: `https://github.com/chenzai666/Aurora-Panel`
- 前端镜像: `chenzai666/aurora-panel-frontend:v1.4.3`
- 后端镜像: `chenzai666/aurora-panel-backend:v1.4.3`

## 快速部署

### 面板端（推荐）

```bash
curl -L https://raw.githubusercontent.com/chenzai666/Aurora-Panel/refs/heads/main/panel_install.sh -o panel_install.sh && chmod +x panel_install.sh && ./panel_install.sh
```

### 节点端

```bash
curl -L https://raw.githubusercontent.com/chenzai666/Aurora-Panel/refs/heads/main/install.sh -o install.sh && chmod +x install.sh && ./install.sh
```

## 手动 Docker Compose 部署

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

### 4) 旧版本升级说明

如果你是从旧版本升级，请执行一次以下 SQL，避免拖拽排序保存失败：

```sql
ALTER TABLE node ADD COLUMN inx int(10) NOT NULL DEFAULT 0;
ALTER TABLE tunnel ADD COLUMN inx int(10) NOT NULL DEFAULT 0;
```

## Release 下载

- 最新发布（当前）：`v1.4.3`
- 地址：`https://github.com/chenzai666/Aurora-Panel/releases/tag/v1.4.3`
- 资产包含：
  - `install.sh`
  - `panel_install.sh`
  - `docker-compose-v4.yml`
  - `docker-compose-v6.yml`
  - `gost.sql`
  - `gost-amd64`
  - `gost-arm64`

## 默认管理员账号

- 用户名：`admin_user`
- 密码：`admin_user`

首次登录后请立即修改默认密码。

## 免责声明

本项目仅用于合法场景下的学习与研究。使用本项目带来的风险（服务异常、数据损失、法律责任等）由使用者自行承担。
