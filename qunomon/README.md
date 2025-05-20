# qunomon

## Overview

`qunomon` is an experimental AI system quality testbed for managing and validating AI system components. It combines frontend, backend, integration provider, storage, and workflow orchestration with a reverse proxy layer to support development and evaluation.

## Architecture

The repository contains the following main components:

- `src/frontend/` - Vue.js frontend application
- `src/backend/` - Flask-based backend API service
- `src/integration-provider/` - integration provider service
- `src/storage/` - PostgreSQL storage and related schemas
- `src/docker-airflow/` - Airflow orchestration environment
- `src/reverse-proxy-resty-local/` - local reverse proxy with TLS support

## Requirements

### Supported platforms

- Windows 10 Pro 1909 or later
- macOS 10.15 or later

### Required software

- Docker Desktop 2.3.0.3 or later
- Git
- Python 3.9.x for local development

## Quick Start (Docker)

From the repository root, start the full environment:

```sh
docker compose up -d
```

If your system uses the legacy `docker-compose` binary, run:

```sh
docker-compose up -d
```

This command starts the following services:

- reverse-proxy
- frontend web server
- backend API
- integration provider API
- PostgreSQL storage
- Airflow scheduler/webserver/worker
- Redis and pgAdmin

## Access URLs

- Reverse proxy (HTTPS): `https://127.0.0.1:443/`
- Reverse proxy (HTTP): `http://127.0.0.1:8888/`
- Frontend raw app: `http://127.0.0.1:8000/`
- Airflow UI: `http://127.0.0.1:8180/`
- pgAdmin: `http://127.0.0.1:5051/`

## TLS Certificate

The local reverse proxy uses a self-signed certificate. To avoid browser trust issues, import the root certificate located at:

```text
./src/reverse-proxy-resty-local/ssl/cert/ca.crt
```

Import it into your OS/browser as a trusted root certificate authority for local development.

## Local Development

### Backend

1. Open PowerShell with administrator privileges.
2. Create a Python virtual environment:

```powershell
cd <repository-root>\src\backend
python -m venv venv
```

3. Activate the environment:

```powershell
.\venv\Scripts\activate
```

4. Install dependencies:

```powershell
pip install -r requirements_dev.txt
```

5. Start the backend service:

```powershell
python -m entrypoint startserver
```

### Integration Provider

1. Create a Python virtual environment:

```powershell
cd <repository-root>\src\integration-provider
python -m venv venv
```

2. Activate the environment:

```powershell
.\venv\Scripts\activate
```

3. Install dependencies:

```powershell
pip install -r constraints.txt
```

4. Start the integration provider service:

```powershell
python -m entrypoint startserver
```

### Frontend

From the frontend directory, use Docker Compose or the Vue development server:

```sh
cd <repository-root>/src/frontend
docker-compose up -d
```

Then visit `http://127.0.0.1:8080/`.

> Note: When accessing the frontend directly, browser CORS settings may block API requests. Use a compatible browser extension or the reverse proxy path for local development.

## Windows Startup Scripts

The repository includes helper scripts for Windows development:

- `start_up.bat` - starts storage, Airflow, backend, integration provider, and frontend
- `start_up_backend.bat` - starts only the backend service locally
- `start_up_ip.bat` - starts only the integration provider service locally
- `start_up_docker_debug.bat` - debug support for Docker-based startup

## Stopping Services

To stop and remove the Docker environment:

```sh
docker compose down
```

or

```sh
docker-compose down
```

## Contribution

Bug reports and pull requests are welcome on GitHub at [aistairc/qunomon](https://github.com/aistairc/qunomon).

## Disclaimer

`qunomon` is an open-source alpha project. It is intended for experimental use only. Use it at your own risk.

## License

[Apache License Version 2.0](LICENSE.txt)

## Author

[AIST](https://www.aist.go.jp/)

