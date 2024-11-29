# Introdução a Web Services

>Web Services são serviços de comunicação entre sistemas diferentes por meio da web.

A internet é baseada numa arquitetura Cliente-servidor, onde um cliente irá fazer uma requisição para o servidor, e este lhe dará uma resposta seguindo parâmetros definidos no momento da requisição. É baseado nesse contexto que os web services são descritos. 

Esses serviços web permitem que os diferentes sistemas possam lidar com dados de maneira padronizada, ou seja, mesmo que os servidores tenham linguagens diferentes, os dados serão processados da mesma maneira. Esses dados podem ser trocados via arquivos XML ou JSON.

Web services frequentemente utilizam protocolo [HTTP]() para realizar a comunicação entre servidor e cliente, através de métodos POST, GET, UPDATE e DELETE. 

Existem dois tipos principais de Web Services:
1. **SOAP(Simple Object Access Protocol)**: Um protocolo mais formal, complexo e estruturado para troca de mensagens entre sistemas, geralmente através de XML.
2. **REST(Representational State Transfer)**: Uma arquitetura mais simples e moderna, que geralmente utiliza JSON para troca de dados.

## Breve explicação sobre SOAP

SOAP é um protocolo de troca de mensagens entre diferentes sistemas, utilizando XML como troca de dados. É um protocolo bastante robusto, porém muito verboso. É ideal para sistemas que precisem de uma segurança maior, porém pode não ser recomendado para sistemas em que o espaço em disco importa, já que pelo fato do arquivo XML ser muito verboso, há muito código e regras rígidas nesses dados. Portanto, a resposta de uma requisição envia dados maiores, caso seja utilizado o protocolo SOAP. 

Abaixo está um exemplo de uma requisição GET enviada através do protocolo SOAP:

```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <listarClientes xmlns="http://brejaonline.com.br/administracao/1.0/service">
    </soap:Body>
</soap:Envelope>
```
A resposta enviada pelo servidor seria:
```
<soap:Envelope xmlns:domain="http://brejaonline.com.br/administracao/1.0/domain" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <listarClientesResponse xmlns="http://brejaonline.com.br/administracao/1.0/">
      <domain:clientes>
        <domain:cliente domain:id="1">
          <domain:nome>Alexandre</domain:nome>
          <domain:dataNascimento>2012-12-01</domain:dataNascimento>
        </domain:cliente>
        <domain:cliente domain:id="2">
          <domain:nome>Paulo</domain:nome>
          <domain:dataNascimento>2012-11-01</domain:dataNascimento>
        </domain:cliente>
      </domain:clientes>
    </listarClientesResponse>
  </soap:Body>
</soap:Envelope>
```

Nota-se que a comunicação entre cliente e servidor é feita via arquivo XML, fazendo com que o código seja bastante complexo e consideravelmente maior. Portanto, esse protocolo não é recomendado para dispositivos móveis. 


## Os principios básicos de REST

>Protocolo de comunicação entre cliente e servidor que utiliza JSON como fonte de transferência de dados.

REST é um estilo de desenvolvimento de *web services*, no qual baseia-se nas boas práticas de uso de HTTP.A base para o protocolo REST são os *recursos*. Esses recursos são os dados que estão disponíveis no servidor, podendo ser uma página da web, um registro no banco de dados, um arquivo, entre outros. Esses recursos são representados por **URIs**. 

**OBS**: No caso de recursos web utilizamos **URL**, que é um tipo específico de **URI**, para representar o recurso. 

🕸️[A diferença entre URI e URL]()

### Como a URL é dividida

Vamos tomar como exemplo a URL `http://localhost:8080/cervejaria/clientes`:
- **http://**- Indica o protocolo que está sendo utilizado (no caso, HTTP).
- **localhost:8080**- Indica o servidor de rede e a porta que estão sendo utilizados. A porta padrão no protocolo HTTP é 8080.
- **cervejaria**- Indica o contexto da aplicação, ou seja, a base para a localização dos recursos.
- **clientes**- É o endereço, de fato, do recurso. Nesse caso, a listagem de clientes. 

#### Protocolo

Apesar do protocolo HTTP ser o mais utilizado em arquiteturas REST, ele não é o único. O motivo pelo qual o protocolo HTTP é tão utilizado em conjunto com REST é que ambos foram criados pela mesma pessoa, por esse motivo REST implementa métodos HTTP na sua arquitetura. Além disso, a existência de HTTPS não configura em um outro protocolo sendo utilizado. Na verdade, a diferença entre o protocolo HTTPS e o protocolo HTTP é que há uma camada de proteção a mais do primeiro em relação ao segundo.

#### URL

A URL escolhida deve ser única por recurso. Por exemplo, ao realizarmos uma consulta em `http://localhost:8080/cervejaria/clientes`, seriam retornado os dados da seguinte maneira:

```
<clientes>
  <cliente id="1">
    <nome>Alexandre</nome>
    <dataNascimento>2012-12-01</dataNascimento>
  </cliente>
  <cliente id="2">
    <nome>Paulo</nome>
    <dataNascimento>2012-11-01</dataNascimento>
  </cliente>
</clientes>
```

Se desejamos buscar um cliente em específico precisamos utilizar uma outra URL, sendo ela `http://localhost:8080/cervejaria/clientes/1`, com o retorno sendo:

```
<cliente id="1">
    <nome>Alexandre</nome>
    <dataNascimento>2012-12-01</dataNascimento>
</cliente>
```

### Resumindo

Vimos como os protocolos SOAP e REST são utilizados para web services. Vimos também as vantagens de utilizar o protocolo REST em cima de SOAP, bem como uma breve explicação sobre como REST é estruturado. 


