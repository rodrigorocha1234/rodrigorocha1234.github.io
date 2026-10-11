---
layout: project
title: "Usado multiagentes no google antigravity para construir um sistema de Previsão inteligente de preço de apartamento para a cidade de Ribeirão Preto"
date: 2026-10-11
image: /assets/img/posts/ml_apartamentos_rp/tumb.png
description: "Proposta de sistema de previsão de preço para apartamentos em Ribeirão Preto"
tags: ['python', 'docker', 'grafana', 'machine_learning', 'mlops', 'regressao', 'Ribeirão Preto', 'Apartamento', 'multiagentes', 'padrão_de_projeto', 'google antigravity']
---


## 1 – Introdução

O objetivo desse projeto é orquestrar vários agentes usando o google antigravity para construção de um sistema de precificação imobiliária de apartamentos da cidade de Ribeirão Preto.

## 2 – Tecnologias usadas




- 🐍 Python
- 🐳 Docker
- 🧪 Mlflow
- 🤖 Sklearn

## 3 -  Requisitos dos Sistemas:

### 3.1 – Equipe multiagente e especificações formais (ESPECS)

O projeto foi concebido e implementado sob uma governança multiagente estrita. Cada aspecto do sistema — desde a concepção dos requisitos de negócio até a infraestrutura de contêineres — é gerido por agentes de inteligência artificial especializados com responsabilidades delimitadas, barreiras de segurança (*guardrails*) e validação cruzada contínua através de especificações formais (specs/) e regras inegociáveis de código (rules/).

#### 3.1.1 - **A Equipe de 7 Agentes Especializados (.agents/agents.md)**

Nenhum agente opera de forma generalista ou arbitrária. A segregação de funções impede sobreposição de escopo e garante auditoria completa em cada commit:

**@pmProduct Manager**  
** Lead Architect & Especificações Auditáveis**  
** Missão: Traduz as necessidades comerciais em requisitos formais auditáveis. Consolida `specs/` e `rules/`, gerencia o Approval Gate e preserva o isolamento entre Inner CV, Outer CV e Holdout.**  
** 🚫 Restrições Rígidas: Não escreve código de produção; não altera regras sem aval humano; proíbe terminantemente FastAPI (exige MLflow Serving nativo).**

**@ml_architectArquiteto de ML**  
** Contratos GoF & Tipagem Estrita**  
** Missão: Define a arquitetura do pipeline, tipagem estática (Protocols, TypeVar, Generic), padrões de projeto (Factory, Adapter, Repository, Strategy, Observer) e organização modular de pacotes em português.**  
** 🚫 Política "No-If": Proibido usar `if`, `elif` ou `match` para decisões de domínio/arquitetura. Exige polimorfismo, dispatch tables ou Chain of Responsibility.**

**@data_engineerEngenheiro de Dados**  
** Ingestão, Staging & Detecção de Drift**  
** Missão: Responsável por ingestão de fontes heterogêneas, validação de contratos de dados (Quality Gate), persistência imutável em staging SQLite, análise descritiva e testes de estabilidade (KS, PSI, Wasserstein).**  
** 🚫 Vetorização Pura: Proibido processamento linha a linha em Pandas (banidos: `iterrows`, `itertuples` e loops manuais).**

**@ml_engineerEngenheiro de ML**  
** Nested CV, Tuning & Ensembles**  
** Missão: Implementa pré-processamento anti-leakage, orquestra Nested Cross-Validation (15 folds externos × 5 internos), gerencia busca de hiperparâmetros (Grid e Random Search), auditoria de resíduos e comitê de modelos.**  
** 🚫 Zero Hardcode: Todos os hiperparâmetros e espaços de busca vêm de arquivos YAML. Obrigatório traduzir parâmetros para linguagem de negócio após treino.**

**@mlopsMLOps & Observabilidade**  
** Registry, Serving & Telemetria**  
** Missão: Gerencia o MLflow Tracking (runs pai/filho), registra artefatos sob o alias `@champion` no MLflow Registry, configura o servidor de inferência com adaptador ASGI e provê métricas OpenMetrics para Prometheus e Grafana.**  
** 🚫 Cardinalidade Controlada: Proibido uso de labels de alta cardinalidade no Prometheus; garante desacoplamento de storage de artefatos (S3/RustFS).**

