Criar paginação para a partir de determinado erros, paginar
	- no caso seria paginar com 10 erros do arquivo txt

Estrutura dos Componentes pai e filho:
- **ProcessamentoComponent (pai)**
    - controla o upload do TXT
    - chama o backend (`preValidacao`)
    - guarda a lista de erros (`validacao: Validacao[]`)
    - passa os erros para o filho
        
- **PrimeiraLinhaComponent (filho A)**
    - só mostra os dados da linha 0000 (arquivo, CNPJ, etc.)
    - **não precisa de paginação**
        
- **ErrosComponent (filho B, que você ainda pode criar)**
    - recebe a lista `validacao: Validacao[]`
    - faz a paginação dos erros (10 por página)
    - renderiza a tabela/lista
O ideal é colocar a paginação dentro do componente erros, no caso seria validação, pois é ela que está apresentando os determinados erros constados no arquivo txt, que vem do drag drop

**Passo a Passo**
	1 - Criar o componente de exibição de erros ou localizar caso já exista no sistema (ex: ValidacaoComponent)
		- Esse componente será responsável apenas **por receber a lista de erros e mostrar com paginação**
	2 - Receber os erros como @Input() (provavelmente seja um componente filho)
		- No "validacao.component.ts":
			- `@Input() validacao: Validacao[];`
				- Permite que o componente pai (ex: ProcessamentoComponent) passe os erros recebidos do backend para o filho (levando um cenário de drag drop)
	3 - Definir variáveis de paginação
		- No mesmo componente:
			`- errosPorPagina = 5;   // quantos erros por página`
			`- paginaAtual = 1;      // página inicial`
	4 - Criar os getters para lógica de paginação 
		![[Captura de tela de 2025-09-03 16-09-44.png]]
	5 - Alterar HTML com "*ngfor*" para usar os itens paginados
		- Caso exista um ngfor no html para determinada validação, precisa mudar, caso não precisa ser criado
		- No validacao.component.html, NÃO usar validacao direto, mas sim errosPaginados
		- ![[Captura de tela de 2025-09-03 16-19-19.png]]
	6 - Exibir texto de status da página
		- Mostra qual faixa de erros está sendo exibida e o total de erros: ![[Captura de tela de 2025-09-03 16-20-36.png]]
			- exemplo: Exibindo 1 até 10 de N erros
	7 - Criar os botões de paginação
		- Botões Anterior | [números de páginas] | Próximo 
		![[Captura de tela de 2025-09-03 16-25-38.png]]


**Explicando a parte lógica do código**
	1 - Definir o tamanho da pagina (quantos itens pode mostrar de cada vez)
		`erroPorPagina = 5;`
			"Minha tela só pode exibir 5 itens de cada vez" 
	2 - Saber em que página você está
		`paginaAtual = 1;`
			Isso indica a "página lógica" - não é uma tela nova, só um **corte diferente do mesmo array**
	3 - Calcular o índice inicial do array
		`const inicio = (this.paginaAtual - 1) * this.erroPorPagina;`
			Exemplo: 
				Página 1 => (1-1) * 5 = 0 => começa o índice 0 do array
				Página 2 => (2-1) * 5 = 5 => começa o índice 5
				Página 3 => (3-1) * 5 = 10 => começa no índice 10
					O calculo **sempre pula de 5 em 5** ( ou do valor definido em `errosPorPagina`)
	4 - Calcular o índice final
		`const fim = inicio + this.errosPorPagina;`
			Exemplo:
				Página 1 -> início 0 -> fim 0 + 5 = 5
				Página 2 -> início 5 -> fim 10
				Página 3 -> início 10 -> fim 15
	5 - Fatiar o array original
		`this.validacao.slice(inicio, fim);`
			-> `slice(inicio, fim)` pega só a parte do array que você quer mostrar. Assim, mesmo que o array tenha 1000 itens, só é mostrado os itens entre `[inicio ... fim]`
	6 - Calcular o número total de páginas
		`totalDePaginas = Math.ceil(this.validacao.length / this.errosPorPagina);`
			Exemplo:
				42 erros, 5 por página -> `42 / 5 = 8.4` -> `ceil` arredonda para cima -> 9 páginas
				Isso evita ficar com "meia página"
	7 - Exibir o intervalo para o usuário
		`inicioExibicao = (paginaAtual - 1) * errosPorPagina + 1;`
		`fimExibicao = Math.min(paginaAtual * errosPorPagina, validacao.length);`
			-> Isso gera o texto:
				"Exibindo 6 até 10 de 42 erros"
			-> O `Math.min` é importante porque na última página pode sobrar menos itens do que `errosPorPagina`

## Como pensar nisso fora do código
O **raciocínio base** da paginação é:
1. **Quantos itens cabem em uma página?** (`errosPorPagina`)
2. **Qual página estou agora?** (`paginaAtual`)
3. **Onde começa e termina esse "recorte" no array?** (`inicio` e `fim`)
4. **Quantas páginas no total eu tenho?** (`totalDePaginas`)