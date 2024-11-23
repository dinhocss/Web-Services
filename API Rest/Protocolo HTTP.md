# O protocolo HTTP

>É um protocolo de comunicação que fornece métodos para lidar com transferência de dados entre diferentes servidores.

## Os fundamentos HTTP

O protocolo HTTP trata-se de um protocolo de camada de aplicação. Foi desenvolvido para ser o mais flexível possível, podendo lidar com diferentes tipos de dados. Este protocolo segue o seguinte formato de requisições:

```
<método> <URL> HTTP/<versão>
<cabeçalho - um por linha>

<corpo da requisição>
```

Por exemplo, imagine um site que contenha um banco de dados referente a clientes. O endereço do site é `http://exemplo.com/clientes`. Ao digitarmos esse site na barra de endereço, a seguinte requisição será enviada para o servidor:

```
GET /clientes HTTP/1.1
Host: exemplo.com
Accept: text/html
```

**OBS**: Accept é um cabeçalho que define o tipo retornado pela requisição. No caso acima seria do tipo texto em html.

A requisição GET é utilizada para obter informações de alguma coisa sem precisar modificar o código da aplicação. Após enviarmos a requisição GET, o método irá retornar uma mensagem referente ao sucesso ou não da requisição. A mensagem retornada tem o seguinte formato:

```
HTTP/<versão> <código de status> <descrição do código>
<cabeçalhos>

<resposta>
```

Por exemplo, a resposta da requisição feita no exemplo anterior seria:

```
HTTP/1.1 200 OK
Content-Type: text/xml
Content-Lenght: 245
```
## Métodos HTTP

A versão atual do protocolo HTTP define oito métodos oficiais, sendo eles:
- GET
- POST
- PUT
- DELETE
- OPTIONS
- HEAD
- TRACE
- CONNECT

Cada um desses métodos diferem entre si em termos de idempotência, segurança e mecanismo de passagem de parâmetros. Vamos exemplificar cada um deles.

### Idempotência

>Um método HTTP é considerado idempotente se ao executá-lo mais de uma vez ele produzirá o mesmo efeito no servidor que executá-lo apenas uma vez.

A idempotência de um método é relativa às modificações que são realizadas do lado do servidor. Se a mesma requisição provocar alterações no servidor como se fosse uma única requisição, então ela será idempotente. Por exemplo, considere os métodos GET, POST, PUT e DELETE. GET irá retornar o conteúdo requisitado pela URL, portanto, não importa quantas vezes GET for utilizado, ele sempre retornará o mesmo conteúdo, fazendo dele idempotente. Já em relação a POST, há a criação de dados, portanto cada requisição criará algo diferente, fazendo com que POST não seja idempotente. No caso de PUT e DELETE ambos são idempotentes, já que uma mesma requisição PUT ou DELETE produzirá os mesmos resultados.

 ### Segurança

 Em relação a segurança, um método é considerado seguro se não realiza nenhuma modificação nos dados contidos. Em relação a idempotência e segurança temos as seguintes informações:
 
 |Método|Idempotente|Seguro|
 |---|---|---|
 |GET|Sim|Sim|
 |POST|Não|Não|
 |PUT|Sim|Não|
 |DELETE|Sim|Não|
 |HEAD|Sim|Sim|
 |OPTIONS|Sim|Sim|

### Tipos de passagens de parâmetros

Os métodos HTTP aceitam parâmetros de duas formas, os chamados *query parameters* e *body parameters*. Os query parameters são passados na própria URL da requisição. Por exemplo, considere a seguinte requisição para realizar uma busca no Google: ´HTTP://www.google.com.br/?q=HTTP´. Esta requisição faz com que o Google entenda que uma busca por HTTP está sendo realizada. 

Os query parameters são inseridos a partir do sinal de interrogação e são inseridos via **<chave>=<valor>**. Caso precisemos adicionar mais de um parâmetro, é necessário utilizar & para fazer a separação. Para representarmos espaço numa URL podemos utilizar + ou %20. Há uma limitação em relação ao método GET, pois o mesmo não consegue passar dados estruturados para o servidor. A passagem de parâmetros do método GET se dá via URL. Para passarmos dados estruturados precisamos utilizar o método POST, que passará os dados no corpo do método. Por exemplo, suponhamos que desejamos fornecer dados complexos ao servidor. A maneira de fazer isso é através do método POST, de acordo com o exemplo abaixo:

