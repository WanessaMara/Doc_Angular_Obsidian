**Criação de componente para aba de ajuda.**
	ng g c Anexos
	alteração na nav para redirecionamento da página e na rota
	imports no NgModule do componente

Componente teria tais tabelas e uma animação para abrir opções e baixar determinado arquivo

**Criação do HTML**
`<h2 class="text-dark mb-4 mt-2 text-start">Anexos</h2>`

`<div *ngFor="let anexo of anexos; let ai = index; let last = last" class="mb-4 border p-2 w-50 mx-auto" [ngClass]="{'mb-5': last}" [@expandCollapse]>`

`<button class="cor-botao-ajuda w-100 text-start" (click)="alterarAnexos(ai)">`
`{{ anexosSelecionados === ai ? '▼' : '▶' }} {{ anexo.nome }}` `</button>`

`<div *ngIf="anexosSelecionados === ai" class="mt-2 mb-2" [@expandCollapse]>`
	`<a [href]="anexo.url" target="_blank" rel="noopener" class="btn btn primary">`
		`<i class="fas fa-download"></i> Baixar Anexo`
		`</a>`
	`</div>`
`</div>`

![[Captura de tela de 2025-07-30 13-43-23.png]]

**Criação do TypeScript**
	Propriedade criada (anexos: ) e recebendo um array de objetos do tipo Anexo[] = [](inicialmente está vazio [] 
	Abaixo ocorre um construtor com uma injeção de dependência, acontecem duas coisas:
		1- Injeção de Serviços
			Angular injeta automatico uma instancia de AjudaAnexosService assim que o componente é criado
			Existe um serviço com métodos para buscar dados do anexos(pode vir uma API, banco local ou até um array mockado)
		2- Popula o array anexo
			O método getAnexos() do service é chamado para buscar a lista de anexos e atribui o resultado para this.anexos
	Propriedade AnexosSelecionados
		`anexosSelecionados: number | null = null;`
		Essa propriedade guarda qual anexo da lista foi selecionado
			Tipo: ou um número (índice no array anexos), ou null se estiver selecionado
			Começa como null, ou seja, nenhum anexo está selecionado no ínicio 
	Método alterarAnexos()
		`alterarAnexos(index: number){ this.anexosSelecionados = this.anexosSelecionados === index ? null : index; }`
		O método é chamado quando quer selecionar/deselecionar um anexo.
		Se o índice recebido for igual ao que está selecionado (`this.anexosSelecionados === index`), significa que o mesmo item foi clicado novamente
			Então o objeto é desmarcado e atribuido a null, no caso ele é fechado
		Se o índice for diferente, ele atualiza this.anexosSelecionados como o novo índice
	Criação da Interface ANEXOS
		`interface Anexo {`
		  `nome: string;`
		  `url?: string; }`
		Define a estrutura do objeto Anexo
			Nome: obrigatorio (string)
			url: opcional (string)

`export class AjudaAnexosComponent {`

`anexos: Anexo[] = [];`

`constructor(private ajudaAnexosService: AjudaAnexosService){`
`this.anexos = this.ajudaAnexosService.getAnexos(); }`
  
`anexosSelecionados: number | null = null;`

`alterarAnexos(index: number){ this.anexosSelecionados = this.anexosSelecionados === index ? null : index;} }`

`interface Anexo {`
`nome: string;`
`url?: string;` `}`

![[Captura de tela de 2025-07-30 13-44-12.png]]

**Criação do Service**
	`import { Injectable } from '@angular/core';`
	
`@Injectable({`
`providedIn: 'root'` `})`

`export class AjudaAnexosService {`

`getAnexos(){` return [`

`{ nome: 'Tabela de Eventos Contábeis em Contas de Resultado', url: 'https://pvnd.sefin.fortaleza.ce.gov.br/downloads/anexos/Anexo_Eventos_Versao_3.1.pdf' },`

`{ nome: 'Tabela de Títulos', url: 'https://pvnd.sefin.fortaleza.ce.gov.br/downloads/anexos/Anexo_Tabela_de_Titulos_Versao_3.1.pdf' },`

`];`
`}` `}`

Após a criação do construtor no Ts, é criado esse array no Service pelo getAnexos, onde tem um retorno do array, cada array tem seu nome e sua url em especifico e cada url tem '_blank' no html, ao clicar para baixar o anexo, é redirecionado para determinada pagina 

![[Captura de tela de 2025-07-30 13-45-08.png]]