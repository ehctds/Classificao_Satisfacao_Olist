Introdução
O projeto tem como objetivo prever a satisfação dos clientes com base nos comentários deixados nas avaliações. Utilizamos o dataset da Olist, que é a maior marketplace online do Brasil. O dataset contém informações detalhadas sobre transações realizadas na plataforma, incluindo produtos, clientes, vendedores e avaliações.

Escolha do Dataset
O dataset escolhido foi o olist_order_reviews_dataset.csv que contém 99.224 linhas com as seguintes colunas:

review_id: Identificador único de cada avaliação.

order_id: Identificador único do pedido associado à avaliação.

review_score: Nota da avaliação (1 a 5).

review_comment_title: Título do comentário.

review_comment_message: Comentário opcional deixado pelo cliente.

review_creation_date: Data de criação da avaliação.

review_answer_timestamp: Data e hora em que a avaliação foi respondida.

Tratamento dos Dados
Os dados foram filtrados para manter apenas review_comment_message e review_score. Linhas com valores nulos em review_comment_message foram removidas. As colunas foram renomeadas para texto e review_score. O dataset resultante ficou com 40.997 linhas.

Análise Exploratória
Os dados foram explorados para entender a distribuição das notas e a polarização dos comentários:

Notas 1 e 2 foram rotuladas como 0 (clientes insatisfeitos).
Notas 4 e 5 foram rotuladas como 1 (clientes satisfeitos).
O dataset binário foi preparado para tokenização.
Tokenização e Pré-processamento
O texto foi transformado em sequências numéricas, ajustando o tamanho das sequências para 120. As palavras fora do vocabulário foram substituídas por um token especial <OOV>.

Implementação da Rede Neural
Baseado nos conceitos da dimensão VC e regra de ouro, optamos por utilizar duas camadas: a primeira com 31 neurônios e activation='tanh', e a segunda camada com 1 neurônio e activation='sigmoid' para a classificação binária.
O otimizador Adam foi configurado com uma taxa de aprendizado de 0.01.
A função de perda utilizada foi binary_crossentropy e a métrica de avaliação foi accuracy.
Utilizou-se a técnica de early stopping para evitar overfitting.

Implementação da Árvore de Decisão
Construímos uma árvore de decisão, calculamos Ein e Eout e analisamos a existência de overfitting.
Realizou-se a regularização do valor de alpha usando o algoritmo de Minimal Cost-Complexity com cross validation.

Comparação entre Modelos
Comparação entre Rede Neural, Árvore de Decisão, Multinomial Naive Bayes e XGBoost.
O modelo XGBoost apresentou a maior acurácia.

Resultados:

Análise Exploratória: 

![image](https://github.com/ehctds/Classificao_Satisfacao_Olist/assets/100098820/48ad8b1a-892e-4904-a67e-e3368c2931b9)

![image](https://github.com/ehctds/Classificao_Satisfacao_Olist/assets/100098820/5015b422-88a7-4891-be28-ab7fda3e8761)

![image](https://github.com/ehctds/Classificao_Satisfacao_Olist/assets/100098820/a3c8b2c4-5c67-4634-a8ff-46770caf738f)

Rede Neural: 

![image](https://github.com/ehctds/Classificao_Satisfacao_Olist/assets/100098820/f5b6f7af-f351-4466-9bbb-f1ff6bee6a30)

![image](https://github.com/ehctds/Classificao_Satisfacao_Olist/assets/100098820/c6a8fc81-b98b-4d48-be09-555b6b0475e4)

![image](https://github.com/ehctds/Classificao_Satisfacao_Olist/assets/100098820/e421b7af-e232-4e13-b1a9-8427a8e9d4b0)

acurácia: 75% 

Árvore de Decisão

![image](https://github.com/ehctds/Classificao_Satisfacao_Olist/assets/100098820/f240703c-0f6f-4620-85c1-e277a01ecc6a)

![image](https://github.com/ehctds/Classificao_Satisfacao_Olist/assets/100098820/0f5f0ff3-70aa-4408-85c8-01c84133a209)

![image](https://github.com/ehctds/Classificao_Satisfacao_Olist/assets/100098820/df4c66d3-442a-4651-9ba4-02e769e833f4)

![image](https://github.com/ehctds/Classificao_Satisfacao_Olist/assets/100098820/448f7040-31cf-4515-b935-7858be9ceef5)

Acurácia: 76% 

Comparação entre os modelos: 

![image](https://github.com/ehctds/Classificao_Satisfacao_Olist/assets/100098820/d125be5e-b0a0-48ba-91b4-18bd10402e9b)

![image](https://github.com/ehctds/Classificao_Satisfacao_Olist/assets/100098820/a777ea4e-f236-4187-bbb1-b9cf190b5790)


Potencial de Melhorias

Utilização de modelos de redes neurais mais avançados, como LSTM, para capturar dependências temporais e contextuais complexas em textos.

Considerações Finais
Os testes mostraram que o XGBoost é o modelo mais eficaz para a classificação deste conjunto de dados. No entanto, modelos de redes neurais recorrentes poderiam potencialmente melhorar a acurácia.


Para um relatório mais completo: https://docs.google.com/document/d/1Cjzd11cFIjouz-5GZpK314n3sEuRqyNs2z2rm0277Xw/edit?usp=sharing
