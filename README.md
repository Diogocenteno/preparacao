Explicação do Código
Importações e Inicialização do Spark:

O código começa com a importação de módulos necessários, como SparkSession para inicializar o Spark e várias funções de transformação e modelagem.
A sessão do Spark é inicializada com o nome "Leitura Parquet".
Carregar o Arquivo Parquet:

O código carrega um arquivo Parquet em df_video. Certifique-se de que o caminho do arquivo está correto e que o arquivo Parquet existe nesse local.
Adicionar a Coluna 'Month':

Uma nova coluna chamada "Month" é adicionada com o mês extraído da coluna Published At (presumivelmente, uma data).
A função month() é usada para extrair o mês.
Adicionar a Coluna 'Keyword Index':

A coluna Keyword é indexada com o StringIndexer, que converte valores de texto em valores numéricos, sendo útil para modelagem. O código renomeia a coluna Keyword com espaço para keyword (presumivelmente para garantir um nome correto de coluna).
O StringIndexer é usado para criar uma coluna de índice numérico chamada "Keyword Index".
Criar o Vetor 'Features':

A coluna Year é convertida para o tipo IntegerType para garantir que seja tratada como numérica durante a modelagem.
O VectorAssembler é utilizado para combinar várias colunas (Likes, Views, Year, Month e Keyword Index) em um vetor chamado "Features", que será usado como entrada para o modelo de regressão.
Adicionar a Coluna 'Features Normal':

O Normalizer é usado para normalizar as características, aplicando a normalização L2 (p=2.0) ao vetor "Features", criando a coluna "Features Normal". Isso é útil para garantir que os dados estejam em uma escala semelhante.
Redução de Características com PCA:

O PCA (Análise de Componentes Principais) é usado para reduzir as dimensões dos dados. O número de componentes principais (k=1) é escolhido, o que significa que a transformação resultará em uma única coluna PCA.
O PCA é ajustado e transformado sobre os dados.
Divisão dos Dados em Treinamento e Teste:

A divisão dos dados em treinamento (80%) e teste (20%) é feita com a função randomSplit(). O parâmetro seed=42 garante que a divisão seja reproduzível.
Treinamento do Modelo de Regressão Linear:

O modelo de regressão linear é treinado usando o vetor normalizado "Features Normal" e a coluna Comments como rótulo (variável dependente).
O modelo é avaliado com o evaluate() no conjunto de teste, gerando o R² (coeficiente de determinação) e o RMSE (erro quadrático médio).
Salvar o DataFrame em Parquet:

O DataFrame df_video é salvo em formato Parquet no caminho especificado.
