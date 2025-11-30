Criação do html básico com 'p' e conteudo da div 

Interpolação de String - {{ exemplo.nome }}

`<div class="container-principal">

	<div *ngFor="let legislacao of legislacoes">
		<div class="conteudo">
		<b>{{ legislacao.titulo }}</b>
		<p>{{ legislacao.descricao }}</p>
		
		<div>
			<a [href]="legislacao.url" target="_blank" rel="noopener" class="btn-dowload">Dowload</a>
		</div>
	</div>
	</div>
	</div>`

![[Captura de tela de 2025-07-30 14-41-38.png]]

Criação simplificada do ts para retornar o url diretamente no ts, sem a necessidade de criar um service para ele
	`export class AjudaLegislacaoComponent {

	legislacoes: Legislacao[] = [
	{
	titulo: 'INSTRUÇÃO NORMATIVA Nº 05/2020 DE 08 DE MAIO DE 2020',
	descricao: 'Prorroga o prazo para a entrega da Declaração...',
	url: 'https://www.sefin.fortaleza.ce.gov.br/'
	},
	
	}
	
	interface Legislacao {
		titulo: string;
		descricao: string;
		url: string;
	}`

![[Captura de tela de 2025-07-30 14-42-18.png]]

Após criar os dois códigos, precisa iterar o array no html.
	Já que vai ser criado uma div com determinado conteúdo, a iteração pode ser feita dentro dele, ao lado da 'class' usando *NgFor='declara exemplo de exemplos '*
	
Detalhes *NgFor='declara exemplo de exemplos':
	`*ngFor=''* - Diretiva estrutural do Angular que permite Iterações (forma abreviada <ng-template>)`
		
	`let: Indica que estamos declarando uma variável local para cada item do loop` 
	`Declara uma variável local chamada 'exemplos', será usada para referenciar cada item da coleção durante a iteração. Cada iteração, a variável terá o valor atual da sua coleção.`
		
	`of: Separa variáveis local do array que será iterado`

	exemplo: Nome da variável local que terá valor do item atual do array 'exemplos' em cada iteração

	 exemplos: Nome do Array (ou objeto iterável) que será percorrido pela diretiva.
	 
Exemplo PARA NÃO FAZER:
	`<div class="conteudo" *ngFor="let legislacao of legislacoes"></div>`
	em cada div dos conteúdos, não se pode colocar o '*ngFor="let legislacao of legislacoes"' repetidas vezes, pois ele ira multiplicar quantas vezes você colocar. 
	O ideal é colocar apenas uma UNICA VEZ, e assim sim, ele ira iterar o array