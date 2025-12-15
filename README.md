# Atividades Dissertativas – Análise do Sistema de Cálculo de IMC

Apenas as atividades que demandam uma resposta discursiva serão respondidas neste arquivo.

---

## Exercício 1

### Atividade 2 – Registro de Falhas e Comportamentos Observados

Este documento apresenta as falhas, comportamentos inesperados e dificuldades de uso identificadas durante a análise do sistema de cálculo do IMC.

---

### 1. Falha crítica – Divisão por zero

**Cenário:**  
Altura igual a 0.

**Comportamento observado:**  
O sistema lança uma exceção (`ArithmeticException`) durante o cálculo do IMC.

**Impacto:**  
A aplicação é encerrada abruptamente.

**Classificação:**  
Falha crítica (crash da aplicação).

---

### 2. Aceitação de valores inválidos – Peso negativo

**Cenário:**  
Peso informado com valor negativo.

**Comportamento observado:**  
O sistema calcula o IMC normalmente e retorna uma classificação.

**Impacto:**  
Resultado inválido do ponto de vista clínico.

**Classificação:**  
Falha funcional / regra de negócio não validada.

---

### 3. Aceitação de valores inválidos – Altura negativa

**Cenário:**  
Altura informada com valor negativo.

**Comportamento observado:**  
O sistema realiza o cálculo e apresenta um IMC positivo.

**Impacto:**  
O valor apresentado não representa uma situação real.

**Classificação:**  
Falha funcional / domínio não validado.

---

### 4. Classificação incorreta em valores de fronteira

**Cenário:**  
IMCs próximos aos limites de classificação (ex.: 16.1, 17.1, 18.6, 25.1).

**Comportamento observado:**  
A classificação ocorre, porém a lógica utilizada (uso de `==` combinado com `<`) torna os intervalos confusos e suscetíveis a erro.

**Impacto:**  
Risco de classificação incorreta para valores próximos aos limites.

**Classificação:**  
Comportamento inesperado / risco funcional.

---

### 5. Falta de tratamento para entradas não numéricas

**Cenário:**  
Entrada de texto no lugar de números (ex.: "abc").

**Comportamento observado:**  
Lançamento de `NumberFormatException`.

**Impacto:**  
A aplicação é finalizada sem qualquer orientação ao usuário.

**Classificação:**  
Falha de robustez / usabilidade.

---

### 6. Uso redundante de Scanner

**Cenário:**  
Leitura de peso e altura.

**Comportamento observado:**  
Dois objetos `Scanner` distintos são utilizados para o mesmo `System.in`.

**Impacto:**  
Não causa erro imediato, mas dificulta a manutenção e reduz a clareza do código.

**Classificação:**  
Dificuldade técnica / má prática de programação.

---

### 7. Ausência de validações e mensagens orientativas

**Cenário:**  
Qualquer erro de entrada de dados.

**Comportamento observado:**  
O sistema não informa limites aceitáveis nem orienta o usuário em caso de erro.

**Impacto:**  
Experiência do usuário prejudicada.

**Classificação:**  
Dificuldade de uso (UX).

---

### 8. Encerramento abrupto do programa em caso de erro

**Cenário:**  
Ocorrência de qualquer exceção.

**Comportamento observado:**  
A execução é interrompida sem possibilidade de correção da entrada.

**Impacto:**  
Baixa tolerância a falhas e confiabilidade reduzida.

**Classificação:**  
Falha de confiabilidade.

___

### Atividade 3 – Especificação Funcional do Sistema de Cálculo de IMC

Este documento descreve a especificação funcional do sistema de cálculo de IMC, definindo de forma clara e objetiva o comportamento esperado da aplicação.

---

### 1. Objetivo do sistema

**Descrição:**  
O sistema tem como objetivo calcular o Índice de Massa Corporal (IMC) de um usuário a partir do peso e da altura informados, apresentando o valor calculado e sua respectiva classificação.

---

### 2. Entradas do sistema

**Descrição:**  
O sistema deve solicitar ao usuário as seguintes informações:

- Peso, informado em quilogramas (kg);
- Altura, informada em metros (m).

