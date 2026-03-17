# Subconverter & Sub-web 开发指南

本文档提供了使用 Docker 部署和开发 Subconverter (MetaCubeX) 与 Sub-web (Modify) 项目的说明。

## 架构

- **后端**: [MetaCubeX/subconverter](https://github.com/MetaCubeX/subconverter) - 处理核心订阅转换逻辑。
- **前端**: [youshandefeiyang/sub-web-modify](https://github.com/youshandefeiyang/sub-web-modify) - 提供管理订阅的 Web 界面。

## 部署

### 前提条件

- Docker
- Docker Compose

### 快速开始 (Docker Compose)

项目包含一个统一的 `docker-compose.yml` 来运行这两个服务。

1.  **启动服务**:
    ```bash
    docker-compose up -d
    ```

2.  **访问应用**:
    - **前端**: [http://localhost:25501](http://localhost:25501)
    - **后端**: [http://localhost:25500](http://localhost:25500)

### 端口映射

| 服务 | 容器端口 | 宿主机端口 |
| :--- | :--- | :--- |
| Subconverter (后端) | 25500 | 25500 |
| Sub-web (前端) | 80 | 25501 |

## 配置

- **后端配置**: 你可以根据需要修改 `base/` 目录中的 `pref.ini` 和其他配置文件（如果需要，可以通过 volumes 映射，但默认配置通常已足够）。
- **前端后端地址**: 默认情况下，前端配置为指向 `http://localhost:25500`。在第一次访问时，前端已硬编码默认使用自建服务器 IP。

## 本地开发 (非 Docker)

### 后端
1. 参考 [README-cn.md](./README-cn.md) 文档，使用 CMake 从源码构建。

### 前端
1. 进入 `sub-web` 目录:
   ```bash
   cd sub-web
   yarn install
   yarn serve
   ```
2. 本地开发服务器通常运行在 `http://localhost:8080`。

## 故障排查与提示

### Quantumult X "Response Invalid"
如果在 Quantumult X 中更新订阅时遇到 `response invalid`:
- **原因**: 当作为外部资源导入时，QuanX 通常只期望接收 **节点列表 (Node List)**。如果 Subconverter 返回的是完整配置文件（默认情况），则可能会失败。
- **解决方案**: 
  - 确保在 Sub-web 界面中勾选了 **“仅输出节点信息” (Only Output Node Info)**。
  - 或者手动在生成的订阅 URL 末尾添加 `&list=true`。