**@qaQA & Security Auditor**  
** Compliance, Regras & Auditoria de PR**  
** Missão: Atua como o fiscal implacável do projeto. Audita o código contra as `specs/` e `rules/`, verificando tipagem estática com MyPy, integridade de testes com PyTest e conformidade arquitetural.**  
** 🚫 Bloqueios Fatais: Rejeita sumariamente código com uso de `Any`, decisões de domínio com `if`, leitura prematura do holdout ou ausência de testes.**

**@devopsDevOps & Infra**  
** Docker Compose, Resiliência & Healthchecks**  
** Missão: Orquestra a infraestrutura local e em nuvem via Docker Compose. Gerencia microsserviços (PostgreSQL, RustFS S3, MLflow, Prometheus, Grafana, Loki e Alloy), assegurando readiness, healthchecks e scripts reproduzíveis.**  
** 🚫 Reprodutibilidade Obrigatória: Todo o ambiente deve subir com um único comando declarativo (`docker compose up -d`) sem intervenções manuais.**

### 3.1.2 -  As 4 Especificações Formais do Sistema (specs/)

**Contratos Técnicos Auditáveis**

Cada documento em `specs/` atua como o contrato canônico do sistema, definindo escopo, premissas matemáticas e evidências de validação:

**Arquivo:** `01_pipeline_ml.md`

**Título da Especificação:** **Spec 01 — Pipeline de ML**

**Escopo Técnico & Requisitos Obrigatórios:** Orquestração sequencial de 20 etapas determinísticas. Particionamento treino/holdout (80/20) com semente 42. Nested Cross-Validation com `RepeatedKFold` externo (5×3) e `KFold` interno (5 splits). Auditoria estatística com testes de Shapiro-Wilk, Friedman, Nemenyi e Tukey.

**Garantia de Governança:** **Isolamento de Holdout & Anti-Leakage**

---

**Arquivo:** `02_modelos_tuning.md`

**Título da Especificação:** **Spec 02 — Modelos & Tuning**

**Escopo Técnico & Requisitos Obrigatórios:** Fábrica com suporte a até 10 algoritmos de regressão (Lineares, Ridge, Lasso, ElasticNet, Árvores, Random Forest, SVR, MLP, XGBoost, CatBoost). Busca adaptativa via `GridSearchCV` e `RandomizedSearchCV` parametrizada em YAML. Montagem de comitê `VotingRegressor` ponderado.

**Garantia de Governança:** **Tuning Declarativo & Rastreabilidade**

---

**Arquivo:** `03_dados_negocio.md`

**Título da Especificação:** **Spec 03 — Dados & Regras de Negócio**

**Escopo Técnico & Requisitos Obrigatórios:** Definição da variável alvo (`Valor_da_Venda`). Enriquecimento hierárquico em 3 níveis (Global, Zona, Bairro). Validador de suficiência amostral (mínimo 30 amostras na Zona e 20 no Bairro) com fallback geográfico. Corredores de segurança (-10%/+10%) e descontos escalonados (5%, 10%, 15%).

**Garantia de Governança:** **Defesa Patrimonial & Coerência**

---

**Arquivo:** `04_observabilidade.md`

**Título da Especificação:** **Spec 04 — Observabilidade & Serving**

**Escopo Técnico & Requisitos Obrigatórios:** Servidor de inferência nativo no MLflow Serving com adaptador ASGI de telemetria na porta 8080. Exposição de 56 métricas nativas do Prometheus na porta 8000. Persistência atômica `treino.prom` para painéis Grafana contínuos. Separação rigorosa entre métricas de treino e observações de produção.

**Garantia de Governança:** **Telemetria em Tempo Real (SLA < 150ms)**

###  3.1.3 - As 4 Regras Inegociáveis de Arquitetura (rules/)

**Padrões Verificados pelo Auditor @qa**

Diretrizes estritas aplicadas na base de código para manter excelência de engenharia de software e eliminar dívida técnica:

**Regra 01: Python 3.12 Estrito & Sem Any**\
`rules/01_python_rules.md`

Código com tipagem estática absoluta (dataclasses congeladas, tuplas imutáveis, Protocols e genéricos). Uso de `Any` é proibido sem autorização explícita. Exatamente uma classe principal por arquivo para alta coesão e baixo acoplamento.

