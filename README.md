# Reserva de Horas Médicas - Proyecto DevOps

Servicio web estático de reserva de horas médicas para un centro de salud ficticio (Centro Médico Vitalia), servido con Nginx dentro de un contenedor Docker. El proyecto se desarrolló para la asignatura DevOps de IACC con el fin de aplicar control de versiones, contenedores, trazabilidad y buenas prácticas de seguridad en un entorno local reproducible.

> La página es una simulación: no tiene API ni base de datos, y los datos del formulario no se envían ni se guardan.

## Estructura del proyecto

```
reserva-horas-devops/
├── src/
│   ├── index.html
│   └── styles.css
├── nginx/
│   └── default.conf
├── Dockerfile
├── docker-compose.yml
├── .env.example
├── .gitignore
└── README.md
```

## Requisitos

- Git
- Docker Desktop (iniciado)
- Navegador web

## Instalación

1. Clonar el repositorio:

   ```bash
   git clone https://github.com/ivyorellana97/reserva-horas-devops.git
   cd reserva-horas-devops
   ```

2. Crear el archivo de variables a partir del ejemplo:

   ```bash
   cp .env.example .env
   ```

   En Windows (PowerShell): `Copy-Item .env.example .env`

## Ejecución

```bash
docker compose up -d --build
```

## Verificación

| Acción | Comando |
|---|---|
| Ver estado del servicio | `docker compose ps` |
| Abrir la aplicación | http://localhost:8080 |
| Revisar salud del servicio | http://localhost:8080/health |
| Ver logs | `docker logs reserva-horas-web` |
| Ver consumo de recursos | `docker stats --no-stream` |

## Detener el servicio

```bash
docker compose stop
```

Para eliminar el contenedor y la red creada:

```bash
docker compose down
```

## Seguridad

- El archivo `.env` no se sube al repositorio, ya que está incluido en `.gitignore`.
- `.env.example` solo contiene valores de ejemplo, nunca credenciales reales.
- No se publican tokens, claves, certificados ni datos personales.
- Nginx oculta su versión (`server_tokens off`) y agrega cabeceras de seguridad básicas.
- Antes de cada commit se revisan los cambios con `git status` y `git diff`.

## Flujo de trabajo

- `main` contiene la versión estable.
- Los cambios se hacen en ramas `feature/...` o `fix/...`.
- La integración a `main` se hace mediante pull request con revisión previa.
