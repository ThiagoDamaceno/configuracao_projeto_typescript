<h1>Typescript + eslint + git + editorconfig + typeorm + Docker + Postgres</h1>

<br>

<h4>1 - Instalar as seguintes extensões no vscode:</h4>
<ul>
  <li>ESlint</li>
  <li>Editor Config for VS Code</li>
  <li>Dotenv</li>
</ul>


<br>

<h4>2 - Criar arquivo package.json:</h4>
```
yarn init -y
```

<br>

<h4>3 - Criar arquivo .editorconfig com a extensão do vscode com as seguintes configurações:</h4>
<ul>
  <li>end_of_line = lf</li>
  <li>ident_size = 2</li>
</ul>

<br>

<h4>4 - Iniciar o repositório git:</h4>
```
git init
```

<p>Criar arquivo .gitignore com os seguintes conteúdos:</p>
```
node_modules
*lock.json
*.lock
.env
```

<br>

<h4>5 - Iniciar o projeto com typescript:</h4>
```
yarn add typescript -D
```
```
yarn add ts-node-dev -D
```
```
yarn tsc --init
```
<p>No arquivo tsconfig.json:</p>
```
{
  "compilerOptions": {
    "target": "es2021",        
    "allowJs": true,                      
    "module": "commonjs",                            
    "esModuleInterop": true,                         
    "forceConsistentCasingInFileNames": true,                                          
    "skipLibCheck": true,
    "strict": false,
    "outDir": "./dist"                      
  }
}
```
<br>

<h4>6 - Eslint:</h4>
```
yarn add eslint -D
```
```
yarn eslint --init
```
<p>No terminal:</p>
<ul>
  <li>To check syntax, find problems, and enforce code style</li>
  <li>Import/export</li>
  <li>None of these</li>
  <li>Yes, use typescript</li>
  <li>Node</li>
  <li>Use a popular guide style</li>
  <li>Standard</li>
  <li>JSON</li>
  <li>yes</li>
  <li>yes</li>
</ul>

<p>Nas configurações do vscode (ctrl + shift + p) settings.json, adicionar: </p>
```
"editor.codeActionsOnSave": {
  "source.fixAll": true
}
```

<br>

<h4>7 - Dependência do dotenv</h4>
```
yarn add dotenv
```

<br>

<h4>8 - Rodar projeto:</h4>

<p>No arquivo package.json, adicionar: </p>
```
"scripts": {
  "dev": "ts-node-dev ./src/index.ts",
  "build": "tsc",
  "start": "node ./dist/index.js"
},
```

<p>Executar ambiente de desenvolvimento: </p>
```
yarn dev
```

<p>Gerar build de produção: </p>
```
yarn build
```

<p>Executar ambiente de produção: </p>
```
yarn start
```

<br>


<h4>9 - Typeorm Doc Oficial: https://typeorm.io/#/</h4>

<p>Depêndencias:</p>

```
yarn add typeorm reflect-metadata
```

<br>

<p>Ao utilizar com o Postgres:</p>

```
yarn add pg
```

<br>

<p>No arquivo .env (criar caso não exista). Na build para js, alterar o caminho das variáveis dos arquivos/diretórios: </p>
```
TYPEORM_CONNECTION = postgres
TYPEORM_HOST = localhost
TYPEORM_USERNAME = root
TYPEORM_PASSWORD = root
TYPEORM_DATABASE = teste_postgres
TYPEORM_PORT = 5432
TYPEORM_MIGRATIONS = ./src/database/migrations/*.ts
TYPEORM_MIGRATIONS_DIR = ./src/database/migrations
TYPEORM_ENTITIES = ./src/models/*.ts
TYPEORM_ENTITIES_DIR = ./src/models
```

<br>


<p>No arquivo package.json, adicionar aos scripts: </p>
```
"scripts": {
  "typeorm": "ts-node-dev node_modules/.bin/typeorm"
}
```

<br>

<p>No arquivo tsconfig.json, adicionar: </p>
```
"emitDecoratorMetadata": true,
"experimentalDecorators": true,
```

<br>

<p>Iniciar a conexão, em algum lugar do código</p>
```
import { createConnection } from 'typeorm'
createConnection()
```

<br>

<h4>10 - Docker + Postgres</h4>
<p>Criar arquivo docker-compose.yml, contendo o seguinte conteudo: </p>

```
version: "3"
services:
  postgres:
    image: postgres:latest
    environment:
      POSTGRES_DB: ${POSTGRES_DB}
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
    ports:
      - "${POSTGRES_PORT}:${POSTGRES_PORT}"
```

<br>

<p>No arquivo .env (podendo alterar o conteúdo das variáveis livremente), adicionar: </p>
```
POSTGRES_DB = teste_postgres
POSTGRES_USER = root
POSTGRES_PASSWORD = root
POSTGRES_PORT = 5432
POSTGRES_HOST = localhost
```

<br>

<p>Criação do container do postgres, com terminal (Em linux, utilizar com sudo):</p>
```
docker-compose up -d
```
```
docker-compose down
```
