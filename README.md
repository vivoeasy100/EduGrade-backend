# EduGrade Backend

API RESTful do EduGrade construída com FastAPI, responsável por toda a lógica de negócio, autenticação, banco de dados, OCR, IA e processamento de arquivos.

## 🚀 Tecnologias

- **FastAPI** - Framework web moderno e rápido
- **SQLAlchemy** - ORM assíncrono
- **Alembic** - Migrations de banco de dados
- **Pydantic** - Validação de dados
- **Tesseract OCR** - Reconhecimento óptico de caracteres
- **OpenAI API** - Correção automática com IA
- **Pytest** - Testes automatizados (cobertura ≥ 80%)

## 📁 Estrutura

```
backend/
├── app/
│   ├── api/routes/        # Rotas da API (REST)
│   ├── core/              # Config, security, database
│   ├── models/            # Modelos SQLAlchemy
│   ├── repositories/      # Camada de acesso a dados
│   ├── schemas/           # Schemas Pydantic (validação)
│   ├── services/          # Lógica de negócio
│   └── integrations/      # OCR, IA, Email, Storage, PDF, QR
├── migrations/            # Alembic migrations
└── tests/                 # Testes unitários e integração
```

## ⚙️ Configuração

```bash
# 1. Clone o repositório
git clone https://github.com/vivoeasy100/EduGrade-backend.git
cd EduGrade-backend

# 2. Crie o ambiente virtual
python -m venv .venv
source .venv/bin/activate  # Linux/Mac
# .venv\Scripts\activate   # Windows

# 3. Instale dependências
pip install -r requirements.txt

# 4. Configure variáveis de ambiente
cp .env.example .env
# Edite .env com suas credenciais

# 5. Execute migrations
alembic upgrade head

# 6. Inicie o servidor
uvicorn app.main:app --reload
```

## 🌐 Endpoints Principais

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/docs` | Documentação Swagger UI |
| GET | `/api/v1/health` | Health check |
| POST | `/api/v1/auth/login` | Login |
| GET | `/api/v1/exams` | Listar provas |
| POST | `/api/v1/exams` | Criar prova |
| POST | `/api/v1/imports` | Importar provas (OCR) |
| GET | `/api/v1/jobs/{id}` | Status de jobs |

## 🧪 Testes

```bash
# Rodar todos os testes com cobertura
pytest --cov=app --cov-fail-under=80 -v

# Rodar testes específicos
pytest tests/unit/test_auth.py -v
```

## 📦 Deploy

- **Railway/Render**: Conecte o repo e configure as variáveis de ambiente
- **Docker**: `docker build -t edugrade-backend .`
- **Variáveis obrigatórias**: `DATABASE_URL`, `SECRET_KEY`, `CORS_ORIGINS`

## 🔗 Frontend

Repositório separado: [EduGrade-frontend](https://github.com/vivoeasy100/EduGrade-frontend)

O frontend consome esta API via `API_BASE_URL` configurável via `.env`.