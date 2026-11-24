# Análise de Sarcopenia com Machine Learning

Projeto experimental de ciência de dados para estudar características associadas à **classificação atual de sarcopenia** em pessoas idosas. A análise usa Python no Google Colab e compara Regressão Logística e Random Forest.

> **Escopo:** este estudo é educacional e exploratório. Como a base é transversal, **não é possível concluir que o modelo prevê o desenvolvimento de sarcopenia no futuro**, nem usá-lo para diagnóstico médico.

## Objetivo

Investigar como idade, medidas de composição corporal, força de preensão e desempenho funcional se relacionam à classificação de sarcopenia registrada na base. O desfecho inicial é binário (`0 = não`, `1 = sim`).

## Origem dos dados

- **Fonte:** repositório de [Dequin et al.](https://github.com/dmdequin/sarcopenia_and_machine_learning).
- **Arquivo:** `data/datos_completos.csv`.
- **Tamanho da amostra original:** 1.253 observações.
- **Artigo:** Virto et al. (2024), [PLOS ONE](https://doi.org/10.1371/journal.pone.0316174).
- **Atenção:** a amostra tem características populacionais específicas e pode não ser representativa de outros países.

## Pergunta de pesquisa

> É possível distinguir participantes classificados com e sem sarcopenia usando informações de idade, composição corporal e desempenho físico?

A previsão de **sarcopenia futura** é uma etapa posterior e exigirá registros longitudinais com um desfecho observado depois da coleta inicial.

## Tecnologias

- Python 3
- pandas e NumPy
- scikit-learn
- matplotlib e seaborn
- Google Colab

## Estrutura sugerida do repositório

```text
sarcopenia-machine-learning/
├── notebooks/
│   └── Sarcopenia_Machine_Learning_Estruturado.ipynb
├── data/
│   └── README.md                # Orientações sobre a fonte original
├── results/
│   └── README.md                # Local para gráficos e relatórios futuros
├── README.md
└── requirements.txt            # Dependências a registrar
```

Os diretórios acima são uma proposta de organização; não é necessário criá-los para executar o Colab.

## Metodologia

1. **Leitura:** importação do CSV, com conversão de vírgulas decimais e reconhecimento de erros de planilha como valores ausentes.
2. **Exploração:** inspeção das variáveis, valores ausentes, estatísticas descritivas e distribuição das classes.
3. **Seleção:** escolha explícita das variáveis de entrada e remoção de colunas que já codificam classificações de sarcopenia.
4. **Divisão:** 80% dos dados para treinamento e 20% para teste, preservando a proporção das classes.
5. **Pré-processamento:** imputação pela mediana para medidas numéricas, categoria mais frequente para sexo, padronização e codificação categórica, dentro do `Pipeline`.
6. **Modelagem:** comparação entre Regressão Logística e Random Forest por validação cruzada estratificada no treino.
7. **Avaliação:** F1-score, recall, precisão, ROC-AUC, matriz de confusão e importância por permutação.

## Execução

1. Abra o arquivo `.ipynb` no [Google Colab](https://colab.research.google.com/).
2. Execute as células em ordem, a partir do início.
3. Verifique as tabelas de qualidade dos dados e as métricas apresentadas.
4. Registre os resultados observados e as limitações na seção final do notebook.

O arquivo CSV é obtido diretamente do repositório original durante a execução; é necessário acesso à internet no Colab.

## Cuidados metodológicos

- **Classificação não é previsão temporal:** apenas uma coorte acompanhada ao longo dos anos permite treinar e validar a previsão de novos casos.
- **Possível circularidade diagnóstica:** massa muscular, força e mobilidade podem integrar os critérios que determinam o próprio rótulo. Um desempenho alto pode refletir reprodução desses critérios.
- **Vazamento de dados:** não usar outras colunas que já são desfechos/diagnósticos como entradas e não ajustar imputação no conjunto de teste.
- **Probabilidades:** os valores de `predict_proba` não devem ser tratados como risco clínico sem avaliação de calibração e validação externa.
- **População:** avaliar desempenho por sexo, idade e em bases externas antes de qualquer interpretação aplicada.

## Estado do projeto

- [x] Importação e reconhecimento das colunas da base
- [x] Implementação proposta de pipelines de classificação
- [x] Implementação proposta de comparação por validação cruzada
- [ ] Executar o notebook atualizado sobre toda a base no Colab
- [ ] Registrar e discutir resultados de teste
- [ ] Validar com base independente
- [ ] Encontrar coorte longitudinal para previsão de casos futuros

## Referência

Virto, N.; Dequin, D. M.; Río, X.; Méndez-Zorrilla, A.; García-Zapirain, B. (2024). *Exploring determinant factors influencing muscle quality and sarcopenia in Bilbao's older adult population through machine learning: A comprehensive analysis approach*. PLOS ONE. DOI: [10.1371/journal.pone.0316174](https://doi.org/10.1371/journal.pone.0316174).
