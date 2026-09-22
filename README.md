# Curso CASE Java — Laboratório (Portal de Pedidos B2B)

Aplicação **Spring Boot 3 / Java 17** propositalmente vulnerável, usada nos
laboratórios do curso **CASE Java (Certified Application Security Engineer)**.
Este repositório é o **código que o aluno executa e corrige** nos labs.

> ⚠️ Código **intencionalmente inseguro**, apenas para fins didáticos. Não use em produção.

## 1. Pré-requisitos

Máquina zerada? Um script instala **Git, Java 17, Maven e (opcional) Docker/Eclipse**:

**Windows** — duplo-clique em `scripts\setup-choco.bat` (Chocolatey) ou `scripts\setup.bat` (winget).
Ou, num PowerShell **como Administrador**:
```powershell
.\scripts\setup-choco.ps1
```

**macOS / Linux**:
```bash
chmod +x scripts/setup.sh && ./scripts/setup.sh
```

Mínimo necessário para rodar: **Java 17** (o projeto já traz o wrapper `mvnw`).

## 2. Subir o ambiente (um comando)

**Sem Docker** (app em H2, em memória — recomendado para a maioria dos labs):
```powershell
.\scripts\start.ps1 -NoDocker
```
```bash
./scripts/start.sh --no-docker
```

**Com Docker** (app + Postgres):
```powershell
.\scripts\start.ps1
```
```bash
./scripts/start.sh
```

Acesse <http://localhost:8080>.

Contas de teste:

| E-mail | Senha | Papel |
|--------|-------|-------|
| admin@portal.com | admin123 | ADMIN |
| joao@acme.com | senha123 | USER |
| maria@globex.com | senha123 | USER |

Parar tudo: `.\scripts\start.ps1 -Stop` (ou `./scripts/start.sh --stop`).

## 3. O codebase de cada aula (tags Git)

Cada laboratório parte de um ponto da história do Git:

| Tag | Uso |
|-----|-----|
| `aula-1-baseline` … `aula-6-baseline` | ponto de partida de cada lab |
| `aula-2-hardened` … `aula-6-hardened` | solução de referência |

O script já faz o checkout para você:
```powershell
.\scripts\start.ps1 -Lab 3 -NoDocker      # pega aula-3-baseline e sobe
```
```bash
./scripts/start.sh --lab 3 --no-docker
```

> Os **guias de cada laboratório** (o que fazer em cada aula) são fornecidos pelo instrutor.

## 4. Estrutura

```
portal-pedidos/     aplicação Spring Boot (o código do lab)
infra/              docker-compose (app + Postgres + SonarQube)
scripts/            setup.* (instalar) e start.* (subir o ambiente)
```

## 5. Modos do start

| Flag | O que faz |
|------|-----------|
| _(padrão)_ | app + Postgres via Docker |
| `-NoDocker` / `--no-docker` | app em H2, sem Docker |
| `-Dev` / `--dev` | só o banco no Docker; app via `mvnw` (editar/depurar) |
| `-Lab N` / `--lab N` | checkout de `aula-N-baseline` e sobe |
| `-Sonar` / `--sonar` | sobe também o SonarQube (:9000) |
| `-Stop` / `--stop` | derruba tudo |
