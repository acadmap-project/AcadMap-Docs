
# Tutorial de Implantação em Servidor com GitHub Actions

Este tutorial descreve como configurar um servidor para receber deployments automáticos usando GitHub Actions, Docker e SSH.

## Pré-requisitos

- [ ] Servidor Ubuntu ARM com acesso SSH
- [ ] Docker e Docker Compose instalados
- [ ] Git instalado
- [ ] Repositório clonado no servidor

## 1. Configuração do Servidor

### Instalação do Docker
```bash
# Atualizar sistema
sudo apt update && sudo apt upgrade -y

# Instalar Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Adicionar usuário ao grupo docker
sudo usermod -aG docker ubuntu

# Instalar Docker Compose
sudo apt install docker-compose-plugin -y
```

### Configuração do diretório do projeto
```bash
# Clonar repositório
cd /home/ubuntu
git clone https://github.com/SEU_USUARIO/SEU_REPOSITORIO.git AcadMap
cd AcadMap
```

## 2. Configuração dos Secrets no GitHub

Configure os seguintes secrets no repositório GitHub:

- `SSH_HOST`: IP ou domínio do servidor
- `SSH_USERNAME`: usuário SSH (ex: ubuntu)
- `SSH_KEY`: chave privada SSH
- `GHCR_PAT`: Personal Access Token do GitHub
- `BACKEND_IMAGE`: nome da imagem backend
- `FRONTEND_IMAGE`: nome da imagem frontend
- `BACK_API_URL`: URL da API backend

## 3. Estrutura do Arquivos Docker de Produção

### docker-compose.prod.yml
```yaml
version: "3.8"

services:
  backend:
    image: ghcr.io/${REGISTRY_USER}/backend:${BACKEND_IMAGE_TAG}
    ports:
      - "8080:8080"
    restart: always
    pull_policy: always

  frontend:
    image: ghcr.io/${REGISTRY_USER}/frontend:${FRONTEND_IMAGE_TAG}
    ports:
      - "8081:80"
    restart: always
    pull_policy: always
```
## 4. Configuração SSH

### Gerar chave SSH (se necessário)
```bash
ssh-keygen -t rsa -b 4096 -C "deploy@github"
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

### Configurar chave no GitHub Secrets
- Copie o conteúdo da chave privada (`~/.ssh/id_rsa`)
- Cole no secret `SSH_KEY`

## 5. Fluxo de Deploy

O workflow executará automaticamente quando houver push na branch `main`:

1. **Build**: Constrói imagens Docker do backend e frontend
2. **Push**: Envia imagens para GitHub Container Registry
3. **Deploy**: Conecta via SSH e atualiza containers no servidor

## 6. Monitoramento

### Verificar logs dos containers
```bash
docker compose logs -f
```

### Verificar status dos containers
```bash
docker compose ps
```

### Limpar imagens antigas
```bash
docker image prune -af
```

## Notas Importantes

- O workflow usa runners ARM64 (`ubuntu-24.04-arm`)
- Imagens são tagueadas com o SHA do commit
- Cache é utilizado para otimizar builds
- Deploy é feito com zero downtime usando Docker Compose