**Regra 02: Política "No-If" em Regras de Domínio**\
`rules/02_no_if_rules.md`

Decisões de domínio não utilizam cascatas de `if`/`elif`/`match`. Substituídas por padrões GoF: *Strategy*, *State*, *Specification*, *Dispatch Tables* e polimorfismo, viabilizando extensibilidade sem modificação de código consolidado (OCP).

**Regra 03: Vetorização Pura em Pandas**\
`rules/03_pandas_rules.md`

Processamento de dados exclusivamente por operações colunares vetorizadas em C/NumPy. Proibição estrita de `iterrows()`, `itertuples()` ou `apply(axis=1)`, garantindo velocidade máxima e baixo consumo de memória.

**Regra 04: Governança de ML & Anti-Leakage**\
`rules/04_ml_rules.md`

Hiperparâmetros estritamente externos (YAML). Todo pré-processamento (imputação, encoding, scaling) deve ocorrer estritamente dentro do Pipeline/ColumnTransformer de cada fold. O cofre de holdout permanece bloqueado até o congelamento da versão.

### 3.2 – Requisitos funcionais:

 | ID | Requisito Funcional | Descrição Técnica & Comportamento Esperado | Módulo Responsável | 
 | --------- | ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------- | 
 | **RF-01** | **Ingestão de Dados & Anti-Leakage** | Carregar dataset de **5.712 apartamentos** (`dados/bairro_final_v3_engineered.xlsx`) e purgar imediatamente colunas com risco de vazamento de target (`Código`, `Apartamento`, `valor_m2`, médias locais de m²). | `CarregadorExcel` | 
 | **RF-02** | **Validação de Contrato & Quality Gate** | Validar a presença da coluna alvo (`Valor`), integridade de tipos e limites físicos estritos (metragem > 0, quartos ≥ 0, banheiros ≥ 0, vagas ≥ 0), emitindo métricas de qualidade ao Prometheus. | `ValidadorContrato` | 
 | **RF-03** | **Persistência em Staging SQLite** | Persistir snapshot integral e imutável dos dados brutos validados na tabela SQLite `apartamentos_staging` para rastreabilidade, auditoria e reprodutibilidade histórica. | `RepositorioStaging` | 
 | **RF-04** | **Isolamento em Cofre de Holdout** | Particionar a base em **80% treino / 20% teste cego**, com semente determinística fixa (`42`). Bloquear a partição de 20% no `CofreHoldout`, proibindo leitura durante EDA, CV e tuning. | `CofreHoldout` | 
 | **RF-05** | **Análise Exploratória & Detecção de Drift** | Calcular estatísticas descritivas sobre os 80% de treino e quantificar estabilidade distributiva via testes **Kolmogorov-Smirnov (KS)**, **PSI** e **distância de Wasserstein** para variáveis numéricas contínuas. | `DetectorDrift` | 
 | **RF-06** | **Nested Cross-Validation (15×5 Folds)** | Avaliar modelos em **15 folds externos** (`RepeatedKFold`: 5 splits × 3 repetições) e ajustar hiperparâmetros em **5 folds internos** (`KFold`), mantendo imputação, codificação e scaling estritamente dentro de cada fold. | `AvaliadorAninhado` | 
 | **RF-07** | **Fábrica de Modelos & Tuning Adaptativo** | Suportar até **10 algoritmos de regressão** e aplicar `GridSearchCV` para modelos lineares/rápidos (**Ridge, ElasticNet**) e `RandomizedSearchCV` para ensembles complexos (**CatBoost, XGBoost, Random Forest**). | `FabricaTuning` | 
 | **RF-08** | **Auditoria Estatística Não-Paramétrica** | Extrair resíduos pareados dos folds externos e aplicar testes de normalidade (**Shapiro-Wilk**), significância de rankings (**Friedman**) e pós-testes de **Nemenyi** e **Tukey** para comprovação matemática. | `TesteFriedman` | 
 | **RF-09** | **Seleção do Campeão & Comitê VotingRegressor** | Eleger o modelo individual campeão ou construir um comitê `VotingRegressor` ponderado com os **Top K modelos** que sejam estatisticamente indistinguíveis pelo teste de Friedman (**p-valor < 0.05**). | `SeletorCampeao` | 
 | **RF-10** | **Motor Imobiliário & Enriquecimento Multinível** | Calcular referências de mercado históricas em **3 níveis (Global, Zona, Bairro)** e enriquecer as previsões com corredores de negociação, índices comparativos de m² e descontos de **5%, 10% e 15%**. | `MotorImobiliario` | 
 | **RF-11** | **Empacotamento Unificado PyFunc no MLflow** | Empacotar o pipeline Scikit-Learn ajustado e o `MotorImobiliario` em um wrapper único `mlflow.pyfunc`, registrando o modelo no MLflow Registry com tag `@champion` e assinatura de **32/40 campos**. | `ObservadorMlflow` | 
 | **RF-12** | **Serving REST de Inferência em Tempo Real** | Disponibilizar endpoint HTTP na porta **8080** (`/invocations`) compatível com JSON nos formatos `dataframe_records` e `dataframe_split`, retornando resposta enriquecida e expondo `/metrics` na porta **8000**. | `servidor_inferencia` | 

