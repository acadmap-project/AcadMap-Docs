# 7. Governança de Arquitetura
![Static Badge](https://img.shields.io/badge/Arquitetura-%230074B6?style=for-the-badge&logo=githubactions&logoColor=%23F2F2F2)

A governança da arquitetura do sistema AcadMap segue diretrizes que garantem rastreabilidade, consistência e validação colaborativa das decisões técnicas. 

## 7.1 Decisões Arquiteturais
Todas as decisões arquiteturais relevantes são formalizadas por meio de registros do tipo RDA (Registro de Decisão Arquitetural), numerados sequencialmente e armazenados no repositório `docs/rda`. 

## 7.2 Alterações no DAS
Qualquer alteração significativa no Documento de Arquitetura de Sistema (DAS) deve ser submetida via *pull request*, obrigatoriamente revisada por outro membro da equipe de Arquitetura. Essa prática assegura que as modificações sejam avaliadas quanto à sua conformidade com os princípios arquiteturais e impacto no sistema.

## 7.3 Sobre o Versionamento
Além disso, as versões do DAS são etiquetadas conforme os ciclos de entrega do projeto, utilizando versionamento semântico e.g. `v1.0`, `v1.1` e assim por diante. Isso permite o controle histórico da evolução da arquitetura e facilita a referência a versões específicas durante auditorias, revisões técnicas e fases de manutenção.


## 7.4 Ferramentas de Apoio à Arquitetura
A elaboração, manutenção e disseminação da arquitetura do sistema AcadMap são apoiadas por um conjunto de ferramentas que promovem automação, padronização e rastreabilidade. Essas ferramentas estão integradas ao fluxo de desenvolvimento e à governança do DAS, conforme a tabela abaixo:

| ID   | Ferramenta       | Finalidade                                  |
|------|------------------|---------------------------------------------|
| 001  | MkDocs           | Geração da documentação navegável em Markdown |
| 002  | Mermaid          | Criação de diagramas leves em Markdown      |
| 003  | PlantUML         | Modelagem de diagramas estruturados via texto |
| 004  | GitHub           | Controle de versionamento e colaboração     |
| 005  | GitHub Actions   | Automação de pipelines CI/CD e publicação   |
| 006  | GitHub Projects  | Acompanhamento visual das atividades (Kanban) |
