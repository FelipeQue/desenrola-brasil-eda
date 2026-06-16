# DataView: Exploração e Análise de Dados do programa Desenrola Brasil

Projeto de análise exploratória dos dados do programa Desenrola Brasil desenvolvido em Python através de um Jupyter notebook. O notebook lê, limpa, transforma,
analisa e visualiza um dataset, proporcionando métricas e informações. Este projeto é parte da avaliação do curso Desenvolvimento de IA para Análise Preditiva do programa SCTEC.

## Os dados: Desenrola Brasil

Foi escolhido um conjunto de dados real do programa Desenrola Brasil, um programa de renegociação de dívidas de pessoas físicas inadimplentes. O dataset é [disponibilizado pelo Banco Central do Brasil](https://dadosabertos.bcb.gov.br/dataset/desenrola-brasil) e contém informações sobre as operações de renegociação, incluindo o número de operações, o volume financeiro renegociado e a distribuição por tipo de operação, instituição financeira e unidade federativa.

## Tecnologias utilizadas (e suas versões)

- Python 3.14.3
- Jupyter Notebook 7.5.7
- Pandas 3.0.3
- Numpy 2.4.6
- Matplotlib 3.11.0
- Seaborn 0.13.2

Durante o desenvolvimento deste projeto foi utilizado um ambiente virtual (venv) para gerenciar as dependências do projeto, garantindo que as bibliotecas necessárias estejam isoladas.

Utilizei a biblioteca Logging para registrar o processo de extração dos dados e tratamento de outliers.

## Comentários

### Idioma

Todas as funções e variáveis do projeto, nomes de branches e commits no Github estão nomeadas em inglês, enquanto os comentários e relatórios parciais e este README estão em português para facilitar a compreensão da equipe que avaliará o projeto — assim como o dataset em si que é elaborado pelo Banco Central do Brasil.

### Extração dos dados

- Como o dataset foi criado pelo governo brasileiro (através do Banco Central), que tipicamente usa o separador ; e vírgula para decimais, foi necessário usar o parâmetro `sep=';'` e `decimal=','` ao ler o arquivo CSV com o Pandas.

- O dataset é bastante limpo. Portanto, para fins de demonstração de técnicas de limpeza de dados, foi criado um processo de "sujar" o dataset, introduzindo valores nulos, strings com espaços, datas inválidas e valores extremos.

### Limpeza dos dados

- Foi feita a limpeza de valores textuais, removendo espaços vazios antes ou depois do texto, bem como unificando em apenas um espaço caso houvesse mais de um;
- Foi feita a transformação da coluna de data, convertendo os valores para objetos datetime e removendo registros com datas inválidas;
- Foi criada uma função auxiliar para preencher os valores nulos na coluna de nome do conglomerado financeiro tomando como base o código do conglomerado financeiro, já que cada código corresponde a uma instituição financeira específica. (imputação baseada em mapeamento);
- Foram removidos registros em que o valor "tipo" não correspondia a uma das faixas possíveis do programa. Só existem 3 faixas no programa Desenrola Brasil (1, 2 e 3); valores fora disso são inválidos.
- Foram removidos a coluna de código do conglomerado financeiro, já que a coluna de nome do conglomerado financeiro é mais legível e já contém a mesma informação.
- Foram removidos os registros com valores nulos restantes (46) e duplicados (428).

Ao final da limpeza o dataset passou de 11658 registros para 10598 (o número original antes de ter sido sujo), ou seja, foram removidos 1060 registros durante o processo de limpeza.

### Tratamento de outliers

Depois de utilizar o método IQR para identificar os outliers, foram encontrados e removidos 2399 registros. Esse número representa um percentual significativo do dataset, indicando que o método do IQR não é adequado para tratar os outliers presentes nesse dataset. Para confirmar essa impressão, foram plotados gráficos de distribuição que confirmaram: a distribuição dos dados é altamente assimétrica e contém muitos valores extremos, o que faz com que o método do IQR identifique uma quantidade excessiva de outliers.

INFO - Coluna 'NUMERO_OPERACOES': Encontrados 1848 outliers (limite_inferior=-107.50, limite_superior=184.50)
INFO - Coluna 'VOLUME_OPERACOES': Encontrados 1685 outliers (limite_inferior=-382135.32, limite_superior=639915.60)
v1=10598 | v2=8199 | removidas=2399

Apliquei portanto uma escala logarítmica ao método IQR para tentar reduzir a influência dos valores extremos e obter uma detecção de outliers mais realista para esse dataset.

Para que a função siga sendo flexível, foi adicionado um parâmetro `logarithmic` que, quando definido como `True`, aplica a transformação logarítmica aos dados antes de calcular os limites do IQR. Isso permite que a função seja utilizada tanto para dados com distribuição normal quanto para dados com distribuição altamente assimétrica e valores extremos, como é o caso deste dataset.

INFO - Coluna 'NUMERO_OPERACOES': Encontrados 29 outliers (limite_inferior=-0.98, limite_superior=9689.63)
INFO - Coluna 'VOLUME_OPERACOES': Encontrados 0 outliers (limite_inferior=-0.67, limite_superior=872928944.90)
v1=10598 | v2=10569 | removidas=29

A versão v2 será o dataset utilizado nas etapas seguintes de análise.

### Criar Colunas Derivadas com Transformações