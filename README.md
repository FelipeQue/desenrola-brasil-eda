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

Utilizei a biblioteca Logging para registrar o processo de extração dos dados.

## Comentários

RF01: Como o dataset foi criado pelo governo brasileiro (através do Banco Central), que tipicamente usa o separador ; e vírgula para decimais, foi necessário usar o parâmetro `sep=';'` e `decimal=','` ao ler o arquivo CSV com o Pandas.

RF01: O dataset é bastante limpo. Portanto, para fins de demonstração de técnicas de limpeza de dados, foi criado um processo de "sujar" o dataset, introduzindo valores nulos, strings com espaços, datas inválidas e valores extremos.

Consistência de idioma: todas as funções e variáveis do projeto, nomes de branches e commits no Github estão nomeadas em inglês, enquanto os comentários e relatórios parciais estão em português para facilitar a compreensão da equipe que corrigirá o projeto, assim como o dataset em si que é produzido pelo Banco Central do Brasil.