### 3.3 – Requitos não funcionais:

 | **ID** | **Requisito Não Funcional** | **Descrição Técnica & Comportamento Esperado** | 
 | ---------- | ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | 
 | **RNF-01** | **Performance & Latência** | **SLA < 150ms**. A API de inferência deve processar requisições unitárias em menos de **80ms em média**, com **p95 < 150ms** e **p99 < 300ms**, viabilizando uso interativo em tempo real por portais e corretores. | 
 | **RNF-02** | **Determinismo & Reprodutibilidade** | **Zero aleatoriedade**. Todas as divisões de dados, validação aninhada e inicialização de modelos utilizam **sementes pseudoaleatórias fixas configuradas via YAML** (semente **42**), garantindo reprodução idêntica de métricas entre execuções. | 
 | **RNF-03** | **Governança Anti-Leakage** | **Lacre estrito**. É proibido qualquer contato do conjunto de teste ou folds de validação com os transformadores de features (`OneHotEncoder`, `RobustScaler`, `SimpleImputer`), eliminando contaminação estatística (*data leakage*). | 
 | **RNF-04** | **Imutabilidade Pré-Teste** | **Trava de segurança**. O cofre de *holdout* só pode ser destravado com chave mestra após o modelo final e o motor imobiliário serem formalmente congelados (`estado_congelado = True`), impossibilitando retreinos ou sobreajustes induzidos após o teste. | 
 | **RNF-05** | **Observabilidade** | **OpenMetrics — 56 métricas nativas**. Exposição de métricas no padrão Prometheus com persistência atômica via `PersistenciaMetricas`, permitindo que os dashboards Grafana continuem ativos mesmo após o término do pipeline de treino. | 
 | **RNF-06** | **Resiliência em Contêineres** | **Docker Compose**. Arquitetura desacoplada em microsserviços via Docker Compose, com isolamento de **PostgreSQL**, armazenamento de artefatos S3 (**RustFS**), **MLflow Tracking**, **Prometheus**, **Grafana** e **Serving REST**. | 
 | **RNF-07** | **Usabilidade & Responsividade** | **Mobile-First**. A documentação oficial e o simulador interativo operam com fluidez em **smartphones** (drawer lateral com overlay), **tablets** e **monitores widescreen**, sem quebras de layout ou transbordamento horizontal. | 
 | **RNF-08** | **Tipagem Estrita & Manutenibilidade** | **Python 3.12**. Código desenvolvido com tipagem estática rigorosa, utilizando **dataclasses congeladas**, tipos genéricos, tuplas imutáveis e verificação **MyPy**, assegurando integridade e documentação viva no próprio código. | 

