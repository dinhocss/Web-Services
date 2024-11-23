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
