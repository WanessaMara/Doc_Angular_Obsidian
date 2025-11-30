- Criação de um service para retorno de determinados parâmetros para um get.
- Usando Authorize no Swagger
	- para funcionar o retorno, teria que obter um token especifico do user para ai conseguir obter o retorno sem Status Code 401 (não autorizado).
- Importante: Isso já um sistema legado!!

- Foi criada um atributo da classe(esse atributo é uma variável de instância), com modificador de acesso private para receber a url com o environment, vindo da url da área de desenvolvimento. 
- Dentro do Get, foi Observable para retornar os dados que está sendo recebido da interface, e quando a requisição `this.http.get(...)` faz chamada HTTP e já leva o objeto headers
- Após, foi criada uma interpolação de string
	- onde se passa a variável + a rota do swagger
	- dps, se passa a  variável local no topo do código,
	- cria no topo uma Authorization para efetuar outra interpolação de string, recebendo um localStorage e um getItem passando um token.

![[Captura de tela de 2025-08-22 16-35-08.png]]