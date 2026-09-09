# 📦 Logística × Satisfação no E-commerce Brasileiro (Olist)

> **O que pesa mais na nota do cliente: o atraso na entrega ou o valor do frete?**  
> *Trabalho acadêmico desenvolvido para a disciplina de **Probabilidade e Estatística**.*

---

## 👥 Integrantes do Grupo
* **Cauan Ferreira**
* **Ricardo**
* **Diego**
* **Victor**
* **Camila**
* **Daniel**

---

## 🎯 O Problema de Negócio

No comércio eletrônico, a experiência do consumidor não termina no clique de compra. A etapa pós-venda, em especial a logística (custo e cumprimento de prazo), desempenha papel crítico na percepção de qualidade do serviço.

Este projeto realiza uma **Análise Exploratória de Dados (EDA)** detalhada a partir do conjunto de dados público da **Olist** (maior marketplace brasileiro), com o objetivo de responder à seguinte questão central:

> *"Até que ponto os gargalos logísticos (tempo de entrega e valor do frete) ditam a satisfação do cliente (nota de 1 a 5) em diferentes regiões do Brasil?"*

---

## 🧪 Hipóteses Investigadas

| Hipótese | Descrição | Metodologia Aplicada |
| :--- | :--- | :--- |
| **H1: Prazo vs. Frete** | O tempo de entrega exerce impacto substancialmente superior sobre a nota de avaliação do que o valor do frete cobrado. | Estatística descritiva, visualizações (Boxplots/Histogramas) e **Correlação Não Paramétrica de Spearman**. |
| **H2: Barreira Regional e Sobrevivência** | Estados do Norte e Nordeste enfrentam fretes médios superiores e maiores índices de pedidos não entregues/falhas. | Mapeamento regional de fretes e diagnóstico percentual de falhas/cancelamentos por estado (**análise do viés de sobrevivência**). |
| **H3: Sensibilidade por Categoria** | Categorias com maior valor agregado ou expectativas emocionais sofrem maior penalização em atrasos severos. | Segmentação de categorias de produto (agregação com tratamento de pedidos multicategoria) e análise de notas médias em pedidos com atraso crítico (**> 28,5 dias**). |

---

## 📊 Principais Resultados e Métricas

### 1. Estatística Descritiva da Operação Logística
* **Tempo de Entrega:** Média de **12,09 dias** e mediana de **10,00 dias** ($DP = 9,55$ dias; cauda longa de até 209 dias). O limite superior do IQR é de **28,50 dias** (5,2% de pedidos anômalos/atrasos severos).
* **Valor do Frete:** Média de **R$ 22,79** e mediana de **R$ 17,17** ($DP = R\$\ 21,56$).

### 2. Comprovação Numérica da Hipótese 1 (Spearman)
* **Amostra Analisada:** 95.830 pedidos entregues e avaliados.
* **Spearman Tempo × Nota:** `r = -0.235` (associação negativa moderada — o cliente penaliza fortemente a demora).
* **Spearman Frete × Nota:** `r = -0.088` (associação fraca — o consumidor aceita pagar mais desde que receba rápido).
* **Multicolinearidade (Frete × Tempo):** `r = +0.381`.
* **Medianas Reais por Nota de Avaliação:**
  * **Nota 1:** Mediana de entrega = **16 dias** | Mediana de frete = **R$ 18,76**
  * **Nota 5:** Mediana de entrega = **9 dias** | Mediana de frete = **R$ 16,79**

### 3. Diagnóstico de Falhas e Disparidades Regionais (H2)
* **Pedidos sem entrega registrada:** 2.965 pedidos (3,0% do total da base).
* **Destaques com relevância estatística:** Estados do Nordeste como **Ceará (2,84% de falha)**, **Sergipe (2,57%)** e **Maranhão (2,28%)** apresentam taxas elevadas de falhas combinadas com médias de frete consideravelmente superiores ao Sul/Sudeste.
* *Ressalva amostral:* Roraima apresenta 8,70% de taxa de falha nominal, porém com volume total de apenas 46 pedidos na base histórica.

### 4. Sensibilidade ao Atraso por Categoria de Produto (H3)
Entre os pedidos com atraso crítico (> 28,5 dias de entrega):
* **Mais penalizadas na nota média (piores notas):**
  1. `instrumentos_musicais`: média **2,03**
  2. `fashion_bolsas_e_acessorios`: média **2,05**
  3. `construcao_ferramentas_construcao`: média **2,10**
  4. `cama_mesa_banho`: média **2,15**
* **Mais tolerantes ao atraso (melhores notas):**
  1. `moveis_escritorio`: média **2,84**
  2. `telefonia`: média **2,51**
  3. `consoles_games`: média **2,50**

---

## 💡 Recomendações Estratégicas de Negócio

1. **Priorização de Prazo sobre Desconto de Frete:** Campanhas de subsídio generalizado de frete geram baixo retorno na satisfação final. O investimento deve ser direcionado para otimização de malha e redução do tempo em trânsito.
2. **Parcerias com Operadores Regionais:** Estabelecer acordos com transportadoras especializadas nas rotas Norte e Nordeste para mitigar as taxas de insucesso e fretes exorbitantes.
3. **Gatilho Proativo de Pós-Venda (28,5 dias):** Implementação de alerta automático no sistema de CRM: pedidos que atinjam o limiar estatístico de 28,5 dias em trânsito devem disparar automaticamente um contato proativo com cupom de desconto ou estorno parcial do frete antes mesmo da avaliação do cliente.

---

## 🗂️ Estrutura do Repositório

```text
├── eda_olist.ipynb          # Notebook Jupyter consolidado com todas as análises e gráficos
├── requirements.txt         # Dependências do ambiente Python
├── .gitignore               # Regras de exclusão do Git
├── README.md                # Documentação executiva e técnica do projeto
└── Dataset/                 # Arquivos CSV da base Olist (ver instruções de download abaixo)
    ├── olist_orders_dataset.csv
    ├── olist_order_items_dataset.csv
    ├── olist_order_reviews_dataset.csv
    ├── olist_customers_dataset.csv
    └── olist_products_dataset.csv
```

---

## 🚀 Como Executar o Projeto Localmente

### 1. Clonar o repositório
```bash
git clone https://github.com/Cauan-Almeida/eda-olist-logistica-satisfacao.git
cd eda-olist-logistica-satisfacao
```

### 2. Criar e ativar o ambiente virtual (Python 3.10+)
```bash
# Linux/macOS:
python3 -m venv .venv
source .venv/bin/activate

# Windows:
python -m venv .venv
.venv\Scripts\activate
```

### 3. Instalar as dependências
```bash
pip install -r requirements.txt
```

### 4. Obter a base de dados
Os dados utilizados são do [Brazilian E-Commerce Public Dataset by Olist no Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce).  
Basta extrair os arquivos `.csv` dentro da pasta `Dataset/` na raiz do projeto.

### 5. Abrir e executar o Notebook
```bash
jupyter notebook eda_olist.ipynb
```
*(Ou abra diretamente no VS Code / Jupyter Lab).*

---

## 🛠️ Tecnologias e Bibliotecas Utilizadas
* **Python 3**
* **Pandas** — Engenharia de recursos, tratamento e agregações multidimensionais
* **Matplotlib & Seaborn** — Visualizações gráficas estatísticas (boxplots, contagens e histogramas)
* **SciPy** — Estatística inferencial e correlação de postos de Spearman
* **Jupyter Notebook** — Ambiente iterativo de análise e apresentação

---

## 📄 Licença
Este projeto foi desenvolvido estritamente para fins acadêmicos e educacionais.
