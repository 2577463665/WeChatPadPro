# WechatPadPro 部署指南

## 系统要求

- Docker 20.10.0 或更高版本
- Docker Compose v2.0.0 或更高版本
- 至少 2GB 可用内存
- 至少 10GB 可用磁盘空间

## 快速部署

1. 创建部署目录：
```bash
mkdir wechatpadpro && cd wechatpadpro
```

2. 下载部署文件：
   - 将 `docker-compose.yml` 和 `.env` 文件复制到部署目录

3. 启动服务：
```bash
docker-compose up -d
```

4. 验证服务状态：
```bash
docker-compose ps
```

## 配置说明
下面这些不需要改动容器默认全部配置好了
### 环境变量（.env）

1. 应用配置：
   - `DEBUG`: 调试模式开关（false/true）
   - `ADMIN_KEY`: 管理员密钥
   - `HOST`: 监听地址
   - `PORT`: 监听端口

2. Redis配置：
   - `REDIS_HOST`: Redis主机名
   - `REDIS_PORT`: Redis端口
   - `REDIS_DB`: Redis数据库编号
   - `REDIS_PASS`: Redis密码

3. MySQL配置：
   - `MYSQL_ROOT_PASSWORD`: MySQL root密码
   - `MYSQL_DATABASE`: 数据库名
   - `MYSQL_USER`: 数据库用户
   - `MYSQL_PASSWORD`: 数据库密码

4. 系统配置：
   - `TZ`: 时区设置

### 持久化存储

系统使用以下Docker卷进行数据持久化：
- `wechatpadpro_data`: 应用数据
- `wechatpadpro_logs`: 应用日志
- `redis_data`: Redis数据
- `mysql_data`: MySQL数据

## 服务访问

- 应用访问地址：`http://localhost:1239`


## 常用操作

1. 查看服务日志：
```bash
docker-compose logs -f
```

2. 重启服务：
```bash
docker-compose restart
```

3. 停止服务：
```bash
docker-compose down
```

4. 完全清理（包括数据）：
```bash
docker-compose down -v
```

## 注意事项

1. 首次启动时，MySQL会自动初始化数据库结构
2. 请确保修改默认密码以提高安全性
3. 建议定期备份数据卷
4. 如需修改配置，请编辑.env文件后重启服务

## 故障排除

1. 如果服务无法启动，请检查：
   - Docker服务是否正常运行
   - 端口1239是否被占用
   - 系统资源是否充足

2. 如果数据库连接失败：
   - 确认MySQL容器是否正常运行
   - 检查数据库密码配置是否正确

3. 如果Redis连接失败：
   - 确认Redis容器是否正常运行
   - 检查Redis密码配置是否正确

## 技术支持

如遇到问题，请查看应用日志：
```bash
docker-compose logs wechatpadpro
``` 