# Proposta de Nova Métrica de Infraestrutura Urbana

Este repositório tem como objetivo **criticar a eficácia do IDH** (Índice de Desenvolvimento Humano) quando aplicado a uma cidade como Fortaleza, propondo uma nova métrica com **foco em infraestrutura urbana**. A ideia é **comparar** essa nova métrica com o IDH oficial de cada bairro, evidenciando possíveis discrepâncias e trazendo à tona dimensões de infraestrutura que não são capturadas pelo IDH tradicional.

---

## 1. Contexto

O IDH considera, de forma resumida, **saúde, educação e renda**. Entretanto, aspectos de **infraestrutura urbana**, como acesso a saneamento, equipamentos de lazer, mobilidade e assistência social, podem ter um impacto direto na qualidade de vida, mas não aparecem de forma explícita no IDH. Nossa proposta é construir um índice que inclua **variáveis de infraestrutura** e, em seguida, **comparar** com o IDH de cada bairro.

---

## 2. Datasets Selecionados

Abaixo, listamos os conjuntos de dados que **manteremos** por serem relevantes à análise de infraestrutura e/ou necessários para a delimitação territorial:

1. **Areninhas**  
   - *Por que manter?* Representa infraestrutura de esporte e lazer em áreas vulneráveis.

2. **Assentamentos Precários**  
   - *Por que manter?* Indica vulnerabilidade habitacional, fundamental para mensurar déficit de infraestrutura básica.

3. **Trechos de Difícil Acesso**  
   - *Por que manter?* Mostra locais onde serviços de limpeza e coleta de lixo enfrentam dificuldades, evidenciando carência de infraestrutura pública.

4. **Bairros de Fortaleza**  
   - *Por que manter?* Necessário para delimitar cada indicador em nível de bairro, permitindo comparações e junções de dados.

5. **CAPS - Centros de Assistência Psicossocial**  
   - *Por que manter?* Retrata a oferta de serviços especializados em saúde mental, complementando a visão de infraestrutura de saúde.

6. **Densidade Populacional por Bairros (km²)**  
   - *Por que manter?* Permite relacionar a quantidade de infraestrutura disponível ao número de habitantes (ou domicílios).

7. **Distritos de Educação**  
   - *Por que manter?* Exibe a organização da rede educacional, mostrando como a educação está distribuída territorialmente.

8. **Domicílios**  
   - *Por que manter?* Informa a quantidade de residências por bairro, útil para comparar oferta de infraestrutura por número de domicílios.

9. **Equipamentos de Assistência Social**  
   - *Por que manter?* Representa a presença de serviços públicos voltados a grupos vulneráveis.

10. **Equipamentos de Saúde**  
    - *Por que manter?* Indica a localização de postos e hospitais, componente-chave de infraestrutura de saúde.

11. **IDH - Classificação**  
    - *Por que manter?* Será nossa base de comparação, pois queremos avaliar a discrepância entre o IDH e a nova métrica.

12. **Pontos de Ônibus**  
    - *Por que manter?* A mobilidade urbana é um elemento crítico de infraestrutura.

13. **Rede Cuca**  
    - *Por que manter?* São equipamentos voltados a cultura, esporte e lazer para jovens e comunidade em geral.

14. **Rede Juv**  
    - *Por que manter?* Semelhante à Rede Cuca, voltada a jovens, ampliando o acesso a cultura/esporte/lazer.

15. **Rede de Abastecimento de Água**  
    - *Por que manter?* Acesso à água encanada é um indicador fundamental de saneamento básico.

16. **Rede de Esgoto**  
    - *Por que manter?* Acesso a rede de esgoto é outro indicador essencial de saneamento básico.

---

## 3. Dataset Excluído

1. **Gravidez na Adolescência**  
   - *Por que retirar?* Trata-se de um indicador de saúde pública e condições sociais, mas não reflete diretamente a **infraestrutura urbana** (como equipamentos e serviços). Poderia ser incluído em um índice mais amplo de qualidade de vida, mas aqui estamos priorizando a infraestrutura física e o acesso a serviços de forma direta.

---

## 4. Como Podemos Cruzar Essas Informações?

Para construir uma **nova métrica** (ou índice) de infraestrutura urbana, adotaremos os seguintes passos:

1. **Padronização Geoespacial**  
   - Todos os *datasets* que possuem dados espaciais (shapefiles, geojsons, etc.) devem ser **unificados** por uma mesma referência territorial.  
   - O *dataset* de **Bairros de Fortaleza** será a base para agrupar ou resumir os demais indicadores por bairro.

2. **Normalização dos Indicadores**  
   - Cada variável pode ser convertida para uma **escala de 0 a 1**, onde 0 representa a pior condição e 1 a melhor.  
   - Exemplo: *densidade de equipamentos de saúde por 10 mil habitantes*, *percentual de domicílios com acesso à rede de esgoto*, etc.

3. **Combinação em um Índice Sintético**  
   - Depois de normalizados, podemos fazer uma **média ponderada** dos indicadores selecionados, definindo pesos de acordo com a importância de cada dimensão (ex.: saneamento pode ter um peso maior que lazer, etc.).  
   - O resultado será um **valor de infraestrutura** para cada bairro.

4. **Comparação com IDH**  
   - Ao final, teremos para cada bairro:  
     - **IDH oficial** (do dataset “IDH - Classificação”).  
     - **Índice de Infraestrutura Urbana** (proposto).  
   - Podemos então analisar a correlação entre os dois índices e identificar bairros com **alto IDH, mas baixa infraestrutura**, ou vice-versa.

5. **Visualização**  
   - Criar mapas temáticos, gráficos de dispersão ou tabelas comparativas para ilustrar como o **IDH** se relaciona (ou não) com o **Índice de Infraestrutura**.

---

## 5. Próximos Passos

- **Coletar** e **limpar** todos os dados, garantindo que haja consistência nos nomes dos bairros e nas projeções geográficas.  
- **Definir** o conjunto final de indicadores (ex.: número de Areninhas, quantidade de CAPS, porcentagem de domicílios atendidos por água/esgoto, etc.).  
- **Calcular** a pontuação de infraestrutura para cada bairro.  
- **Comparar** com o IDH, analisando padrões, correlações e possíveis discrepâncias.  
- **Documentar** as conclusões e possíveis sugestões de políticas públicas voltadas à melhoria da infraestrutura nos bairros mais carentes.

---

*Última atualização: 17/02/25*  
