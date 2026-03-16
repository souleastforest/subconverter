# Subconverter & Sub-web Development Guide

This document provides instructions for deploying and developing the Subconverter (MetaCubeX) and Sub-web (Modify) project using Docker.

## Architecture

- **Backend**: [MetaCubeX/subconverter](https://github.com/MetaCubeX/subconverter) - Handles the core subscription conversion logic.
- **Frontend**: [youshandefeiyang/sub-web-modify](https://github.com/youshandefeiyang/sub-web-modify) - Provides a web interface for managing subscriptions.

## Deployment

### Prerequisites

- Docker
- Docker Compose

### Quick Start (Docker Compose)

The project includes a unified `docker-compose.yml` to run both services.

1.  **Start the services**:
    ```bash
    docker-compose up -d
    ```

2.  **Access the applications**:
    - **Frontend**: [http://localhost:25501](http://localhost:25501)
    - **Backend**: [http://localhost:25500](http://localhost:25500)

### Port Mappings

| Service | Container Port | Host Port |
| :--- | :--- | :--- |
| Subconverter (Backend) | 25500 | 25500 |
| Sub-web (Frontend) | 80 | 25501 |

## Configuration

- **Backend Configuration**: You can modify the `pref.ini` and other configuration files in the `base/` directory (mapped via volumes if needed, though default handles most cases).
- **Frontend Backend URL**: By default, the frontend is configured to point to `http://localhost:25500`. On first visit, you may need to ensure the "Backend Address" in the UI correctly points to your API endpoint.

## Local Development (Without Docker)

### Backend
1. Follow the instructions in [README-cn.md](./README-cn.md) to build from source using CMake.

### Frontend
1. Navigate to the `sub-web` directory:
   ```bash
   cd sub-web
   yarn install
   yarn serve
   ```
2. The local dev server will typically run on `http://localhost:8080`.
