1 - Usando Pipes no Angular
	- Para manter o banco retornando apenas os números (1,2,3...) e transformando isso direto no front, pode criar pipes
	- Dentro da pasta Pipes no projeto
		- `ng g p 'nome do pipe'`
		- *DETALHE*: Precisa importar no `shered.module` caso não seja standalone
		- Exemplo de um Pipe criado: ![[Captura de tela de 2025-08-19 14-12-20.png]]
		- E fazendo a interpolação da string no HTML
			- `<td>{{ item.consolidacao | consolidacao }}</td>`
		- Caso venha valores do banco como string, mas no meu caso funcionou assim, criando uma `cont num = Number(value)`:
			- Assim ele aceita tanto `string` quanto `number` ![[Captura de tela de 2025-08-19 14-15-41.png]]