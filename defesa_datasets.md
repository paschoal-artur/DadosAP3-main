# Proposta de Nova Métrica de Infraestrutura Urbana

Este repositório tem como objetivo **criticar a eficácia do IDH** (Índice de Desenvolvimento Humano) quando aplicado a uma cidade como Fortaleza, propondo uma nova métrica com **foco em infraestrutura urbana**. A ideia é **comparar** essa nova métrica com o IDH oficial de cada bairro, evidenciando possíveis discrepâncias e trazendo à tona dimensões de infraestrutura que não são capturadas pelo IDH tradicional.

---

## 1. Contexto

O IDH considera, de forma resumida, **saúde, educação e renda**. Entretanto, aspectos de **infraestrutura urbana**, como acesso a saneamento, equipamentos de lazer, mobilidade e assistência social, podem ter um impacto direto na qualidade de vida, mas não aparecem de forma explícita no IDH. Nossa proposta é construir um índice que inclua **variáveis de infraestrutura** e, em seguida, **comparar** com o IDH de cada bairro para verificar possíveis divergências.

---

## 2. Datasets Selecionados

Abaixo, listamos os conjuntos de dados que **manteremos** por serem relevantes à análise de infraestrutura e/ou necessários para a delimitação territorial:

1. **Areninhas**  
   - *Por que manter?*  
     - Representa infraestrutura de esporte e lazer em áreas vulneráveis.  
     - Pode ser convertido em indicador de *quantidade de arenas por bairro*.

2. **Assentamentos Precários**  
   - *Por que manter?*  
     - Indica vulnerabilidade habitacional e déficit de infraestrutura básica.

3. **Trechos de Difícil Acesso**  
   - *Por que manter?*  
     - Evidencia locais onde serviços de coleta de lixo enfrentam obstáculos, sinalizando carência de infraestrutura pública.

4. **Bairros de Fortaleza**  
   - *Por que manter?*  
     - Fundamental para delimitação e junção (join) de dados.  
     - Base geográfica para resumir indicadores por bairro.

5. **CAPS - Centros de Assistência Psicossocial**  
   - *Por que manter?*  
     - Oferece dados sobre infraestrutura de saúde mental.  
     - Pode ser transformado em *quantidade de CAPS por bairro* ou *distância média aos CAPS*.

6. **Densidade Populacional por Bairros (km²)**  
   - *Por que manter?*  
     - Permite relacionar a oferta de infraestrutura com o número de habitantes.  
     - Pode ser usado para normalizar outros indicadores (ex.: *Areninhas por 10 mil habitantes*).

7. **Distritos de Educação**  
   - *Por que manter?*  
     - Mostra a divisão territorial específica da rede educacional, podendo revelar disparidades na oferta de escolas.

8. **Domicílios**  
   - *Por que manter?*  
     - Ajuda a comparar infraestrutura com o total de residências.  
     - Indicador útil para entender a *cobertura de serviços por domicílio*.

9. **Equipamentos de Assistência Social**  
   - *Por que manter?*  
     - Demonstra a presença de equipamentos públicos voltados a grupos vulneráveis.  
     - Pode ser convertido em *quantidade de equipamentos por bairro*.

10. **Equipamentos de Saúde**  
    - *Por que manter?*  
      - Representa postos e hospitais, um componente-chave de infraestrutura de saúde.  
      - Pode ser convertido em *densidade de equipamentos de saúde*.

11. **IDH - Classificação**  
    - *Por que manter?*  
      - Serve como base de comparação para a nova métrica de infraestrutura.

12. **Pontos de Ônibus**  
    - *Por que manter?*  
      - Mobilidade urbana é crucial; podemos avaliar a *densidade de pontos de ônibus* por bairro.

13. **Rede Cuca**  
    - *Por que manter?*  
      - Oferece infraestrutura de cultura e lazer voltada a jovens; pode ser convertido em *número de equipamentos por bairro*.

14. **Rede Juv**  
    - *Por que manter?*  
      - Semelhante à Rede Cuca, ampliando o acesso a cultura/esporte/lazer para jovens.

15. **Rede de Abastecimento de Água**  
    - *Por que manter?*  
      - Saneamento básico (água encanada) é um indicador essencial de infraestrutura.

16. **Rede de Esgoto**  
    - *Por que manter?*  
      - Saneamento básico (esgoto) é outro indicador crítico de infraestrutura.