```
POST /clientes HTTP/1.1
Host: www.exemplo.com
Content-Type: text/html
Content-Lenght: 93

<cliente>
   <nome>Alexandre</nome>
   <dataNascimento>2012-01-01</dataNascimento>
</cliente>
```
## Cabeçalho

>São essencialmente um conjunto chave=valor que contém metadados sobre a requisição ou resposta.

Esses metadados informados no cabeçalho permite uma melhor comunicação entre cliente e servidor, uma vez que eles informam uma melhor maneira de como processar as informações. O cabeçalho pode informar uma série de coisas, sendo algumas delas:
- Qual o formato de resposta que o cliente aceita (JSON, html)
- O idioma preferido do cliente
- O tipo de navegador ou aplicação que está fazendo a requisição
- Detalhes sobre compressão e a persistência da conexão

Segue alguns dos principais cabeçalhos utilizados e seus significados:

### Cabeçalhos de requisição (do cliente para o servidor)

#### 1. Host:
- Indica o domínio ou o endereço DNS do servidor
- Ex: `Host: www.exemplo.com`

#### 2. User-Agent:
- Informa detalhes sobre o cliente (navegador, sistema operacional, etc)
- Ex: `User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)`

#### 3. Accept:
- Informa ao servidor quais formatos de resposta são aceitáveis
- Ex: `Accept: text/html, application/json`

#### 4. Accept-Language:
- Especifica o idioma preferido para resposta
- Ex: `Accept-Language: en-US,pt-BR`

#### 5. Accept-Encoding:
- Indica quais tipos de compressão o cliente aceita para economizar largura de banda
- Ex: `Accept-Encoding: gzip, deflate`

#### 6. Connection:
- Define se a conexão deve se manter aberta para outras conexões
- Ex: `Connection: keep-alive`

### Cabeçalhos de resposta (do servidor para o cliente)

#### 1. Content-Type:
- Indica o formato do conteúdo da resposta
- Ex: `Content-Type: text/html, application/json`

#### 2. Content-Lenght:
- Indica o tamanho do corpo da resposta, em bytes
- Ex: `Content-Lenght: 128`

#### 3. Cache-Control:
- Define políticas de cache para o cliente
- Ex: `Cache-Control: no-cache`

#### 4. Set-Cookie:
- Utilizado para enviar Cookies para o cliente
- Ex: `Set-Cookie: sessionId=abc123; HttpOnly`

### Resumindo

Cabeçalhos são metadados que auxiliam na comunicação entre cliente e servidor. Cada requisição e resposta possuem cabeçalhos padronizados, porém podemos também criar cabeçalhos personalizados. Por exemplo, considere a comunicação entre cliente-servidor abaixo:

```
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Accept: text/html
Accept-Language: en-US
```

O servidor pode responder com:
```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 3456
Cache-Control: max-age=3600
```

**OBS**: O cabeçalho Host é o único que é obrigatório. 

## Media Types

>Fornece uma forma padrão para identificar o formato dos dados que estão sendo enviados ou recebidos.

O Media Type é composto por duas palavras-chave separadas por '/': `<tipo-principal>/<subtipo>`. O tipo-principal indica a categoria geral do dado, por exemplo, imagem, vídeo, texto, etc. Já o subtipo indica o formato exato do tipo. Segue abaixo os principais Media Types:

### 1. text:
- Representa dados baseados em texto
- Ex: `text/html, text/plain`

### 2. application:
- Representa dados estruturados ou arquivos de aplicação
- Ex: `application/json, application/xml, application/pdf`

### 3. images
- Representa dados de imagens
- Ex: `image/png, image/jpeg`

### 4. audio
- Representa dados de audio
- Ex: `audio/mpeg, audio/wav`

### 5. video:
- Representa dados de vídeo
- Ex: `video/mp4, video/webm`

### 6. multi-part:
- Representa dados compostos por múltiplas partes (como formulários ou arquivos anexados)
- Ex: `multi-part:form-data, multi-part:byteranges`

O Media Type é utilizado com os cabeçalhos Accept e Content-Type, pois tratam-se de metadados que informam qual tipo de dado está sendo trabalhado entre cliente e servidor. Se houver parâmetros dentro de um Media Type utilizamos o demarcador ';' para defini-los. Por exemplo, `text/html;charset=utf-8`

