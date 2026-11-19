# Avaliação 02 - Relatório de evidências

Estudante: Marcos PAulo
Turma: __________________  Data: 18/11/2026
Identificador AV02_ID: marcos
Porta utilizada: 8080

## E01 - Preparação / configuração válida
- Comandos executados:
	- docker compose version
	- docker compose config --quiet
	- docker compose up -d --build
	- docker compose ps
- Saída relevante (retire qualquer senha real):
- NAME                              IMAGE                           COMMAND                  SERVICE    CREATED         STATUS                   PORTS
unisenai-av02-marcos-backend-1    unisenai-av02-marcos-backend    "gunicorn --bind 0.0…"   backend    3 minutes ago   Up 3 minutes (healthy)   8000/tcp
unisenai-av02-marcos-db-1         postgres:16-alpine              "docker-entrypoint.s…"   db         3 minutes ago   Up 3 minutes (healthy)   5432/tcp
unisenai-av02-marcos-frontend-1   unisenai-av02-marcos-frontend   "/docker-entrypoint.…"   frontend   3 minutes ago   Up 3 minutes (healthy)   127.0.0.1:8080->80/tcp
[+] Running 7/7
 ✔ unisenai-av02-marcos-backend               Built                                                                0.0s
 ✔ unisenai-av02-marcos-frontend              Built                                                                0.0s
 ✔ Network unisenai-av02-marcos_web_net       Created                                                              0.0s
 ✔ Network unisenai-av02-marcos_data_net      Created                                                              0.0s
 ✔ Container unisenai-av02-marcos-db-1        Healthy                                                              6.0s
 ✔ Container unisenai-av02-marcos-backend-1   Healthy                                                             11.6s
 ✔ Container unisenai-av02-marcos-frontend-1  Started    
- Evidência anexada:![[Pasted image 20261118200824.png]]
## E02 - Configuração segura do Compose
- Alterações no compose.yaml e .env.example:
	compose.yaml 
	- ![[Pasted image 20261118202437.png]]
	- AV02_ID=Marcos
APP_PORT=8182
POSTGRES_USER=marcos
POSTGRES_PASSWORD=postgres
POSTGRES_DB=unisenai
- Como conferi que backend e db não publicam portas no host:
-  docker compose ps
- Evidência anexada:
- ![[Pasted image 20261118203037.png]]



## E03 - Liveness, readiness e healthcheck
- Respostas HTTP normais observadas:
- Arquivos alterados:
- Evidência anexada:

## E04 - Integração
- Título único da tarefa: AV02-<seu-ID>-integracao
- POST: código HTTP e trecho da resposta:
- ![[Pasted image 20261118211407.png]]
- GET ou tela da tarefa:
![[Screenshot_1.png]]
- Caminho da requisição browser > ... > banco:
http://127.0.0.1:8182/api/tasks -> '/api/tasks' ->  "SELECT id, titulo, criada_em FROM tarefas ORDER BY id DESC LIMIT 100"  

## E05 - Persistência
- ID/título antes do down:
- AV02-Marcos-integracao
- Comandos utilizados, sem -v:
-  docker compose down
- docker compose up -d --build
- Evidência do mesmo registro após up:
- ![[Pasted image 20261118212054.png]]
- ![[Pasted image 20261118212152.png]]

## E06 - Falha controlada e recuperação
- Com db parado: /api/live = ___ e /api/ready = ___
- Qual log ou sinal investiguei:
- Após o start do db: /api/ready = ___
- Evidência anexada:

## E07 - Justificativa técnica
1. Por que somente o frontend publica uma porta no host?
Resposta: Pois apenas ele usa a variavel APP_HOST no .env, onde ele indentifica como uma variavel de ambiente

2. Por que .env não deve ser tratado como cofre de segredos?
Resposta:pois é um arquivo que pode ser enviado com o projeto

3. depends_on: service_healthy resolve indisponibilidade posterior do banco?
Resposta: não , ele apenas roda quando constrói o container

4. Volume nomeado é o mesmo que backup externo? Justifique.
Resposta: ele pode guardar em uma pasta externa aos container, possibilitando guardar estes dados mesmo derrubando os containers

## Checklist final
- [x] compose.yaml final
- [x] backend/app.py final
- [x] .env.example com valores estritamente fictícios
- [x] relatorio_evidencias.md preenchido
- [x] Evidências E01-E06
- [x] Sem .env nem dados sensíveis
