# Aplicativo de Conferência PVD

A aplicação possuirá duas telas que ficarão abertas simultaneamente, ambas tendo um tamanho do qual possam ficar abertas uma no canto esquerdo e outra no canto direito. E visualmente, poderão ser utilizadas em conjunto com o retaguarda.

## Tela 1

A **"Primeira Tela Principal"**, terá por padrão, uma tela simples de outputs **"Informa Produtos"**, que irá exibir as informações de cada produto bipado, essas informações serão texto e poderão ser copiadas. As informações serão:

-  *Descrição*
-  *Cód. Interno*
-  *Endereço*
-  *Fornecedor*
-  *Custo*
-  *Grupo*

##### Janela alterável

Essa tela será alterada, caso o usuário clique no botão ***'Relatar ocorrência'***, que estará **"Segunda Tela Principal"**. E voltará a exibir a tela **"Informa Produtos"**, quando o usuário clicar no botão *'Salvar Ocorrência'*.

## Tela 2

### Botões Fixos

Na **"Segunda Tela Principal"**, terão botões fixos na parte inferior que seriam:

#### 1 - *'Pesquisar produto'* 

Abriria uma  janela flutuante "Pesquisa", onde o usuário conseguira pesquisar um produto, pelo código de barras, descrição ou código interno.

#### 2 - *'Ativar/Desativar Bipador'*

Tudo que é digitado no teclado será capturado quando essa opção estiver ativo.

#### 3 - *'Relatar Ocorrência'*

Irá atualizar a janela **"Primeira tela principal"**, para uma tela **"Relatar Ocorrência"**, onde será possível dar 2 inputs: 

1 - *'Número da Filial'*, 
2 - '*Produtos*', com um botão ***'Add Pdt**'* ao lado, integrando a funcionalidade ***'Pesquisar produto'.*** 

###### 'Add Pdt'

- Ele abrirá uma janela flutuante **"Pesquisa Ocorrência"**, onde haverá a barra de pesquisa, com um botão *'**Adicionar*'** ao lado, que adiciona o código interno desse produto que foi bipado na *[listaOcorrenciasProdutos]*, esse botão ***'Adicionar'*** também é ativado com a tecla Enter. Haverá o botão ***'Salvar'*** que fecha essa janela flutuante  **"Pesquisa Ocorrência"** e retorna todos os códigos internos da [listaOcorrenciasProdutos], no caixa de texto do input '*Produtos'*, separando-os por vírgula. 

Haverão outros inputs nessa tela, dependendo de qual tratativa estiver sendo feita, de acordo com a variável **'TelaAtiva'**. Além disso, também haverá o botão *'**Salvar Ocorrência'***, que retorna um dataframe *'ocorrencia'* contendo as colunas: 

- 'Número da Filial' / 'Produto' / 'x' / 'y'

Sendo que o que irá ditar o número de linhas, será a quantidade de códigos internos, esse relatório  *'relatorioOcorrencias'*, também terá mais colunas, de acordo com a variável **'TelaAtiva'**.

#### 4 - '*Relatório Ocorrência*'

Irá fazer uma junção de todos os dataframes *'ocorrencia'* em um único dataframe *'relatorioOcorrencia'* e retornará um arquivo Excel. O retorno desse botão dependerá da variável **'TelaAtiva'**, sendo que será possível gerar relatório de excessos e de descartes.

#### 5 - '*Carregar dados'*

Será utilizado para carregar os dados do arquivo parquet, retornando um dicionário.

#### 6 - *'Ícone Tema'*

Será utilizado para alterar entre os temas claro e escuro.

### Botões de Alteração

Na parte superior da **"Segunda Tela Principal"**, haverão dois botões que irão atualizar a tela (mantendo os botões fixos), sendo necessário uma variável de '**TelaAtiva**', que será nula por padrão, para saber qual tela está ativa. Os botões serão:

#### 7 - *'Conferência Excessos'*

Irá atualizar a a janela **"Segunda Tela Principal"** para uma tela **"Conferir Excessos"**, contendo 2 inputs: *'Número NF'* e *'Número Conferência'*, terá também o botão ***'Iniciar conferência'***, que irá salvar esses dois inputs e alterar a variável de **'TelaAtiva'** para '*excesso*'. 

Nessa tela, haverá um botão ***'Finalizar conferência'***, que ao ser clicado, irá abrir uma janela flutuante com a tela **"Finalizar Conferencia"** contendo uma caixa de *seleção* com três opções:

