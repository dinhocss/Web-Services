> REST é baseado nos conceitos do Protocolo HTTP

REST utiliza dos conceitos de HTTP para realizar a conexão entre cliente e servidor, sendo esses conceitos base para a web. Quando um cliente envia uma solicitação para o servidor por exemplo, `GET /users`, o servidor retorna algum dado para o cliente. Aqui o cliente pode ser o navegador utilizado e o servidor a fonte de informação que se deseja acessar. 

## Semântica de recursos

Todo serviço em REST é baseado em recursos. Um recurso representa qualquer entidade ou dado que se deseja representar. Por exemplo, imagine uma cervejaria online. A URL referente as cervejas disponíveis é dada por `cervejaria.com/cervejas`. A página referente as cervejas é um recurso, e esse recurso pode ser acessado enviando uma solicitação GET para `/cervejas`. O servidor irá responder a requisição enviando o recurso desejado, que nesse caso é uma lista de cervejas disponíveis. 

Todo recurso possui um identificador e um endereço (URL) unicos. A URL, além de ser única, deve ser também significativa. Por exemplo, `/cervejas` é significativa, e indica todas as cervejas disponíveis. `/cervejas/1` indica a cerveja de ID 1, sendo também um recurso. Esse ID é o identificador do recurso `/cervejas`. O identificador pode ter qualquer formato. Por exemplo, podemos definir que os identificadores de cervejas é o código de barras de uma cerveja específica, sendo assim, poderíamos ter `/cervejas/20331`. Mais de um tipo de identificador pode ser usado para um recurso.

**OBS:** É importante criar um padrão para todos os seus recursos, de modo que facilite a leitura das requisições.

## Interação por métodos

Para a interação entre URL e cliente ser feita é necessário utilizar os métodos HTTP. As URLs e os recursos disponíveis nela são estáticas. Para realizarmos alguma modificação em cima dos recursos disponibilizados pela URL nós precisamos utilizar os métodos HTTP. Cada método pode realizar alguma ação em cima do recurso fornecido pela URL. Segue abaixo um exemplo dos métodos mais comuns em REST e como utilizá-los:

|Método HTTP|Ação|Descrição|Exemplo de uso|
|---|---|---|---|
|GET|Ler ou buscar|Recupera os dados do recurso|`GET /cervejas`(todas)|
||||`GET /cervejas/1`(uma)|
|POST|Criar|Envia dados ao servidor para criar um novo recurso|`POST /cervejas`(nova)|
|PUT|Atualizar/substituir completamente|Atualiza os dados de um recurso existente ou cria se ele não existir (idempotente).|`PUT /cervejas/1`(editar)|
|DELETE|Apagar|Remove o recurso identificado pela URL|`DELETE /cervejas/1`(deletar)|

### CRUD

CRUD diz respeito as operações básicas de criação, leitura, atualização e exclusão de dados em um sistema. Essas operações são básicas em praticamente todo sistema que utiliza banco de dados para manipulação de dados. CRUD serve como base para gerenciamento de dados em aplicativo, e relaciona-se com os métodos HTTP, onde:

* **CREATE(POST)**: Cria um novo recurso.
* **READ(GET)**: Lê os dados disponíveis de um recurso.
* **UPDATE(PUT)**: Atualiza um recurso existente.
* **DELETE(DELETE)**: Remove um recurso específico.


## Representações distintas

Um recurso REST pode ser representado de várias maneiras diferentes. O conceito de representação de um recurso indica quais serão os tipos retornados para os dados solicitados. O cabeçalho `Accept` é utilizado para definir qual será o formato da resposta que o cliente irá receber do servidor.

### Explicando como a distinção funciona

Quando realizamos uma solicitação para um recurso (por exemplo, `GET /cervejas`) o mesmo recurso pode ser disponibilizado em vários formatos diferentes. O cabeçalho `Accept` é o responsável por indicar qual será o formato da resposta do recurso. Segue abaixo alguns exemplos de valores que podem ser passados para o cabeçalho `Accept`:
* application/json (espera-se que a resposta seja em formato JSON)
* application/xml (espera-se que a resposta seja em formato XML)
* image/* (espera-se que a resposta seja em formato de qualquer tipo de imagem - JPEG, PNG, etc.)

**OBS**: Podemos adicionar mais de um tipo de mídia no cabeçalho `Accept`, e o servidor vai retornar o primeiro tipo de mídia que ele consegue fornecer. Porém, o primeiro tipo listado é priorizado. 

Exemplo, uma requisição GET para o endereço `/cervejas/1` pode ter o cabeçalho `Accept` fornecido da seguinte maneira:

```
GET /cervejas/1 HTTP/1.1
Host: cervejaria.com
Accept: application/json, application/xml
```

## Uso correto de status codes

Algo que REST também considera é o uso correto dos status codes HTTP. Status codes são códigos númericos utilizados para informar a resposta de alguma requisição feita ao servidor.  


