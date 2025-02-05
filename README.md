# SQL-Analyses
# 🚀 Lead Data Analysis

Este repositório apresenta uma análise detalhada de dados de leads para uma empresa Tech, utilizando consultas SQL no Metabase para visualizar métricas importantes.  

## 🎯 Objetivo do Projeto 

O objetivo deste projeto é realizar uma análise de dados a partir de informações sobre leads de uma plataforma educacional, utilizando consultas SQL no Metabase para criar gráficos e dashboards interativos. Com isso, busca-se extrair insights relevantes sobre características demográficas, níveis educacionais, engajamento e interações dos leads, oferecendo suporte à tomada de decisões estratégicas.  

---

## ⚙️ Ferramentas Utilizadas  

- **Linguagem:** SQL  
- **Ferramenta de BI:** Metabase  

---

## 📊 Análises Realizadas  

1. **Gráfico de Pizza:** Distribuição por Gênero
```sql
SELECT 
  gender,
  COUNT(gender) AS quantidade
FROM 
  leads_basic_details
GROUP BY 
  gender;
```
2. **Cartão:** Média de Idade dos Leads
```sql
SELECT 
  ROUND(AVG(age)) AS media_idade
FROM 
  leads_basic_details;
```  
3. **Gráfico de Barras:** Quantidade de Leads por Grau de Escolaridade
```sql
SELECT 
  current_education,
  COUNT(lead_id) AS quantidade
FROM 
  leads_basic_details
GROUP BY 
  current_education
ORDER BY 
  quantidade DESC;
```  
4. **Tabela:** Porcentagem Assistida por Idioma (Acima de 50%)
```sql
SELECT 
  language,
  watched_percentage AS Porcentagem
FROM 
  leads_demo_watched_details
WHERE 
  watched_percentage > 0.5
GROUP BY 
  language, watched_percentage;
```    
5. **Gráfico de Linhas:** Evolução de Ligações por Plataforma
```sql
WITH CONSULTA1 AS (
  SELECT 
    call_done_date, 
    COUNT(call_status) AS Qtd_ligacoes
  FROM 
    leads_interaction_details
  GROUP BY 
    call_done_date
),
CONSULTA2 AS (
  SELECT 
    lead_gen_source
  FROM 
    leads_basic_details
  GROUP BY 
    lead_gen_source
)
SELECT 
  lid.call_done_date, 
  lbd.lead_gen_source, 
  IFNULL(c1.Qtd_ligacoes, 0) AS Qtd_ligacoes
FROM 
  leads_interaction_details lid
LEFT JOIN 
  leads_basic_details lbd ON lid.lead_id = lbd.lead_id
LEFT JOIN 
  CONSULTA1 c1 ON lid.call_done_date = c1.call_done_date;
```    

---

## 🚀 Dashboard Final  

![final_dashboard](https://github.com/user-attachments/assets/c5ad218f-d1d6-4f07-bab2-189d5315f416)
 

---

