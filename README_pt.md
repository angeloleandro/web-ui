<img src="./assets/web-ui.png" alt="Browser Use Web UI" width="full"/>

<br/>

# Browser Use WebUI com suporte ao Gemini 2.0-flash

Esta interface web facilita o uso da biblioteca [browser-use](https://github.com/browser-use/browser-use), permitindo que agentes de IA interajam com sites de forma eficiente.

## Recursos Principais

**WebUI:** Construída em Gradio, oferece uma interface amigável para interagir com o agente de navegador.

**Suporte a múltiplos LLMs:** Integração com diversos modelos de linguagem, incluindo Google Gemini 2.0-flash, OpenAI, Azure OpenAI, Anthropic, DeepSeek, Ollama, OpenRouter e outros.

**Navegador Personalizado:** Use seu próprio navegador com nossa ferramenta, eliminando a necessidade de fazer login novamente em sites ou lidar com desafios de autenticação.

**Sessões de Navegador Persistentes:** Mantenha a janela do navegador aberta entre tarefas de IA para preservar o histórico completo e o estado das interações.

## Guia de Instalação

### Pré-requisitos
- Python 3.11 ou superior
- Git (para clonar o repositório)

### Opção 1: Instalação Local

#### Passo 1: Clonar o Repositório
```bash
git clone https://github.com/browser-use/web-ui.git
cd web-ui
```

#### Passo 2: Configurar o Ambiente Python
Recomendamos usar [uv](https://docs.astral.sh/uv/) para gerenciar o ambiente Python.

Usando uv (recomendado):
```bash
uv venv --python 3.11
```

Ativando o ambiente virtual:
- Windows (Prompt de Comando):
```cmd
.venv\Scripts\activate
```
- Windows (PowerShell):
```powershell
.\.venv\Scripts\Activate.ps1
```
- macOS/Linux:
```bash
source .venv/bin/activate
```

#### Passo 3: Instalar Dependências
Instalar pacotes Python:
```bash
uv pip install -r requirements.txt
```

Instalar Playwright:
```bash
playwright install
```

#### Passo 4: Configurar o Ambiente
1. Crie uma cópia do arquivo de ambiente de exemplo:
- Windows (Prompt de Comando):
```bash
copy .env.example .env
```
- macOS/Linux/Windows (PowerShell):
```bash
cp .env.example .env
```
2. Abra o arquivo `.env` no seu editor de texto preferido e adicione suas chaves de API e outras configurações.

### Configuração para o Gemini 2.0-flash

Para usar o modelo Gemini 2.0-flash da Google, adicione sua chave de API no arquivo `.env`:

```
GOOGLE_API_KEY=sua_chave_api_aqui
```

Exemplo de uso da API Gemini 2.0-flash:

```bash
curl "https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=GEMINI_API_KEY" \
-H 'Content-Type: application/json' \
-X POST \
-d '{
  "contents": [{
    "parts":[{"text": "Explain how AI works"}]
    }]
   }'
```

### Configuração para o OpenRouter

O OpenRouter permite acesso a diversos modelos de diferentes provedores através de uma única API. Adicione sua chave de API no arquivo `.env`:

```
OPENROUTER_API_KEY=sua_chave_api_aqui
```

Modelos disponíveis incluem:
- openai/gpt-4o-mini
- openai/gpt-4o-mini-search-preview
- google/gemini-2.0-flash-001
- google/gemini-2.0-pro-exp-02-05:free
- qwen/qwen-vl-plus

### Opção 2: Instalação com Docker

#### Pré-requisitos
- Docker e Docker Compose instalados
  - [Docker Desktop](https://www.docker.com/products/docker-desktop/) (Para Windows/macOS)
  - [Docker Engine](https://docs.docker.com/engine/install/) e [Docker Compose](https://docs.docker.com/compose/install/) (Para Linux)

#### Passos de Instalação
1. Clone o repositório:
```bash
git clone https://github.com/browser-use/web-ui.git
cd web-ui
```

2. Crie e configure o arquivo de ambiente:
- Windows (Prompt de Comando):
```bash
copy .env.example .env
```
- macOS/Linux/Windows (PowerShell):
```bash
cp .env.example .env
```
Edite o arquivo `.env` com seu editor de texto preferido e adicione suas chaves de API.

3. Execute com Docker:
```bash
# Construir e iniciar o contêiner com configurações padrão (navegador fecha após tarefas de IA)
docker compose up --build
```
```bash
# Ou execute com navegador persistente (navegador permanece aberto entre tarefas de IA)
CHROME_PERSISTENT_SESSION=true docker compose up --build
```

4. Acesse a Aplicação:
- Interface Web: Abra `http://localhost:7788` no seu navegador
- Visualizador VNC (para assistir às interações do navegador): Abra `http://localhost:6080/vnc.html`
  - Senha VNC padrão: "youvncpassword"
  - Pode ser alterada configurando `VNC_PASSWORD` no seu arquivo `.env`

## Uso

### Configuração Local
1.  **Execute a WebUI:**
    Após completar os passos de instalação acima, inicie a aplicação:
    ```bash
    python webui.py --ip 127.0.0.1 --port 7788
    ```
2. Opções da WebUI:
   - `--ip`: O endereço IP para vincular a WebUI. O padrão é `127.0.0.1`.
   - `--port`: A porta para vincular a WebUI. O padrão é `7788`.
   - `--theme`: O tema para a interface do usuário. O padrão é `Ocean`.
     - **Default**: O tema padrão com design balanceado.
     - **Soft**: Um esquema de cores suave para uma experiência relaxante.
     - **Monochrome**: Um tema em tons de cinza com cores mínimas para simplicidade e foco.
     - **Glass**: Um design elegante e semi-transparente para uma aparência moderna.
     - **Origin**: Um tema clássico de inspiração retrô para uma sensação nostálgica.
     - **Citrus**: Uma paleta vibrante inspirada em frutas cítricas com cores brilhantes.
     - **Ocean** (padrão): Um tema azul inspirado no oceano proporcionando um efeito calmante.
   - `--dark-mode`: Ativa o modo escuro para a interface do usuário.
3.  **Acesse a WebUI:** Abra seu navegador e navegue até `http://127.0.0.1:7788`.
4.  **Usando Seu Próprio Navegador (Opcional):**
    - Configure `CHROME_PATH` para o caminho executável do seu navegador e `CHROME_USER_DATA` para o diretório de dados do usuário do seu navegador. Deixe `CHROME_USER_DATA` vazio se quiser usar dados de usuário locais.
      - Windows
        ```env
         CHROME_PATH="C:\Program Files\Google\Chrome\Application\chrome.exe"
         CHROME_USER_DATA="C:\Users\SeuUsuario\AppData\Local\Google\Chrome\User Data"
        ```
        > Nota: Substitua `SeuUsuario` pelo seu nome de usuário real do Windows.
      - Mac
        ```env
         CHROME_PATH="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
         CHROME_USER_DATA="/Users/SeuUsuario/Library/Application Support/Google/Chrome"
        ```
    - Feche todas as janelas do Chrome
    - Abra a WebUI em um navegador que não seja o Chrome, como Firefox ou Edge. Isso é importante porque o contexto persistente do navegador usará os dados do Chrome ao executar o agente.
    - Marque a opção "Usar Navegador Próprio" nas configurações do navegador.
5. **Manter o Navegador Aberto (Opcional):**
    - Configure `CHROME_PERSISTENT_SESSION=true` no arquivo `.env`.

### Gerenciamento de Contêineres Docker:
```bash
# Iniciar com navegador persistente
CHROME_PERSISTENT_SESSION=true docker compose up -d

# Iniciar com modo padrão (navegador fecha após tarefas)
docker compose up -d

# Ver logs
docker compose logs -f

# Parar o contêiner
docker compose down
``` 