## 📖 Índice

1. [Introdução](#introdução)
2. [Objetivos](#objetivos)
3. [Metodologia](#metodologia)
4. [Pontos Positivos](#pontos-positivos)
5. [Pontos Negativos](#pontos-negativos)
6. [Avaliação CPU vs GPU](#avaliação-cpu-vs-gpu)
7. [Resultados e Percepções Pessoais](#resultados-e-percepções-pessoais)
8. [Conclusão](#conclusão)

---

## Introdução

Este repositório apresenta a reprodução e análise prática de um modelo Transformer aplicado à tarefa de tradução automática de frases do Português para o Inglês. O trabalho é baseado no tutorial oficial do TensorFlow, mas com adaptações e comentários críticos que visam destacar tanto os aspectos técnicos quanto as limitações do método.

O Transformer, introduzido no artigo clássico “Attention is All You Need” (Vaswani et al., 2017), revolucionou o campo de Processamento de Linguagem Natural (PLN) ao substituir arquiteturas recorrentes (RNNs, LSTMs) e convolucionais por um mecanismo de autoatenção (self-attention). Essa inovação permitiu ganhos expressivos em desempenho, paralelismo e capacidade de capturar dependências de longo alcance em sequências de texto, tornando-se a base de modelos amplamente utilizados, como BERT, GPT e T5.

Neste projeto, foi implementada uma versão reduzida do Transformer para fins educacionais, utilizando o dataset TED Talks (Português ↔ Inglês), disponibilizado pelo TensorFlow Datasets. O foco principal foi compreender:

Como o modelo é construído a partir de camadas de embedding, codificação posicional, atenção multi-cabeças e feed-forward.

- Como organizar e treinar um pipeline eficiente de dados com tf.data.

- O impacto do treinamento em diferentes hardwares (CPU vs GPU).

- A importância de técnicas auxiliares, como scheduler de taxa de aprendizado e métricas mascaradas, para garantir estabilidade no aprendizado.

Além de reproduzir traduções automáticas, o projeto inclui visualizações de mapas de atenção, permitindo interpretar como o modelo associa palavras entre os dois idiomas, e a exportação do modelo treinado, viabilizando seu uso em aplicações reais.

---

## Objetivos

* **Reproduzir** o tutorial original de tradução automática utilizando Transformer.
* **Documentar** percepções pessoais sobre a experiência de implementação e execução.
* **Comparar** o desempenho do treinamento em CPU e GPU.
* **Refletir** sobre as aplicações práticas e os desafios de usar Transformers em cenários reais.

---

## Metodologia

1. **Implementação**: execução do notebook `tutorial_transformer_revised.ipynb`, que possui 82 células de código e 155 células de documentação em Markdown.
2. **Treinamento**: rodado em ambientes distintos — CPU e GPU.
3. **Avaliação**: análise qualitativa (facilidade de aprendizado, clareza do código) e quantitativa (tempo de treinamento, escalabilidade).
4. **Documentação**: registro de pontos positivos e negativos, além da experiência pessoal durante a execução.

---

## Pontos Positivos

* **Clareza e progressão pedagógica**: o tutorial conduz o leitor passo a passo, tornando conceitos complexos mais acessíveis.
* **Estrutura modular do código**: funções e classes bem separadas facilitam experimentação e personalização.
* **Integração com `tf.keras`**: uso de API de alto nível que permite callbacks, métricas e otimizadores sem esforço adicional.
* **Resultados visíveis**: mesmo com dataset reduzido, é possível observar aprendizado real nas traduções.
* **Exposição ao mecanismo de *self-attention***: fundamental para compreensão prática de como os Transformers funcionam.

---

## Pontos Negativos

* **Tempo de execução em CPU**: excessivamente elevado, inviabilizando múltiplos testes ou ajustes de hiperparâmetros.
* **Complexidade conceitual**: a quantidade de novos conceitos (positional encoding, máscaras, multi-head attention) pode sobrecarregar iniciantes.
* **Alto custo computacional**: consumo significativo de memória, especialmente em GPUs menores, podendo gerar erros de *out of memory*.
* **Dataset limitado**: base de dados pequena não reflete o verdadeiro potencial do modelo.
* **Pouca exploração de hiperparâmetros**: o tutorial segue configurações fixas, reduzindo a experimentação.

---

## Avaliação CPU vs GPU

### Treinamento em CPU

* **Tempo por época:** elevado, chegando a horas mesmo para datasets pequenos.
* **Produtividade:** inviável para iterações rápidas.
* **Utilidade:** apenas para rodar células isoladas e entender o fluxo do código.

### Treinamento em GPU

* **Tempo por época:** reduzido de forma significativa (ordens de magnitude mais rápido).
* **Produtividade:** permite explorar parâmetros, rodar múltiplas épocas e observar convergência da perda.
* **Utilidade:** essencial para qualquer aplicação prática ou acadêmica que envolva Transformers.

📊 **Resumo Comparativo**

| Aspecto            | CPU                           | GPU                              |
| ------------------ | ----------------------------- | -------------------------------- |
| Tempo de treino    | Muito alto (horas/dias)       | Baixo (minutos/horas)            |
| Produtividade      | Frustrante, pouco prática     | Fluida, permite experimentação   |
| Escalabilidade     | Quase inviável                | Suporta datasets maiores         |
| Consumo energético | Elevado (processo prolongado) | Mais eficiente em treinos curtos |

---

## Resultados e Percepções Pessoais

* O tutorial é extremamente didático e cumpre bem o papel de **introduzir o Transformer**.
* No entanto, percebi que **sem GPU, o aprendizado é quase inviável**: a experiência em CPU é limitada a execuções de teste, sem possibilidade real de explorar aprendizado profundo.
* A utilização em GPU mostrou a **evolução real das traduções** ao longo das épocas, o que reforça o valor da aceleração por hardware.
* Pessoalmente, o maior ganho foi a **compreensão do self-attention**, algo que antes parecia apenas teórico e abstrato.
* Apesar disso, fiquei com a sensação de que para **aplicações concretas**, seria necessário:

  * usar datasets maiores,
  * investir em ajustes de hiperparâmetros,
  * e dispor de infraestrutura mais completa.