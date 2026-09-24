# Netflix Content Analytics 🎬

Projeto de portfólio de análise de dados usando o dataset público **Netflix Movies and TV Shows** (Kaggle), com tratamento em Python, armazenamento em SQLite e visualização em um dashboard interativo no Power BI.

Este projeto foi pensado como uma introdução prática ao fluxo completo de um projeto de dados: da exploração e limpeza até a entrega de um dashboard com storytelling visual.

---

## 🎯 Perguntas de negócio respondidas

1. Quantos títulos existem no catálogo?
2. Quantos são filmes e quantos são séries?
3. Como o catálogo cresceu ano a ano?
4. Quais países produzem mais conteúdo no catálogo?
5. Quais gêneros são mais comuns?
6. Qual é a classificação etária (rating) mais frequente?
7. Qual é a duração média dos filmes?
8. Qual é o número médio de temporadas das séries?
9. Existe relação entre o ano de lançamento e o gênero mais comum?

---

## 🗂️ Estrutura do projeto

```
├── dados/
│   ├── netflix.db                  # Banco SQLite com os dados tratados
│   └── netflix_titles_tratado.csv  # Dataset limpo, pronto para consumo no Power BI
├── cadernos/
│   └── exploracao.ipynb            # Exploração, limpeza e tratamento dos dados em Python
├── NETFLIX.pbix                    # Dashboard interativo no Power BI
├── .gitattributes
└── README.md
```

---

## 🛠️ Tecnologias utilizadas

- **Python (Pandas)** — exploração, limpeza e tratamento dos dados (`cadernos/exploracao.ipynb`)
- **SQLite** — armazenamento estruturado dos dados tratados (`dados/netflix.db`)
- **Power BI + DAX** — modelagem, medidas calculadas e dashboard interativo (`NETFLIX.pbix`)

---

## 📊 Sobre o dashboard

O dashboard (`NETFLIX.pbix`) foi construído com identidade visual inspirada na marca Netflix (preto, cinza e vermelho `#E50914`), e inclui:

- **Cartões de KPI**: Total de Títulos, Total de Filmes, Total de Séries, Total de Países, Duração Média (Filmes), Média de Temporadas (Séries)
- **Evolução do catálogo por ano**: gráfico de colunas com gradiente de cor destacando os anos mais recentes, tooltip customizado (ano, quantidade de títulos e variação % em relação ao ano anterior) e gridlines limpas
- **Distribuição Filmes x Séries**: gráfico de rosca (donut)
- **Total de Títulos por país**: gráfico de barras com o país líder destacado em vermelho
- **Principais gêneros**: gráfico de barras com o gênero líder destacado em vermelho
- **Classificação etária (rating) mais frequente**: gráfico de barras ordenado, com o rating líder destacado
- Formatação visual consistente: fundo claro, cartões com sombra sutil e cantos arredondados

### Medidas DAX principais

```dax
Total de Títulos = COUNTROWS(netflix_titles_tratado)

Total de Filmes = CALCULATE([Total de Títulos], netflix_titles_tratado[type] = "Movie")

Total de Séries = CALCULATE([Total de Títulos], netflix_titles_tratado[type] = "TV Show")

Duração Média (Filmes) = 
CALCULATE(AVERAGE(netflix_titles_tratado[duracao_minutos]), netflix_titles_tratado[type] = "Movie")

Média de Temporadas (Séries) = 
CALCULATE(AVERAGE(netflix_titles_tratado[temporadas]), netflix_titles_tratado[type] = "TV Show")

Var % Ano Anterior = 
VAR AnoAtual = SELECTEDVALUE(netflix_titles_tratado[release_year])
VAR TitulosAnoAnterior = 
    CALCULATE([Total de Títulos], FILTER(ALL(netflix_titles_tratado), netflix_titles_tratado[release_year] = AnoAtual - 1))
RETURN
DIVIDE([Total de Títulos] - TitulosAnoAnterior, TitulosAnoAnterior)
```

Também foram criadas medidas de formatação condicional (`Cor Coluna`, `Cor País`, `Cor Gênero`, `Cor Rating`) para destacar dinamicamente o item de maior valor em cada gráfico.

---

## 🚀 Como reproduzir

1. Clone este repositório
2. Explore o tratamento dos dados em `cadernos/exploracao.ipynb`
3. Os dados tratados já estão disponíveis em `dados/netflix_titles_tratado.csv` e `dados/netflix.db`
4. Abra `NETFLIX.pbix` no Power BI Desktop para visualizar e interagir com o dashboard

---

## 📌 Status

Projeto em desenvolvimento — próximos passos incluem uma análise cruzada entre ano de lançamento e gênero (pergunta 9) e uma tabela de atores com mais participações no catálogo.

---

## 👤 Autor

**Caio Antunes**
Em transição de carreira para Análise de Dados / BI / Engenharia de Dados.