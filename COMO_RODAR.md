# 🚀 Como Rodar o EduGrade Backend

## Pré-requisitos

- Python 3.11+
- Git

## Estrutura de Importação

> [!IMPORTANT]
> O backend usa imports `from backend.app...`. Ele deve ser executado a partir da **pasta pai** do repositório, onde a pasta do repo é referenciada como `backend`.
>
> No Windows, crie uma junction na pasta pai:
> ```powershell
> cmd /c mklink /J "pasta-pai\backend" "pasta-pai\EduGrade-backend"
> ```

## Instalação

```powershell
# 1. Clone e entre na pasta
git clone https://github.com/vivoeasy100/EduGrade-backend.git EduGrade-backend
cd EduGrade-backend

# 2. Crie o ambiente virtual
python -m venv .venv
.venv\Scripts\activate

# 3. Instale as dependências
pip install -r requirements.txt

# 4. Configure o .env
copy .env.example .env
# Edite o .env: DATABASE_URL, SECRET_KEY, CORS_ORIGINS etc.
```

## Rodando

```powershell
# A partir da pasta PAI do repositório (não de dentro de EduGrade-backend/)
cd ..

# Inicia o servidor (banco SQLite criado e populado automaticamente)
.\EduGrade-backend\.venv\Scripts\python.exe -m uvicorn backend.app.main:app --host 0.0.0.0 --port 8000 --reload
```

| URL | Descrição |
|-----|-----------|
| http://localhost:8000 | App (redireciona para login) |
| http://localhost:8000/docs | Swagger UI (documentação interativa) |
| http://localhost:8000/health | Health check (JSON) |

## Contas de demonstração (seed automático)

| Perfil | Usuário | Senha |
|--------|---------|-------|
| Admin | `admin` | `admin123` |
| Admin 2 | `admin2` | `admin123` |
| Professor | `professor` | `prof123` |
| Professor 2 | `professor2` | `prof123` |
| Aluno | `aluno` | `aluno123` |
| Aluno 2 | `aluno2` | `aluno123` |

## Configuração do .env

| Variável | Padrão dev | Descrição |
|----------|-----------|-----------|
| `DATABASE_URL` | `sqlite:///./edugrade.db` | SQLite para dev, PostgreSQL para prod |
| `SECRET_KEY` | — | Chave JWT (mín. 32 chars) |
| `CORS_ORIGINS` | `["http://localhost:8080"]` | Origens permitidas para o frontend |
| `AI_PROVIDER` | `mock` | `mock`, `ollama` ou `fcc_claude` |
| `DEBUG` | `true` | Habilita Swagger e logs detalhados |

## Rodando Testes

```powershell
# A partir da pasta raiz do projeto
.\EduGrade-backend\.venv\Scripts\python.exe -m pytest --cov=backend/app --cov-fail-under=80 -v
```

## Problemas Comuns

| Erro | Causa | Solução |
|------|-------|---------|
| `ModuleNotFoundError: No module named 'backend'` | Rodando de dentro do repo | Execute da pasta pai com junction criada |
| `Connection refused` para PostgreSQL | `.env` apontando para PG | Mude para `sqlite:///./edugrade.db` |
| `CORS error` no browser | Origem do frontend não está no `.env` | Adicione a URL do frontend em `CORS_ORIGINS` |
