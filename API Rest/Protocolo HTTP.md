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