**OBS**: Caso o cliente possa receber mais de um tipo de dado é possível definir prioridades em como um dado deve ser enviado ou lido. Por exemplo, `text/html,application/xml;q=0.9,*/*;q=0.8`, que significa que caso não haja um documento de texto html disponível, o cliente tem 90% de prioridade de receber dados do tipo application/xml e 80% de prioridade para receber dados de qualquer tipo.

## Código de Status

Toda solicitação que o cliente faz para o servidor retorna um código de status. Esses códigos são dividos em cinco famílias: 1xx, 2xx, 3xx, 4xx, 5xx, sendo:

- **1xx**: Informacionais
- **2xx**: Código de sucesso
- **3xx**: Códigos de redirecionamento
- **4xx**: Erros causados pelo cliente
- **5xx**: Erros originados no servidor

Tendo a lista acima como referência, vamos ver quais são os principais erros de cada categoria:

### 2xx

#### 200 - OK
- Indica que a operação indicada teve sucesso

#### 201 - Created
- Indica que o recurso desejado foi criado com sucesso. Deve retornar um cabeçalho *Location*, que deve conter a URL onde o recurso recem criado está disponível.

#### 202 - Accepted
- Indica que a solicitação foi recebida e será processada em outro momento. É tipicamente utilizada em requisições assíncronas, que não serão processadas em tempo real. Por esse motivo, pode retornar um cabeçalho *Location*, que trará uma URL que o cliente pode acessar para verificar se o recurso já está disponível ou não.

#### 204 - No Content
- Usualmente enviado em resposta a uma requisição PUT, POST ou DELETE, onde o servidor pode recusar-se a enviar o conteúdo.

#### 206 - Partial Content
- Utilizados em requisições GET parciais, ou seja, que demanda apenas parte do conteúdo amazenado no servidor (caso muito utilizado em servidores de download)

### 3xx

#### 301 - Moved Permanently
- Significa que o recurso solicitado foi realocado permanentemente. Uma resposta com o código 301 deve conter um cabeçalho *Location*  com a URL completa de onde o recurso está atualmente.

#### 303 - See Other
- É utilizado quando a requisição é processada, mas o servidor não quer enviar o resultado do processamento. Ao invés disso, o servidor envia a resposta com este código de status e o cabeçalho *Location* informando onde a resposta do processamento está.

#### 304 - Not Modified
- É utilizado, principalmente, em requisições GET condicionais- quando o cliente deseja ver a resposta apenas se ela tiver sido alterada em relação a uma requisição anterior.

#### 307 - Temporary Redirect
- Semelhante ao 301, mas indica que o redirecionamento é temporário, e não permanente.

### 4xx

#### 400 - Bad Request
- É uma resposta genérica para qualquer tipo de erro de processamento cuja responsabilidade é do cliente do serviço.

#### 401 - Unauthorized
- Utilizado quando o cliente está tentando realizar uma operação sem ter fornecido dados de autenticação (ou a autenticação for inválida).

#### 403 - Forbidden
- Utilizado quando o cliente está tentando realizar uma operação sem ter a devida autorização.

#### 404 - Not Found
- Utilizado quando o recurso solicitado não existe.

#### 405 - Method Not Allowed
- Utilizado quando o método HTTP utilizado não é suportado pela URL. Deve incluir um cabeçalho *Allow* na resposta, contendo a listagem dos métodos suportados (separados por ",").

#### 409 - Conflict
- Utilizado quando há conflito entre dois recursos. Comumente utilizado em resposta a criações de conteúdo que tenham restrições de dados únicos - por exemplo, criação de um usuário no sistema utilizando um *login* já existente.

#### 410 - Gone
- Semelhante ao 404, mas indica que um recurso já existiu nesse local.

#### 412 - Precondition Failed
- Comumente utilizada em resposta a requisições GET condicionais.

#### 415 - Unsupported Media Type
- Utilizado em resposta a clientes que solicitam um tipo de dados que não é suportado - Por exemplo, solicitar JSON quando o único formato de dados suportado é XML.

### 500 - Internal Server Error
- É uma resposta de erro genérica , utilizada quando nenhuma outra se aplica.

### 503 - Service Unavailable 
- Indica que o servidor está atendendo requisições, mas o serviço em questão não está funcionando corretamente. Pode incluir um cabeçalho *Retry-After*, dizendo ao cliente quando ele deveria tentar submeter a requisição novamente 

