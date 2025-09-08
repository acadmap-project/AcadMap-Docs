# Guia de Implantação: localhost

## 1. Pré-requisitos
É importante notar que esse tutorial de implantação leva em consideração o cenário sugerido pelo cliente: Inicializar a aplicação em localhost.
### Requisitos de Sistema
- [ ] Sistema operacional Linux.
- [ ] 1GB de Memória RAM mínima.
- [ ] Portas 8081, 8080, 5432 e 80 liberadas para uso.

### Dependências
- [ ] Git
- [ ] Docker
- [ ] Docker Compose

## 2. Preparação do Ambiente
Com os requisitos de sistema e dependências solucionadas, podemos seguir com a implantação do sistema.

## 3. Processo de Instalação

### Passo 1: Download
```bash
git clone https://github.com/acadmap-project/AcadMap.git
```

### Passo 2: Configuração
Caso seu objetivo seja rodar em uma rede local e que todos os computadores dessa rede tenham acesso, é necessário configurar a URL da API do Backend no Frontend. Caso esse não seja seu objetivo, pule para o tópico "inicalização".
```bash
cd ./AcadMap/frontend/src/utils/
sed -i "s#http://localhost:8080#http://$(hostname -I | awk '{print $1}'):8080#g" ./apiUrl.js
cd ../../..
```

### Passo 3: Inicialização
No diretório raiz da aplicação, execute o seguinte comando para iniciar o projeto:
```bash
docker compose up
```

Após a inicialização, o projeto já estará pronto para o uso no ip da rede local da máquina onde o projeto foi implantado.