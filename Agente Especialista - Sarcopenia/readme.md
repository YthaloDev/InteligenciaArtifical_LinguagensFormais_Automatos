# Agente Especialista Mecânico

## 1. Problema escolhido, entradas, rótulo e recomendação

### Problema escolhido
O agente procura monitorar as condições de veículos e informar recomendações ou ações do que deve ser feito a respeito.

### Entradas (X)
As entradas são as informações utilizadas pelo modelo para realizar suas previsões.

- **X1 – Temperatura do motor:** Representa a temperatura do motor em celsius e possui um intervalo de 0 a 120 C
- **X2 – Nível do óleo:** Representa o nível do óleo do carro e possui um intervalo de 0% a 100%

### Rótulo (Y)
O modelo ira prever os estados dos veículos podendo ter as seguintes classificações

Classificações utilizadas:
- Normal
- Atenção
- Problema
- Problema crítico

### Recomendações
Cada classificação é associada a uma recomendação sendo elas

| Classificação | Recomendação |
|---|---|
| Normal | Veículo Normal (Nenhuma ação requisitada)|
| Atenção | Atenção ao veículo cheque o nível do óleo e considere levar a um mecanico |
| Problema | O veículo possui um provavel problema, leve a um mecanico |
| Problema crítico | O veículo possui um possivel problema critico leve a um mecanico |

---

## 2. Regras do sistema especialista e origem

As regras representam os critérios utilizados pelo sistema para interpretar as entradas e determinar uma classificação.

### Regra 1
- **Condição:** Temperatura entre níveis normais (60 a 84) e Oleo em niveis normais (40% a 100%)
- **Resultado:** Normal
- **Ação:** Veículo Normal (Nenhuma ação requisitada)

### Regra 2
- **Condição:** Temperatura e nivel oleo onde seus niveis resulta em uma pontuação de atenção == 1
- **Resultado:** Atenção
- **Ação:** Checar nível do oleo e considerar levar a um mecanico

### Regra 3
- **Condição:** Temperatura e nivel oleo onde seus niveis resulta em uma pontuação de atenção == 2
- **Resultado:** Problema
- **Ação:** Levar a um mecanico

### Regra 4
- **Condição:** Temperatura e nivel oleo onde seus niveis resulta em uma pontuação de atenção > 2
- **Resultado:** Problema critico
- **Ação:** Levar a um mecanico

### Origem das regras
Os critérios utilizados nas regras foram definidos com base nos meus conhecimentos básicos de mecânica automotiva.

Para a temperatura do motor, os intervalos foram estabelecidos considerando valores aproximados de funcionamento de motores automotivos, levando em conta as diferentes condições de temperatura durante o uso.

Já para o nível de óleo, os critérios foram definidos com base nos níveis recomendados para o funcionamento adequado e a lubrificação do motor.

Os valores que escolhi foram simplificações para fins da simulação e podem variar conforme o fabricante e o modelo do veículo.

---

## 3. Dataset rotulado

### Tamanho
- **Quantidade de registros:** A quantidade de registros é dinamica e pode ser configurada. Padrao = 100
- **Quantidade de entradas:** 2
- **Quantidade de classificações:** 4

### Origem dos dados
Os dados foram gerado por um algoritmo que criei em gerar_base_mecanica.py

### Critérios de rotulagem
Cada intervalo de valores das entradas possui uma pontuação de atenção específica. Dessa forma, a classificação do estado do veículo é definida pela soma das pontuações da temperatura do motor e do nível do óleo.

Por exemplo: se a temperatura for de 64 C (pontuação 0) e o nível do óleo for de 75% (pontuação 0), a soma será igual a 0, correspondendo à Regra 1, que classifica o veículo como "Normal".

### Dados simulados
Os dados são puramente artificiais e foram gerados pelo script apenas para demonstrar a criação de um agente especialista.

---

## 4. Treinamento e avaliação do classificador

### Separação dos dados
- 75% para treinamento.
- 25% para teste.

### Classificador utilizado
- **Algoritmo:** Decision Tree Classifier (Árvore de Decisão).
- **Profundidade máxima:** 10
- **Random state:** 42

### Resultados

- **Acurácia:** 100%

### Matriz de confusão

![Matriz de Confusão](./assets/Figure_1.jpeg)

### Grafico da arvore

![Grafico da arvore](./assets/arvore.png)

### Interpretação dos resultados
A acurácia representa a proporção de previsões corretas realizadas pelo modelo em relação aos resultados reais (y_teste). Neste treinamento, o modelo obteve 100% de acurácia, indicando que todas as previsões corresponderam aos rótulos esperados.

A matriz de confusão confirma esse resultado, apresentando todos os valores na diagonal principal e nenhum erro de classificação.

---

## 5. Utilização da previsão em uma regra do sistema especialista

Exemplo de funcionamento:

1. O usuário informa a temperatura do motor e o nível do óleo.
2. O classificador recebe essas duas entradas.
3. O modelo realiza uma previsão do estado do veículo.
4. O sistema especialista utiliza a classificação prevista para selecionar a recomendação correspondente.

**Previsão:** Temperatura motor 60 C e nivel do oleo 40%

**Regra aplicada:** Regra 1 – Se a pontuação de atenção for igual a 0, classificar como Normal.

**Recomendação:** Veículo Normal.

---

## 6. Demonstração de três novos casos

Codigo:
![Novos casos](./assets/novoscasos1.jpg)

Output:
![Novos casos output](./assets/novoscasos2.jpg)

---

## 7. Limitações

### Limitações
As limitações do sistema por exemplo seria que ele não pode ser usado em um contexto real de automotivos e que para realmente dizer o estado de um carro seria preciso de muitas outras entradas e classificações.

---
