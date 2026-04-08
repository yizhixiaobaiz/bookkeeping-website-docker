# 个人记账应用 (Expense Tracker)

## 项目概述

这是一个基于前后端分离架构的个人记账应用，用于管理个人收支记录、分类管理和数据统计分析。应用采用现代化的技术栈，支持Docker容器化部署，并集成了HTTPS安全访问。

### 核心功能

- **用户认证**：注册/登录功能、JWT令牌认证、密码加密存储
- **交易记录管理**：添加、编辑、删除交易记录，支持收入和支出两种类型
- **分类管理**：系统默认分类、自定义分类、分类与用户关联
- **数据导入导出**：Excel格式导入导出、数据备份与恢复
- **统计分析**：收支趋势分析、分类占比分析、数据可视化图表
- **AI 集成**：AI聊天功能、技能管理

## 技术架构

### 前端技术栈

- **框架**：Vue 3
- **构建工具**：Vite
- **UI组件库**：Element Plus
- **状态管理**：Pinia
- **路由**：Vue Router
- **图表库**：ECharts
- **其他工具**：xlsx（Excel导入导出）、crypto-js（加密）

### 后端技术栈

- **运行环境**：Node.js
- **Web框架**：Express
- **数据库**：MySQL
- **认证**：JWT
- **AI集成**：OpenAI API
- **其他工具**：bcryptjs（密码加密）、dotenv（环境变量）

### 部署技术

- **容器化**：Docker
- **反向代理**：Nginx
- **HTTPS支持**：自签SSL证书

## 环境要求

- **Docker**：版本 20.0+
- **Docker Compose**：版本 1.29+
- **Node.js**（仅本地开发）：版本 14.0+
- **Git**：版本 2.0+

## 运行方式

### 方式一：一键启动（推荐）

1. **克隆项目**：
   ```bash
   git clone <仓库地址>
   cd <项目目录>
   ```

2. **运行启动脚本**：
   ```bash
   # Linux/Mac
   chmod +x qd.sh && ./qd.sh
   
   # Windows（使用 Git Bash 或 WSL）
   ./qd.sh
   ```

   该脚本会：
   - 自动生成 SSL 证书
   - 配置防火墙端口
   - 构建并启动所有容器

3. **访问应用**：
   - **前端**：https://localhost
   - **API**：http://localhost:3000/api
   - **健康检查**：http://localhost:3000/api/health

### 方式二：本地开发模式

**前端开发**：
```bash
npm install
npm run dev
# 访问：http://localhost:5173
```

**后端开发**：
```bash
cd server
npm install
npm run dev
# API地址：http://localhost:3000/api
```

## 项目结构

```
bookkeeping-website-docker-main/
├── src/                          # 前端源码
│   ├── components/business/      # 业务组件
│   ├── router/                   # 路由配置
│   ├── stores/                   # Pinia 状态管理
│   ├── utils/                    # 工具函数
│   └── views/                    # 页面视图
├── server/                       # 后端源码
│   ├── config/                   # 配置文件
│   ├── database/                 # 数据库初始化
│   ├── middleware/               # 中间件
│   ├── routes/                   # API 路由
│   └── server.js                 # 后端入口
├── docker-compose.yml            # Docker 服务编排
├── nginx.conf                    # Nginx 反向代理配置
├── qd.sh                        # 一键启动脚本
└── ssl/                          # SSL 证书目录
```

## 网络配置

- **前端服务**：
  - HTTP端口：80
  - HTTPS端口：443
- **后端API服务**：
  - 端口：3000
- **数据库服务**：
  - 端口：3306（容器内部）

## 环境变量

后端服务使用以下环境变量：
- `NODE_ENV`：运行环境（production/development）
- `DB_HOST`：数据库主机
- `DB_USER`：数据库用户名
- `DB_PASSWORD`：数据库密码
- `DB_NAME`：数据库名称
- `JWT_SECRET`：JWT密钥

## 数据库结构

### 1. users 表
- **id**：用户ID（主键）
- **username**：用户名（唯一）
- **password**：密码（加密存储）
- **created_at**：创建时间
- **updated_at**：更新时间

### 2. categories 表
- **id**：分类ID（主键）
- **user_id**：用户ID（外键）
- **name**：分类名称
- **type**：类型（income/expense）
- **created_at**：创建时间
- **updated_at**：更新时间

### 3. records 表
- **id**：记录ID（主键）
- **user_id**：用户ID（外键）
- **type**：类型（income/expense）
- **category**：分类
- **amount**：金额
- **date**：日期
- **datetime**：时间
- **note**：备注
- **created_at**：创建时间
- **updated_at**：更新时间

## 注意事项

1. **SSL证书**：
   - 项目使用自签SSL证书，仅用于开发和测试环境
   - 生产环境建议使用受信任的CA证书

2. **端口冲突**：
   - 若端口冲突，可修改 `docker-compose.yml` 中的端口映射
   - 例如：将 `80:80` 改为 `8080:80`

3. **数据备份**：
   - 定期备份数据库数据，避免数据丢失
   - 数据库数据存储在 `mysql-data` 卷中

4. **性能优化**：
   - 生产环境建议增加服务器资源
   - 可根据实际用户量调整容器资源限制

5. **安全配置**：
   - 修改默认的数据库密码和JWT密钥
   - 配置防火墙规则，限制外部访问

## 项目特点

1. **前后端分离**：清晰的职责划分，便于维护和扩展
2. **容器化部署**：简化部署流程，提高环境一致性
3. **数据安全**：密码加密、JWT认证、HTTPS传输
4. **用户体验**：响应式设计、友好的UI、流畅的交互
5. **功能完整**：从基础记账到高级统计分析，满足个人记账需求
6. **可扩展性**：模块化设计，便于添加新功能
7. **AI集成**：提供智能助手功能，增强用户体验

## 停止服务

```bash
docker-compose down
```

## 故障排查

1. **服务启动失败**：
   - 检查 Docker 是否正常运行
   - 检查端口是否被占用
   - 查看容器日志：`docker logs <容器名称>`

2. **数据库连接问题**：
   - 检查数据库服务是否启动
   - 验证环境变量配置是否正确

3. **前端访问问题**：
   - 检查 Nginx 配置是否正确
   - 验证 SSL 证书是否生成成功

项目已完全配置就绪，只需按照上述步骤即可快速启动和运行。
