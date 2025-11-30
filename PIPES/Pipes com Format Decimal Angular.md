Receber dados decimais no banco, e formatar no front com Pipes
	- Criar formatação numérica:
		- Exemplo do Pipe usando `Intl.NumberFormat`: ![[Captura de tela de 2025-08-19 14-19-59.png]]
		- no HTML: ![[Captura de tela de 2025-08-19 14-21-03.png]]
	- ✅ Resultado esperado:
		- Se o valor for `0` → mostra `-`
		- Se o valor for `1` → mostra `1,00`
		- Se o valor for `10.5` → mostra `10,50`
		- Se o valor for `null` → mostra `-`