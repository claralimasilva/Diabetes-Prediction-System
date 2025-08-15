# Diabetes Prediction System

Sistema de **predição de diabetes** com foco em reprodutibilidade e MLOps “lightweight”.  
O projeto organiza dados, experimentos (notebooks), treinamento e uma **aplicação Streamlit** para inferência local, mantendo uma estrutura clara para evoluir do protótipo para produção.

> Estruturado a partir de um template de ciência de dados com Poetry, Streamlit e MkDocs, já incluindo diretórios padrão (`data/`, `models/`, `notebooks/`, `src/`, etc.) e um `app.py` para a interface.

---

## ✨ Principais recursos

- **Pipeline enxuto** para exploração e modelagem (Jupyter/`notebooks/`).
- **Inferência via Streamlit** (`app.py`) para testes rápidos da solução.
- **Estrutura de projeto padronizada** para dados, código, modelos e documentação.
- **Gerenciamento de dependências** com Poetry (ou alternativa com `requirements.txt`).

---

## 🧱 Estrutura do projeto

```
.
├── data/              # Dados (raw/interim/processed/external)
├── docs/              # Documentação MkDocs
├── models/            # Artefatos de modelos serializados
├── notebooks/         # Exploração e experimentos
├── references/        # Dicionários, papers, notas
├── src/               # Código-fonte (data/, model/, deployment/)
│   ├── data/          # Ingestão/limpeza/engenharia
│   ├── model/         # Treino/avaliação/serialização
│   └── deployment/    # Utilitários para servir modelo
├── app.py             # App Streamlit (inferência)
├── pyproject.toml     # Dependências (Poetry)
├── requirements.txt   # Alternativa com pip
└── README.md
```

*Esta estrutura e o `app.py` já existem no repo.*

---

## ⚙️ Como rodar

### Opção A) Usando Poetry (recomendado)
```bash
# 1) Clonar
git clone https://github.com/claralimasilva/Diabetes-Prediction-System.git
cd Diabetes-Prediction-System

# 2) Instalar dependências
poetry install

# 3) Ativar venv
poetry shell

# 4) Rodar o app (inferência)
streamlit run app.py
```

### Opção B) Usando pip/venv
```bash
python -m venv .venv
# Ativar: Windows
.venv\Scripts\activate
# Ativar: Linux/Mac
source .venv/bin/activate

pip install -r requirements.txt
streamlit run app.py
```

> Observação: o repositório já inclui `app.py` e arquivos de dependência para esses fluxos.

---

## Dados

1. **Coloque seu dataset** em `data/raw/` (ex.: `data/raw/diabetes.csv`).  
2. Caso use o conjunto Pima Indians Diabetes (UCI/Kaggle), mantenha as colunas padronizadas (ex.: `Pregnancies, Glucose, BloodPressure, SkinThickness, Insulin, BMI, DiabetesPedigreeFunction, Age, Outcome`), ou ajuste o código de preparação em `src/data/`.

> Dica: padronize tipos/nomes de colunas e trate outliers/valores ausentes antes do treino.

---

## Experimentos e treino

- Use os **notebooks** em `notebooks/` para EDA e experimentos.
- Centralize funções em `src/` para que o notebook chame apenas “orquestradores” (boa prática p/ reuso e testes).
- Ao finalizar um experimento, **salve o modelo** em `models/` (ex.: `models/model.pkl`) e referencie no app Streamlit.

Sugestão de passos:
1. `src/data/`: limpeza, splits (treino/val), engenharia de atributos.
2. `src/model/`: treino (ex.: scikit-learn/XGBoost), avaliação, serialização (`joblib/pickle`).
3. `app.py`: carregar o artefato de `models/` e expor predições.

> A presença de `notebooks/`, `src/` e `models/` já está prevista no repo.

---

## Aplicação (Streamlit)

O `app.py` é a interface para inserir features e obter a predição.  
Após `streamlit run app.py`, acesse o link exibido no terminal e utilize os campos para inferência.

> O arquivo `app.py` já consta no repositório como ponto de entrada da UI.

---

## Métricas recomendadas

- **Classificação binária**: *Accuracy*, **F1-Score**, *Precision*, *Recall*, *ROC AUC*, *Matriz de confusão*.
- Relate também **curvas ROC/PR** e **importância de variáveis** (ex.: `permutation_importance`, SHAP) para interpretabilidade.

---

## Qualidade e estilo

- **Pre-commit**: o repo inclui `.pre-commit-config.yaml`. Ative com:
  ```bash
  pre-commit install
  pre-commit run --all-files
  ```
- **Estruture funções** em `src/` e mantenha notebooks limpos, chamando utilitários.

---

## Stack

- **Linguagem**: Python
- **Modelagem**: scikit-learn / XGBoost (sugeridos)
- **App**: Streamlit
- **Gestão de deps**: Poetry ou `requirements.txt`
- **Docs**: MkDocs (Material) – arquivo `mkdocs.yml` já presente

---

## Roadmap

- [ ] Script CLI para treino e salvamento automático em `models/`
- [ ] Padronizar schema de entrada (pydantic) no `app.py`
- [ ] Adicionar testes unitários básicos em `src/`
- [ ] Pipeline de CI (lint/test) no GitHub Actions
- [ ] Publicar documentação com MkDocs (`docs/`)

---

## Contribuição

1. Faça um fork e crie uma branch: `feature/nome-da-feature`  
2. Siga o estilo do projeto e adicione testes quando possível  
3. Abra um Pull Request descrevendo mudanças e contexto

---

## Licença

MIT. Consulte o arquivo `LICENSE`.

---