### 3-4 – Regras de negócio:

 | **Regra** | **Conceito de Negócio** | **Fórmula / Definição Operacional** | **Impacto & Aplicação na Mesa de Vendas** | 
 | --------- | ------------------------------------------- | ------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | 
 | **RN-01** | **Preço Justo Algorítmico** | `valor_previsto` — estimativa do comitê de ML | **Âncora de Avaliação:** Ponto central de equilíbrio para captação e precificação inicial do apartamento. | 
 | **RN-02** | **Equalizador Unitário de Área** | `valor_m2_previsto = valor_previsto ÷ max(Metragem, 1.0)` | **Comparador Universal:** Permite equalizar unidades de metragens distintas no mesmo prédio ou bairro. | 
 | **RN-03** | **Hierarquia em 3 Níveis** | Comparações simultâneas em: **Global (Município), Zona e Bairro** | **Contextualização Completa:** Evita precificar um imóvel de alto padrão com base na média genérica da cidade. | 
 | **RN-04** | **Suficiência & Fallback Geográfico** | Bairros `< 20` amostras ou Zonas `< 30` amostras herdam a referência superior | **Proteção Estatística:** Impede que bairros com poucas transações gerem referências distorcidas ou voláteis. | 
 | **RN-05** | **Corredor de Segurança (Piso & Teto)** | `faixa_segura_piso = -10%` \| `faixa_segura_teto = +10%` | **Defesa Patrimonial:** O piso é a **“linha vermelha”** (nunca vender abaixo sem aval); o teto é a margem de vitrine nos portais. | 
 | **RN-06** | **Política Escalonada de Desconto** | **5%** (cortesia), **10%** (limite do corretor), **15%** (deságio urgente) | **Agilidade Comercial:** Estabelece a alçada de flexibilização do corretor sem necessidade de consultar a gerência. | 
 | **RN-07** | **Índice do Imóvel** | `indice_imovel_* = valor_m2_previsto ÷ mediana_m2_mercado` | **Diferencial Competitivo:** `> 1.15x` indica padrão construtivo superior/vista; `< 0.85x` indica oportunidade ou necessidade de reforma. | 
 | **RN-08** | **Desvio Percentual de Mercado** | `diferenca_perc_* = (valor_previsto − media_mercado) ÷ media × 100` | **Qualificação do Comprador:** Mostra se a unidade pertence ao padrão médio local ou se está no topo da pirâmide de renda. | 

## 4 – Interpretação para a equipe de negócio

