# 📊 Análise de Cobertura por Filial e Setor - Varejo

<img width="1441" height="810" alt="image" src="https://github.com/user-attachments/assets/1ce793b0-e42e-4c66-8e3d-e67fba31dfff" />

Este projeto foi desenvolvido para otimizar a **gestão de estoque em uma rede de varejo**, permitindo a identificação precisa do equilíbrio entre o volume de vendas e o estoque disponível (**Cobertura**).

> **Nota de Privacidade**  
> Este repositório contém uma versão **minimizada e anonimizada de um projeto real de larga escala**.  
> Todos os dados sensíveis foram tratados via **script Python** para garantir a confidencialidade das informações originais.

---

## 📌 Visão Geral do Projeto

O objetivo central é monitorar a **Cobertura de Estoque**, um KPI vital para o varejo que indica **por quanto tempo o estoque atual suprirá a demanda com base no ritmo de vendas**.

O dashboard permite que gestores identifiquem rapidamente:

- Filiais com **excesso de estoque** (capital imobilizado)
- Filiais com **baixo estoque** (risco de ruptura)
- Desempenho de **cobertura por setor e subclasse de produto**

---

## 🛠️ Tecnologias Utilizadas

- **Power BI**  
  Construção dos dashboards e modelagem de dados

- **DAX**  
  Criação de métricas de inteligência de tempo e classificação ABC

- **Python (Jupyter Notebook)**  
  Desenvolvimento de um **gerador de dados sintéticos para anonimização**, garantindo a veracidade das proporções estatísticas sem expor dados reais

---

## 🏗️ Modelagem de Dados

O projeto utiliza um **esquema em estrela (Star Schema)** para garantir performance e escalabilidade.

### Tabelas de Fato
- **fVendas** — histórico de movimentações  
- **fEstoque** — posição diária/mensal de estoque

### Tabelas de Dimensão
- **dProdutos** — hierarquia de categorias  
- **dFiliais** — geografia e tipo de unidade  
- **dCalendario** — dimensão temporal

### Tabelas Auxiliares
- **_Medidas**  
- **Dicionario_Medidas**

Utilizadas para organização e governança das métricas do relatório.

---

## 📊 Estratégia de Análise ABC

Para direcionar o foco dos gestores, foi implementada uma **Classificação ABC por Filial**.

Essa lógica não foca apenas no faturamento, mas em **como a cobertura de cada unidade se comporta em relação à média da rede**.

A métrica permite identificar **filiais com cobertura destoante**, direcionando ações para corrigir distorções de estoque.

### Lógica DAX utilizada

```DAX
ABC = 
// Medida usada de parâmetro para o ABC
VAR Percentual
RETURN
SWITCH(
    TRUE(),
    Percentual <= 0.7, "A",
    Percentual <= 0.9, "B",
    "C"
)