1.  'OK', 
2. 'Passou' 
3. 'Sobrou' 

Na tela **"Finalizar Conferencia"**, haverá um botão ***'Finalizar'***. Ao finalizar, a variável de **'TelaAtiva'** voltará a ser nula, e será gerado um dataframe 'relatórioConf' contendo as colunas:

- *'Número NF' / 'Número Conferência' / 'Resultado'*

Sendo que a linha de 'Resultado', será o valor da *caixa de seleção* do botão ***'Finalizar conferência'***. 

A cada conferência salva, é adicionado uma nova linha no dataframe 'relatórioConf'. Por último, haverá o botão ***'Relatório Conferências***', que permitirá salvar o dataframe das conferências em um arquivo Excel.

##### Relatório Ocorrência Excesso

Caso o usuário aperte o botão ***'Relatar ocorrência'***  na conferencia de excessos, haverá mais um input dentro da tela **"Relatar Ocorrência"**, que será uma *caixa de seleção* que terá as opções:

1. 'Fora do Padrão'
2. 'Vencido' 
3. 'Danificado'

Ao salvar a ocorrência, cada linha do dataframe *'ocorrencia'* também terá as colunas que foram obtidos ao clicar em ***'Iniciar conferência'***:

- *'Número NF' / 'Número Conferência'*

#### 8 - *'Conferência Descartes'* 

Irá atualizar para uma tela **"Conferir Descarte"**, contendo 2 botões: ***'Retorno Filial***' e ***'Lojinha***', ambos alteram a variável de '**TelaAtiva**', para *'descarte'*. 

##### 'Retorno Filial'

Ao clicar no botão ***Retorno Filial'***, a janela **"Segunda Tela Principal"** irá atualizar para uma tela **"AV Filial"**, onde serão exibidas informações a cada produto bipado de acordo com a demanda de cada filial, obtidas do parquet de 'Demanda'. As informações serão: 

- *Descrição*
- *Código Interno*
- *Filial Destino*
- *Demanda*
- *Quantidade Restante*

Cada código bipado será salvo em um dataframe *'pedidoVenda*', com as colunas:

 - *'Código Interno' / 'Descrição' / 'Filial Destino'.*
 
 Nessa tela **"AV Filial"**, também haverá o botão ***'Relatório Pedido Venda'***, que irá retornar um arquivo Excel, que terá as mesmas colunas do dataframe *'pedidoVenda'*, porém com valores únicos de código interno, e uma nova coluna chamada *'Quantidade'*, com a soma de cada código interno repetido, basicamente:

- *'Código Interno' / 'Descrição' / 'Filial Destino' ; 'Quantidade'*

O botão ***'Relatório Pedido Venda'***, irá atualizar a janela **"Segunda Tela Principal"**, retornando para a tela **"Conferir Descarte"**, e alterando a variável "TelaAtiva" para nulo.

##### 'Lojinha'

Ao clicar no botão ***'Lojinha'***, a janela **"Segunda Tela Principal"** irá atualizar para uma tela **"AV Lojinha"**, onde  haverá uma uma barra de pesquisa, integrando a funcionalidade do ***'Pesquisar produto'***. Ao apertar Enter nessa barra de pesquisa, seria exibido as seguintes informações:

- *Descrição*
- *Código Interno*
- *Custo*

E aparecerá abaixo, um input *'Data Vencimento'.* E um botão ***'Adicionar'*** abaixo, que ao ser clicado geraria um dataframe 'relatorioLojinha', com as colunas:

*'Descrição' / 'Código Interno' / 'Custo' / 'Data Vencimento'.*

Nessa tela **"AV Lojinha"**, também haverá o botão  ***'Relatório Lojinha'***, que irá retornar um arquivo Excel do dataframe 'relatorioLojinha' e irá atualizar a janela **"Segunda Tela Principal"**, retornando para a tela **"Conferir Descarte"**, e alterando a variável "TelaAtiva" para nulo.

##### Relatar Ocorrência Descarte

As telas **"Retorno Filial"** e **"Lojinha"** geralmente serão utilizada em conjunto a de relatar ocorrências, quando o usuário aperta o botão ***'Relatar ocorrência'*** na conferencia de descartes, haverão mais dois inputs na tela de **"Relatar ocorrência"**, serão duas caixas de seleção: 

Validade

1. 'Validade Longa' 
2. 'À Vencer'  

Estado

1. 'Ótimo Estado' 
2. 'Bom Estado' 
3. 'Faltando Parte'
