## 02. Add authentification layer with authelia and traefik

### Prerequisites

Docker

- [macOS](https://docs.docker.com/desktop/install/mac-install/)
- [Linux](https://docs.docker.com/engine/install/)
- [Windows](https://docs.docker.com/desktop/install/windows-install/)

Git Version Control System

- [Git](https://git-scm.com/downloads)

\* Bash compatible shell for Windows
- [Git Bash](https://git-scm.com/downloads)

### 1. Clone additional repos

- Main DataLens repo with docker-compose.yml file

`git clone git@github.com:datalens-tech/datalens.git`

### 2. Generate your secrets

Copy `.env.example` file to `.env` and replace secrets

Secrets can be generated by script: `scripts/gen-secrets.sh`

\* For custom `DL_CRY_KEY` variable value you need to recreate manually PostgreSQL demo connection with new crypto key

### 3. Check authelia config

Check authelia config with users list at:

- `authelia/configuration.yml`

- `authelia/users.yml`

! Be sure to change the password in the file `authelia/users.yml` with argon2 crypto hash algorithm

You can generate password by command:

`docker run authelia/authelia authelia crypto hash generate argon2 --password 'YOUR_PASSWORD'`

### 4. Pull all needed docker images

`docker compose pull`

### 5. Up all compose stack

`docker compose up -d`

### 6. Copy root cert to local folder

Copy root certificate to local folder to import in browser settings

`docker compose cp traefik:/acme/certs/root_ca.crt ./root_ca.crt`

### 7. Add additional domains for local resolve

- For linux:

`sudo nano /etc/hosts`

- For Windows:

`Windows/System 32/drivers/etc`

Additional domains:

```
127.0.0.1 datalens.dev
127.0.0.1 traefik.datalens.dev
127.0.0.1 authelia.datalens.dev
```

### 8. Open DataLens

Open your custom DataLens by path: [https://datalens.dev](https://datalens.dev)