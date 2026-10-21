# 🛒 Food Delivery App: Funnel Analysis & A/A/B Hypothesis Testing

![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=flat-square&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-1.3+-150458?style=flat-square&logo=pandas&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-Statistics-8CA1AF?style=flat-square&logo=scipy&logoColor=white)
![Status](https://img.shields.io/badge/Status-Conclu%C3%ADdo-brightgreen?style=flat-square)

---

## 📌 Apresentação do Projeto

Este projeto foi desenvolvido para uma startup do setor de retalho e distribuição de produtos alimentícios que opera através de um aplicativo móvel. 

O estudo é dividido em duas vertentes estratégicas de Data Science:
1. **Mapeamento e Diagnóstico do Funil de Eventos:** Identificação do fluxo ideal de navegação do usuário, medição da taxa de conversão em cada etapa consecutiva e localização do gargalo onde há maior perda de potenciais compradores.
2. **Validação Estatística de Experimento A/A/B:** Avaliação científica do impacto da alteração global das fontes tipográficas do aplicativo em relação ao comportamento de compra dos usuários.

---

## 🛠️ Tecnologias e Bibliotecas Utilizadas

* **Linguagem:** Python 3.9+
* **Manipulação e Análise de Dados:** `pandas`, `numpy`
* **Inferência Estatística:** `scipy.stats` (Teste Z de Proporções, Distribuição Normal Padrão)
* **Visualização de Dados:** `matplotlib`, `seaborn`
* **Ambiente de Desenvolvimento:** Jupyter Notebook

---

## ⚙️ Metodologia e Etapas da Análise

1. **Inspeção e Auditoria dos Dados (Data Wrangling):**
   * Inspeção inicial de metadados de 244.126 registros brutos.
   * Padronização de nomes de colunas para `snake_case`.
   * Verificação de valores nulos e remoção de registros duplicados (~0,17%).
   * Conversão de timestamps no formato Unix (segundos) para objetos nativos de data/hora (`datetime64[ns]`).

2. **Análise de Consistência Temporal:**
   * Avaliação da distribuição temporal dos eventos por histograma dinâmico.
   * Filtro de registros incompletos, retendo os dados com amostragem integral entre **01/08/2019 e 07/08/2019** (retenção de 98,84% dos eventos e 99,77% dos usuários).

3. **Análise e Modelagem do Funil de Vendas:**
   * Mapeamento do fluxo cronológico: `MainScreenAppear` ➔ `OffersScreenAppear` ➔ `CartScreenAppear` ➔ `PaymentScreenSuccessful`.
   * Exclusão do evento `Tutorial` por se tratar de um fluxo opcional assistencial (~11% de engajamento).
   * Cálculo das taxas de conversão por etapa consecutiva e da taxa de conversão global (end-to-end).

4. **Inferência Estatística e Testes de Hipóteses (A/A/B):**
   * **Teste A/A de Sanidade:** Validação da divisão homogênea entre os grupos de controle `246` e `247`.
   * **Testes A/B:** Comparação do grupo de teste `248` (novas fontes) contra os controles isolados e contra o grupo de controle unificado (`246` + `247`).
   * **Aplicação do Teste Z de Duas Proporções** (amostras independentes, bicaudal).
   * **Controle de Falsos Positivos:** Correção de Bonferroni para ajustar o nível de significância estatística ($\alpha = 0{,}05 / 16 = 0{,}003125$).

---

## 📊 Resultados e Insights Obtidos

### 1. Funil de Vendas e Conversão

| Etapa do Funil | Usuários Únicos | Conversão (Etapa Anterior) | Conversão Acumulada |
| :--- | :---: | :---: | :---: |
| **MainScreenAppear** (Home) | 7.419 | 100,00% | 100,00% |
| **OffersScreenAppear** (Ofertas) | 4.593 | **61,91%** | 61,91% |
| **CartScreenAppear** (Carrinho) | 3.734 | 81,30% | 50,33% |
| **PaymentScreenSuccessful** (Pagamento) | 3.539 | **94,78%** | **47,70%** |

* 🚨 **Gargalo Principal:** A maior perda de usuários ocorre na transição da **Tela Principal ➔ Tela de Ofertas** ($38,09\%$ de abandono imediato).
* 🔥 **Força de Retenção:** Uma vez na tela de ofertas, $81,30\%$ avançam para o carrinho e $94,78\%$ dos que chegam ao carrinho concluem a compra.
* 📈 **Taxa de Conversão Final:** $47,70\%$ dos usuários que entram na Home concluem o pagamento.

---

### 2. Resultados do Teste A/A/B (Nova Tipografia)

* **Validação do Teste A/A (Grupos 246 vs 247):** Nenhum evento apresentou diferença estatisticamente significativa ($p > 0{,}05$), confirmando a correta alocação aleatória dos usuários.
* **Resultado dos Testes A/B (248 vs Controles):** Todos os $p$-valores calculados nas comparações individuais e combinadas permaneceram acima de $0{,}05$.
* **Conclusão Estatística:** Mesmo com a Correção de Bonferroni ($\alpha = 0{,}003125$), a alteração de fontes **não apresentou qualquer impacto significante** (positivo ou negativo) nas taxas de conversão de nenhuma etapa do funil.

---

## 💡 Recomendações Estratégicas

* **Design (UI/UX):** A alteração de fontes pode ser implementada com segurança, pois demonstrou ser neutra para o comportamento de compra dos usuários.
* **Equipe de Produto:** Concentrar os esforços de otimização na transição **Home ➔ Ofertas** (onde se perdem $38\%$ dos clientes), testando novos elementos visuais, chamadas para ação (CTAs) e vitrines de produtos na página inicial.
* **Growth Marketing:** Criar campanhas de engajamento direcionadas aos usuários que abandonam o app na Tela Principal antes de visualizar o catálogo.

---

## 📁 Estrutura do Repositório

```text
├── datasets/
│   └── logs_exp_us.csv          # Base de dados de logs do experimento (git-ignored)
├── .gitignore                   # Arquivo de exclusões do Git
├── requirements.txt             # Dependências e bibliotecas do projeto
├── notebook.ipynb               # Jupyter Notebook com a análise completa
└── README.md                    # Documentação técnica do projeto
```

---

## 👨‍💻 Autor

* **Luiz Almeida**
* Projeto desenvolvido como parte da formação em **Data Analytics — TripleTen**.