*Um apartamento localizado no Sumarezinho (zona Oeste) com três quartos, dois banheiros , uma vagas na garagem, a tabela abaixo mostra a interpretação dos dados da api.
*

 | **Campo no JSON** | **Valor Retornado** | **Conceito Imobiliário** | **Interpretação Prática para a Equipe de Negócio & Roteiro de Conversa** | 
 | ----------------------------------------------------------------------- | ---------------------------------------------- | ------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | 
 | **1. Identificação e Precificação Base do Imóvel** |  |  |  | 
 | `valor_previsto` | **R$ 291.609,93** | Preço Justo Algorítmico | **Âncora de Avaliação:** valor central estimado pelo modelo de Machine Learning. Pode ser utilizado como referência principal para anúncio e negociação. | 
 | `valor_m2_previsto` | **R$ 3.430,71 / m²** | Valor Unitário de Área | **Métrica de Equalização:** permite comparar o imóvel com outras unidades de diferentes tamanhos dentro da mesma região. | 
 | `Zona` | **"Zona Oeste"** | Macrorregião | Identifica a região geográfica utilizada pelo modelo para contextualizar a precificação. | 
 | `Bairro` | **"Sumarezinho"** | Micro-localização | Identifica o bairro utilizado pelo modelo como referência para a análise microlocal. | 
 | **2. Contexto Macrolocal: Cidade de Ribeirão Preto (Nível Global)** |  |  |  | 
 | `global_mediana_mercado` | **R$ 290.000,00** | Mediana Municipal | Representa o valor mediano utilizado como referência para o mercado global. O imóvel previsto está praticamente alinhado à mediana global. | 
 | `global_media_mercado` | **R$ 422.828,81** | Média Municipal | Média de mercado utilizada como referência global. O valor previsto está abaixo dessa média. | 
 | `global_mediana_m2_mercado` | **R$ 4.738,10 / m²** | Mediana do m² Global | Referência do preço mediano por metro quadrado no mercado global. | 
 | `diferenca_perc_global` | **−31,03%** | Desvio sobre a Média Global | O valor previsto está **31,03% abaixo da média global de mercado**, indicando posicionamento abaixo do ticket médio geral. | 
 | `indice_imovel_global` | **0,7241x** | Múltiplo do m² Global | O m² previsto corresponde a aproximadamente **72,41% da mediana global do m²**, ou seja, está cerca de **27,59% abaixo** desse benchmark. | 
 | `global_desconto_5` | **R$ 275.500,00** | Referência Global −5% | Faixa de negociação equivalente a 5% abaixo da mediana global de R$ 290 mil. | 
 | `global_desconto_10` | **R$ 261.000,00** | Referência Global −10% | Faixa equivalente a 10% abaixo da mediana global. | 
 | `global_desconto_15` | **R$ 246.500,00** | Referência Global −15% | Faixa de desconto mais agressiva, equivalente a 15% abaixo da mediana global. | 
 | `global_faixa_segura_piso` | **R$ 261.000,00** | Piso Global Seguro | Referência mínima da faixa segura global, equivalente a 90% da mediana global. | 
 | `global_faixa_segura_teto` | **R$ 290.000,00** | Teto Global Seguro | Limite superior da faixa segura global, correspondente à mediana global. | 
 | **3. Contexto Regional: Zona Oeste** |  |  |  | 
 | `zona_mediana_mercado` | **R$ 220.000,00** | Mediana da Zona Oeste | Valor mediano de mercado utilizado como benchmark para a Zona Oeste. | 
 | `zona_media_mercado` | **R$ 243.404,97** | Média da Zona Oeste | Média dos valores de mercado utilizados como referência para a zona. | 
 | `zona_mediana_m2_mercado` | **R$ 4.166,67 / m²** | Mediana do m² na Zona | Referência do preço mediano por metro quadrado da Zona Oeste. | 
 | `valor_previsto_zona` | **R$ 291.609,93** | Previsão do Imóvel na Zona | O valor previsto pelo modelo para este imóvel é utilizado também como referência da previsão dentro da zona. | 
 | `valor_m2_previsto_zona` | **R$ 3.430,71 / m²** | Previsão do m² na Zona | Valor previsto por metro quadrado para o imóvel dentro da análise regional. | 
 | `diferenca_perc_zona` | **+19,80%** | Desvio sobre a Mediana da Zona | O valor previsto está **19,80% acima da mediana da Zona Oeste**, indicando posicionamento superior ao padrão mediano regional. | 
 | `indice_imovel_zona` | **0,8234x** | Múltiplo do m² da Zona | O m² previsto corresponde a aproximadamente **82,34% da mediana do m² da Zona Oeste**, ficando cerca de 17,66% abaixo desse benchmark. | 
 | `zona_desconto_5` | **R$ 209.000,00** | Referência Zona −5% | Valor correspondente a 5% abaixo da mediana regional de R$ 220 mil. | 
 | `zona_desconto_10` | **R$ 198.000,00** | Referência Zona −10% | Valor correspondente a 10% abaixo da mediana regional. | 
 | `zona_desconto_15` | **R$ 187.000,00** | Referência Zona −15% | Faixa de desconto agressivo, equivalente a 15% abaixo da mediana regional. | 
 | `zona_faixa_segura_piso` | **R$ 198.000,00** | Piso Regional Seguro | Referência mínima da faixa segura regional, correspondente a 90% da mediana da Zona Oeste. | 
 | `zona_faixa_segura_teto` | **R$ 220.000,00** | Teto Regional Seguro | Limite superior da faixa segura regional, correspondente à mediana da Zona Oeste. | 
 | **4. Contexto Microlocal: Sumarezinho (Nível Bairro)** |  |  |  | 
 | `bairro_mediana_mercado` | **R$ 255.000,00** | Mediana do Bairro | Valor mediano utilizado como principal benchmark de mercado para Sumarezinho. | 
 | `bairro_media_mercado` | **R$ 281.768,00** | Média do Bairro | Média dos valores de mercado utilizada como referência para o bairro. | 
 | `bairro_mediana_m2_mercado` | **R$ 4.415,41 / m²** | Mediana do m² no Bairro | Principal referência de preço por metro quadrado para a análise microlocal. | 
 | `valor_previsto_bairro` | **R$ 291.609,93** | Previsão do Imóvel no Bairro | O valor previsto pelo modelo para este imóvel é utilizado também como referência da previsão no bairro. | 
 | `valor_m2_previsto_bairro` | **R$ 3.430,71 / m²** | Previsão do m² no Bairro | Valor previsto por metro quadrado para o imóvel dentro da análise do bairro. | 
 | `diferenca_perc_bairro` | **+3,49%** | Desvio sobre a Mediana do Bairro | O valor previsto está **3,49% acima da mediana de mercado de Sumarezinho**, indicando forte proximidade ao padrão central do bairro. | 
 | `indice_imovel_bairro` | **0,7770x** | Múltiplo do m² do Bairro | O m² previsto corresponde a aproximadamente **77,70% da mediana do m² do bairro**, ficando cerca de 22,30% abaixo do benchmark. | 
 | `bairro_desconto_5` | **R$ 242.250,00** | Desconto Comercial de 5% | Referência equivalente a 5% abaixo da mediana do bairro. | 
 | `bairro_desconto_10` | **R$ 229.500,00** | Desconto Comercial de 10% | Referência equivalente a 10% abaixo da mediana do bairro. | 
 | `bairro_desconto_15` | **R$ 216.750,00** | Desconto Agressivo de 15% | Faixa de negociação equivalente a 15% abaixo da mediana do bairro. | 
 | `bairro_faixa_segura_piso` | **R$ 229.500,00** | Piso Seguro de Venda | Referência mínima da faixa segura do bairro, correspondente a 90% da mediana de R$ 255 mil. | 
 | `bairro_faixa_segura_teto` | **R$ 255.000,00** | Teto Seguro de Venda | Limite superior da faixa segura, correspondente à mediana de mercado do bairro. | 
 | **5. Previsões Hierárquicas do Modelo** |  |  |  | 
 | `valor_previsto_zona` | **R$ 291.609,93** | Previsão Hierárquica — Zona | Valor previsto retornado pela API para o nível regional. Neste caso, é idêntico ao `valor_previsto`. | 
 | `valor_previsto_bairro` | **R$ 291.609,93** | Previsão Hierárquica — Bairro | Valor previsto retornado pela API para o nível microlocal. Neste caso, é idêntico ao `valor_previsto`. | 
 | `valor_m2_previsto_zona` | **R$ 3.430,71 / m²** | Previsão do m² — Zona | Valor unitário previsto para o nível regional. | 
 | `valor_m2_previsto_bairro` | **R$ 3.430,71 / m²** | Previsão do m² — Bairro | Valor unitário previsto para o nível microlocal. | 
 | `valor_previsto_medio_zona` | **R$ 291.609,93** | Média da Previsão na Zona | Média retornada pelo modelo para a previsão no contexto da zona. | 
 | `valor_previsto_medio_bairro` | **R$ 291.609,93** | Média da Previsão no Bairro | Média retornada pelo modelo para a previsão no contexto do bairro. | 
 | **6. Estratégia de Negociação, Margens de Desconto e Fechamento** |  |  |  | 
 | `bairro_desconto_5` | **R$ 242.250,00** | Negociação com 5% de desconto | Primeiro nível de concessão em relação à mediana de mercado do bairro. | 
 | `bairro_desconto_10` | **R$ 229.500,00** | Negociação com 10% de desconto | Segundo nível de concessão, utilizado para negociações mais agressivas. | 
 | `bairro_desconto_15` | **R$ 216.750,00** | Negociação com 15% de desconto | Nível de desconto mais agressivo em relação ao benchmark do bairro. | 
 | `bairro_faixa_segura_piso` | **R$ 229.500,00** | Piso Seguro | Referência de 90% da mediana do bairro para controle da negociação. | 
 | `bairro_faixa_segura_teto` | **R$ 255.000,00** | Teto Seguro | Referência máxima da faixa segura baseada na mediana do bairro. | 

###

> **"O modelo de inteligência de mercado estimou o valor deste imóvel em R$ 291.609,93, equivalente a R$ 3.430,71 por metro quadrado. No mercado global, a mediana é de R$ 290 mil, enquanto a mediana da Zona Oeste é de R$ 220 mil e a de Sumarezinho é de R$ 255 mil. Isso posiciona o imóvel praticamente na mediana global e 3,49% acima da mediana do próprio bairro. Ao mesmo tempo, o valor previsto está 19,80% acima da mediana da Zona Oeste, demonstrando um posicionamento superior ao padrão regional. Para negociação, os benchmarks de segurança do bairro ficam entre R$ 229.500,00 e R$ 255.000,00."**

*5 – Demonstração do projeto:*

{% include youtube.html 
   id="gMFt4OhIO2w" 
   title="Usado multiagentes no google antigravity para construir um sistema de Previsão inteligente de preço de apartamento para a cidade de Ribeirão Preto"
%}



[Link do reposítório](https://github.com/rodrigorocha1234/machine-learning-previsao_preco_ap_v3)