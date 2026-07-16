
# 🎮 Retro Car Predictor — README

> **INSERT COIN** — Preveja o preço de carros clássicos e usados com um toque retrô de arcade!

---

## 🌐 Links do Projeto

- **Site (frontend):** [1]
- **API (backend):** [2]

> ✅ Este projeto foi **desenvolvido por Emilly**. Todos os créditos e a autoria pertencem a criadora desta aplicação.

---

## 📖 Sobre

O **Retro Car Predictor** é uma aplicação web com tema de arcade que permite estimar o preço de mercado de carros usados com base em quatro características principais:

- Ano de fabricação
- Quilometragem
- Motorização (cilindrada)
- Número de revisões

O **frontend** — acessível em [1] — apresenta uma interface retrô com dropdowns e sliders estilizados. Ao clicar em **▶ PREVER PREÇO**, os dados são enviados via requisição `POST` para o **backend**, que retorna a estimativa de preço calculada por um modelo de Machine Learning.

O **backend** é uma API REST construída com **Flask** e utiliza um modelo de **Regressão Linear** do scikit-learn, treinado em um dataset de carros usados.

---

## 🛠️ Tecnologias Utilizadas

| Camada | Tecnologia |
|---|---|
| **Backend** | Flask (Python 3.8+) |
| **Machine Learning** | scikit-learn (`LinearRegression`) |
| **Manipulação de dados** | pandas |
| **CORS** | flask-cors |
| **Frontend** | HTML / CSS / JavaScript |
| **Hospedagem** | [3] |

---

## 🧠 Como Funciona o Modelo de ML

O modelo é um **Regressor Linear** treinado a partir do arquivo `dataset_carros_usados_.csv`, que deve conter as seguintes colunas:

| Coluna | Tipo | Descrição |
|---|---|---|
| `ano` | `int` | Ano de fabricação do veículo |
| `quilometragem` | `int` ou `float` | Quilômetros rodados |
| `motor` | `float` | Cilindrada do motor (ex: `1.0`, `1.4`, `1.6`, `1.8`, `2.0`) |
| `num_revisoes` | `int` | Quantidade de revisões realizadas |
| `preco` | `float` | Preço de mercado (variável alvo) |

O treinamento é executado na inicialização do app:

```python
from sklearn.linear_model import LinearRegression
import pandas as pd

df = pd.read_csv("dataset_carros_usados_.csv")
modelo = LinearRegression()

X = df[["ano", "quilometragem", "motor", "num_revisoes"]]
y = df["preco"]

modelo.fit(X, y)
```

---

## 📡 Endpoints da API

A API está disponível em: [2]

---

### `GET /`

Verifica se a API está online e funcionando.

**Resposta de exemplo:**
```json
{
  "Status": "API online e funcionando corretamente!",
  "Autor": "Você"
}
```

---

### `POST /prever`

Recebe os dados de um carro e retorna a previsão de preço.

**Endpoint:** [4]

**Payload JSON esperado:**
```json
{
  "ano": 2015,
  "quilometragem": 85000,
  "motor": 1.6,
  "num_revisoes": 4
}
```

**Resposta de sucesso:**
```json
{
  "Preço": 48500.75
}
```

**Resposta de erro (HTTP 400):**
```json
{
  "erro": "KeyError('ano')"
}
```

---

## 🚀 Como Rodar Localmente

### Pré-requisitos

- Python 3.8 ou superior
- pip (gerenciador de pacotes)

### 1. Instalar as dependências

```bash
pip install flask flask-cors scikit-learn pandas
```

### 2. Preparar o dataset

Garanta que o arquivo **`dataset_carros_usados_.csv`** esteja no diretório raiz do projeto, contendo as colunas:

> `ano`, `quilometragem`, `motor`, `num_revisoes`, `preco`

> ⚠️ O nome do arquivo deve ser **exatamente** `dataset_carros_usados_.csv` (com o `_` no final), conforme o código.

### 3. Iniciar o servidor

```bash
python app.py
```

O backend ficará disponível em **[5] (ou `[6] na rede local).

---

## 🧪 Exemplo de Requisição (cURL)

```bash
curl -X POST [4] \
  -H "Content-Type: application/json" \
  -d '{
    "ano": 2019,
    "quilometragem": 35000,
    "motor": 1.4,
    "num_revisoes": 2
  }'
```

**Resposta esperada:**
```json
{
  "Preço": 62345.92
}
```

---

## 📊 Sobre o Dataset

- **Quantidade:** Recomenda-se ao menos **100 amostras** para resultados minimamente confiáveis.
- **Qualidade:** Dados realistas e atualizados geram previsões mais precisas.
- **Diversidade:** Inclua variedade de anos, motores e faixas de quilometragem.
- **Sem nulos:** As colunas usadas pelo modelo não devem conter valores ausentes.

> 💡 **Para melhorar o modelo:** adicione mais features (marca, modelo, combustível, etc.) e ajuste a variável `X` no código.

---

## 👤 Desenvolvedor

**Desenvolvido por Emilly** 🚀

Todos os direitos e créditos pertencem ao autor original desta aplicação.

---

## 📄 Licença

*(Não especificada. Recomenda-se adicionar um arquivo `LICENSE` — ex: MIT ou Apache 2.0 — para definir os termos de uso e distribuição.)*

---

*README gerado com auxílio do Sabiá-4, mantendo links ativos e autoria atribuída a você.*

## Referências

[1] https://retro-car-predictor.lovable.app - https://retro-car-predictor.lovable.app
[2] https://retro-car-predictor.lovable.app/ - https://retro-car-predictor.lovable.app/
[3] Lovable - https://lovable.app
[4] https://retro-car-predictor.lovable.app/prever - https://retro-car-predictor.lovable.app/prever
[5] http://localhost:8000** - http://localhost:8000**
[6] http://0.0.0.0:8000` - http://0.0.0.0:8000`