---

## 3. Dataset Excluído

1. **Gravidez na Adolescência**  
   - *Por que retirar?*  
     - Trata-se de um indicador de saúde pública e condições sociais, mas não reflete diretamente a **infraestrutura urbana** (como equipamentos e serviços).  
     - Poderia integrar um índice mais amplo de qualidade de vida, mas aqui priorizamos a infraestrutura física e o acesso a serviços.

---

## 4. Como Podemos Cruzar Essas Informações?

Para construir uma **nova métrica** (ou índice) de infraestrutura urbana, adotaremos os seguintes passos:

### 4.1 Padronização Geoespacial

1. **Unificar projeções**:  
   - Garantir que todos os datasets (Bairros, Areninhas, CAPS, etc.) estejam no mesmo sistema de coordenadas.  
   - Exemplo: **EPSG:31984 (SIRGAS 2000 - UTM 24S)** ou **EPSG:4326 (WGS 84)**.

2. **Chaves de agregação**:  
   - Utilizar o *código do bairro* ou *nome do bairro* para associar cada equipamento, densidade populacional, etc., ao respectivo bairro.  
   - Onde não houver correspondência exata, será necessário fazer uma correção manual ou *spatial join* (junção espacial).

### 4.2 Criação de Indicadores

1. **Indicadores de Infraestrutura**:  
   - Exemplo 1: *Areninhas por 10 mil habitantes*.  
   - Exemplo 2: *Percentual de domicílios com acesso à rede de esgoto*.  
   - Exemplo 3: *Número de equipamentos de saúde por km²*.

2. **Conversão em escala de 0 a 1**:  
   - Para cada indicador, definir um método de normalização.  

### 4.3 Combinação em um Índice Sintético

1. **Definir pesos**:  
   - Alguns indicadores podem ter maior relevância (ex.: saneamento) do que outros (ex.: lazer).  
   - Exemplo: 40% saneamento, 20% mobilidade, 20% lazer, 20% saúde.

2. **Cálculo do índice**:  
   - Índice de Infraestrutura (II) = ∑ indicador * peso.  
   - Gera-se um valor final (0 a 1) para cada bairro.

### 4.4 Comparação com IDH

1. **Cruzamento**:  
   - Para cada bairro, teremos:  
     - **IDH** (do dataset “IDH - Classificação”).  
     - **Índice de Infraestrutura** (II).  
   - Podemos verificar correlações, identificar bairros com alto IDH e baixa infraestrutura, etc.

2. **Visualização**:  
   - Criar **mapas temáticos** mostrando o IDH e o II.  
   - Gráficos de dispersão (IDH x II).  
   - Tabelas comparativas.

---

## 5. Próximos Passos

1. **Coletar e Limpar** os Dados  
   - Verificar consistência de nomes de bairros, formatos de data, sistemas de coordenadas, etc.  
   - Excluir ou corrigir entradas inconsistentes.

2. **Definir o Conjunto Final de Indicadores**  
   - Escolher variáveis-chave (ex.: Areninhas, Rede de Água, Rede de Esgoto, CAPS, Equipamentos de Saúde, etc.).  
   - Decidir como cada variável será calculada (por km², por 10 mil habitantes, etc.).

3. **Calcular a Pontuação de Infraestrutura**  
   - Aplicar a normalização para cada indicador.  
   - Atribuir pesos e gerar o índice final para cada bairro.

4. **Comparar com o IDH**  
   - Analisar correlações e discrepâncias.  
   - Identificar bairros prioritários para políticas públicas.

5. **Documentar Conclusões**  
   - Elaborar relatórios e visualizações.  
   - Propor intervenções ou sugestões de melhoria na infraestrutura urbana dos bairros mais carentes.

---

## 6. Justificativas Complementares

- **Uso dos Distritos de Educação e Regionais**:  
  - As regionais e distritos podem oferecer uma visão mais justa de como saúde e educação se distribuem, pois alguns bairros podem se sobrepor a diferentes regionais.  
  - Facilita o planejamento de políticas públicas direcionadas, principalmente para equipamentos de saúde e educação.

- **Possibilidade de Expansão**:  
  - Indicadores de resultado social (como *Gravidez na Adolescência*) podem ser reintroduzidos em estudos futuros que busquem avaliar **qualidade de vida** de forma mais ampla, não apenas a infraestrutura física.

---

*Última atualização: 17/02/25*  