**Regras:**  
- As entradas devem ser valores numéricos reais;
- Os valores informados devem ser positivos;
- A altura não pode ser igual a zero.

---

### 3. Processamento

**Descrição:**  
Após a entrada dos dados, o sistema deve calcular o IMC utilizando a seguinte fórmula:

IMC = peso / (altura × altura)

Em seguida, o sistema deve determinar a classificação do IMC com base em faixas predefinidas.

---

### 4. Classificação do IMC

**Descrição:**  
O sistema deve classificar o IMC conforme as seguintes faixas:

- IMC < 16.0 → Magreza grave  
- 16.0 ≤ IMC < 17.0 → Magreza moderada  
- 17.0 ≤ IMC < 18.5 → Magreza leve  
- 18.5 ≤ IMC < 25.0 → Saudável  
- 25.0 ≤ IMC < 30.0 → Sobrepeso  
- 30.0 ≤ IMC < 35.0 → Obesidade Grau I  
- 35.0 ≤ IMC < 40.0 → Obesidade Grau II  
- IMC ≥ 40.0 → Obesidade Grau III  

---

### 5. Saídas do sistema

**Descrição:**  
Após o processamento, o sistema deve exibir ao usuário:

- O valor do IMC calculado, formatado com duas casas decimais;
- A classificação correspondente ao IMC calculado.

---

### 6. Regras de negócio

**Descrição:**  
- Cada execução do sistema deve calcular um único IMC;
- O sistema deve utilizar exclusivamente os valores informados pelo usuário;
- O sistema não deve realizar diagnósticos médicos, apenas fornecer uma classificação informativa.

---

### 7. Comportamento esperado em caso de erro

**Descrição:**  
- Caso sejam informados valores inválidos (não numéricos, negativos ou altura igual a zero), o sistema deve informar o erro ao usuário de forma clara;
- O sistema não deve encerrar sua execução abruptamente sem apresentar uma mensagem explicativa.

---

### 8. Restrições e premissas

**Descrição:**  
- O sistema é executado em ambiente de console;
- Não há persistência de dados;
- O sistema não depende de integrações externas.

---



### Atividade 4 – Casos de Teste Formais (Partições de Equivalência e Análise de Valor Limite)

Este documento apresenta os casos de teste formais elaborados com base nas técnicas de **partições de equivalência** e **análise de valor limite**, considerando o comportamento esperado do sistema de cálculo de IMC.

---

## 1. Partições de Equivalência

### 1.1 Entradas válidas – Peso e altura positivos

**Descrição:**  
Valores numéricos positivos para peso e altura.

| Caso de Teste | Peso (kg) | Altura (m) | Resultado Esperado |
|--------------|----------|------------|--------------------|
| CT-01 | 70 | 1.75 | IMC calculado e classificação exibida corretamente |
| CT-02 | 50 | 1.60 | IMC calculado e classificação exibida corretamente |

---

### 1.2 Entradas inválidas – Peso negativo

**Descrição:**  
Peso informado com valor negativo.

| Caso de Teste | Peso (kg) | Altura (m) | Resultado Esperado |
|--------------|----------|------------|--------------------|
| CT-03 | -70 | 1.75 | Sistema deve rejeitar a entrada e informar erro |

---

### 1.3 Entradas inválidas – Altura negativa

**Descrição:**  
Altura informada com valor negativo.

| Caso de Teste | Peso (kg) | Altura (m) | Resultado Esperado |
|--------------|----------|------------|--------------------|
| CT-04 | 70 | -1.75 | Sistema deve rejeitar a entrada e informar erro |

---

### 1.4 Entradas inválidas – Altura igual a zero

**Descrição:**  
Altura informada igual a zero.

| Caso de Teste | Peso (kg) | Altura (m) | Resultado Esperado |
|--------------|----------|------------|--------------------|
| CT-05 | 70 | 0 | Sistema deve impedir o cálculo e informar erro |

---

### 1.5 Entradas inválidas – Dados não numéricos

**Descrição:**  
Valores não numéricos informados como entrada.

| Caso de Teste | Peso | Altura | Resultado Esperado |
|--------------|------|--------|--------------------|
| CT-06 | "abc" | 1.70 | Sistema deve informar erro de formato inválido |
| CT-07 | 70 | "xyz" | Sistema deve informar erro de formato inválido |

---

## 2. Análise de Valor Limite – Classificação do IMC

### 2.1 Limites inferiores e superiores das faixas de IMC

**Descrição:**  
Casos de teste próximos aos limites de classificação do IMC.

| Caso de Teste | IMC Calculado | Classificação Esperada |
|--------------|--------------|------------------------|
| CT-08 | 15.9 | Magreza grave |
| CT-09 | 16.0 | Magreza moderada |
| CT-10 | 16.9 | Magreza moderada |
| CT-11 | 17.0 | Magreza leve |
| CT-12 | 18.4 | Magreza leve |
| CT-13 | 18.5 | Saudável |
| CT-14 | 24.9 | Saudável |
| CT-15 | 25.0 | Sobrepeso |
| CT-16 | 29.9 | Sobrepeso |
| CT-17 | 30.0 | Obesidade Grau I |
| CT-18 | 34.9 | Obesidade Grau I |
| CT-19 | 35.0 | Obesidade Grau II |
| CT-20 | 39.9 | Obesidade Grau II |
| CT-21 | 40.0 | Obesidade Grau III |

---

### Atividade 5 – Justificativa dos Cenários de Teste

Este documento apresenta a justificativa para os cenários de teste definidos na Atividade 4, considerando a lógica de funcionamento do sistema e os riscos associados à aplicação no contexto de saúde digital.

---

### 1. Justificativa do uso de Partições de Equivalência

A técnica de partições de equivalência foi aplicada para agrupar conjuntos de entradas que produzem comportamentos semelhantes no sistema, reduzindo a quantidade de testes necessários sem comprometer a cobertura funcional.

As entradas de **peso e altura positivos** representam a partição válida principal, pois refletem o uso esperado da aplicação. Testar múltiplos valores dentro dessa partição garante que o cálculo do IMC funcione corretamente em condições normais.

As partições inválidas (peso negativo, altura negativa, altura igual a zero e entradas não numéricas) foram escolhidas devido ao alto risco de erro associado à ausência de validação de dados no sistema. Esses cenários podem levar a resultados incoerentes, falhas de execução ou encerramento inesperado da aplicação, comprometendo a confiabilidade do sistema.

---

### 2. Justificativa dos testes de Análise de Valor Limite

A análise de valor limite foi utilizada porque a classificação do IMC depende diretamente de intervalos numéricos bem definidos. Erros costumam ocorrer nos pontos de transição entre faixas, especialmente quando a lógica de comparação utiliza operadores relacionais de forma inadequada.

Os valores imediatamente abaixo, exatamente iguais e imediatamente acima de cada limite foram selecionados para garantir que:
- Cada faixa de classificação seja aplicada corretamente;
- Não ocorram sobreposições ou lacunas entre os intervalos;
- O sistema classifique corretamente valores críticos, como IMC igual a 18.5, 25.0, 30.0, 35.0 e 40.0.

---

### 3. Justificativa dos cenários de erro e robustez

Os cenários envolvendo entradas inválidas e exceções foram incluídos devido ao contexto de uso da aplicação. Sistemas da área de saúde exigem alto nível de robustez, pois erros de execução ou resultados incorretos podem induzir o usuário a interpretações equivocadas sobre sua condição física.

A ausência de tratamento de exceções e validação de dados aumenta o risco de falhas críticas, como divisão por zero e erros de conversão de dados. Testar esses cenários permite avaliar a tolerância a falhas do sistema e identificar pontos que necessitam de melhoria antes do lançamento.

---

### 4. Justificativa sob a perspectiva de risco

Os cenários de teste priorizam:
- Riscos funcionais, relacionados à classificação incorreta do IMC;
- Riscos técnicos, associados a falhas de execução e encerramento abrupto do sistema;
- Riscos de usabilidade, decorrentes da falta de mensagens claras e orientativas ao usuário.

A escolha desses cenários garante que os aspectos mais críticos da aplicação sejam avaliados, reduzindo a probabilidade de falhas em produção e aumentando a confiabilidade do sistema.

---




