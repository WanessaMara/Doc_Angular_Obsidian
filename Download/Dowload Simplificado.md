Click para dowload aplicando em uma img com icone
	Criação do html
		`<div class="exportar-pdf" title="Exportar para PDF" >`
		`<i class="bi bi-file-earmark-pdf" aria-hidden="true" (click)="exportarPdf()"></i>`
		`</div>` 
		
![[Captura de tela de 2025-07-30 13-46-51.png]]

Criação do TypeScript
		Cria interface para receber o objeto em array
		`interface Faq { arquivo: string; }`
		Array para receber objeto no array - Necessariamente não é necessário esse array e nem a interface, pois está passando o caminho no próprio método.
			`faq: Faq[] = [`
			  `{ arquivo: 'assets/files/FAQ DES-IF Fortaleza 30-05-2019.pdf' } ];`
		Criação do Método para efetuar download do arquivo
			`exportarPdf(): void {`
			`const link = document.createElement('a');`
			`link.href = 'assets/files/FAQ DES-IF Fortaleza 30-05-2019.pdf';`
			`link.download = 'FAQ DES-IF Fortaleza 30-05-2019.pdf';`
			`link.target = '_blank';`
			`document.body.appendChild(link);`
			`link.click();`
			`document.body.removeChild(link); }`
			Nessa criação o arquivo é apontado direto sem depender do índice do array, por isso o html (click)="exportarPdf()" - não recebe nenhum parâmetro no método
				Caso seja necessário o índice do array, no caso tendo APENAS um único arquivo, (click)="exportarPdf(0)", caso tenha MAIS de um arquivo, usaríamos NgFor=''

![[Captura de tela de 2025-07-30 13-48-01.png]]

## **Outro jeito de fazer o método para baixar arquivo**
	`exportarPdf(index: number): void {`
	  `const link = document.createElement('a');
	  `link.href = this.faq[index].arquivo;
	  `link.download = this.faq[index].arquivo.split('/').pop() || 'arquivo.pdf';` 
	  `link.target = '_blank';
	  `document.body.appendChild(link);
	  `link.click(); 
	  `document.body.removeChild(link);
	  `}`

### Linha por linha explicada:

| Linha                                                     | O que faz                                         | Por quê?                                             |
| --------------------------------------------------------- | ------------------------------------------------- | ---------------------------------------------------- |
| `const link = document.createElement('a');`               | Cria um elemento `<a>`                            | Esse será o link para download                       |
| `link.href = this.faq[index].arquivo;`                    | Define o caminho do arquivo PDF                   | O navegador precisa saber o que baixar               |
| `link.download = this.faq[index].arquivo.split('/').pop() |                                                   | 'arquivo.pdf';`                                      |
| `link.target = '_blank';`                                 | Abre o link em uma nova aba, se não baixar direto | Uma medida de segurança padrão                       |
| `document.body.appendChild(link);`                        | Adiciona o link temporariamente no HTML           | O `click()` só funciona se o elemento estiver no DOM |
| `link.click();`                                           | Simula um clique no link                          | Inicia o download como se fosse um clique de verdade |
| `document.body.removeChild(link);`                        | Remove o link da página                           | Limpa o DOM após o clique                            |

Criação de Animação Spinner ao clicar no icone
	`carregando: boolean = false;`
	
		`exportarPdf(): void {`
		
		`this.carregando = true;`

		Detalhes do código para add click ao arquivo
		
		`setTimeout(() => {`
		`document.body.appendChild(link);`
		`link.click();`
		`document.body.removeChild(link);`
		`this.carregando = false;`
		`}, 800);`
		`}`
	`}`
Recebe a variável sendo true pro primeiro click, e false para finalizar o tempo de espera do download

No HTML ao lado do (click), recebe um NgIf para carregamento do spinner 
	`(click)="exportarPdf()" *ngIf="!carregando"` - inicialmente recebe ele em false
	dentro da mesma div, add outra div especifica para o spinner
		`<div class="spinner" *ngIf="carregando">`
		`<i class="bi bi-arrow-repeat spin"></i>`
		`</div>`
	CSS para animação
		`.spinner {`
		`display: flex;`
		`font-size: 18px;`
		`align-items: center;`
		`justify-content: center; }`
		
		.spin {
		animation: spin 1s linear infinite; }
		
		@keyframes spin {
		0% { transform: rotate(0deg); }
		100% { transform: rotate(360deg); } }


Alternativa para Real-Time do Spinner
	Importações
		`import { Component } from '@angular/core';` - Permite definir o componente Angular
		`import { HttpClient } from '@angular/common/http';` - Permite requisições HTTP, como download de arquivos.
	Configurações de Componentes
		`@Component({`
		  `selector: 'app-download',` - Nome tag do componente HTML
		  `templateUrl: './download.component.html',` - Aponta para html do componente
		  `styleUrls: ['./download.component.css']` - Aponta para CSS
			`})`
	Variável
		`export class DownloadComponent {`
		  `carregando = false;` - Usada para controlar a exibição do spinner. Falso por padrão, ou seja, spinner não aparece até iniciar download.
	Construtor com injeção de dependência
		  `constructor(private http: HttpClient) {}` - HttpClient é injetado no componente para ser usado no método de download.
	Início do método
		  `baixarArquivo() {`
		    `this.carregando = true;` - Quando botão é clicado, o método é chamado. O carregando é colocado como true, fazendo spinner aparecer
	Url/Arquivo que será baixado
		`const url = 'https://exemplo.com/arquivo.pdf';` - Pode trocar para um caminho no back ou até na pasta assets para um arquivo real.
	Requisição HTTP para baixar arquivo
		`this.http.get(url, { responseType: 'blob', reportProgress: true, observe: 'events' }).subscribe({` 
			ResponseType: blob - Indica que queremos baixar um arquivo binário (como PDF)
			ReportProgress: true - Habilita o acompanhamento do progresso
			Observe: 'events' - Permite observar eventos do progresso (não só a resposta final)
	Evento Type
		 `next: (evento) => {`
        `if (evento.type === 4) {` - Evento === 4 significa 'resposta final' (HttpEventType.Response)
	        Arquivo completamente recebido
	Criação do arquivo
		`const blob = new Blob([evento.body as BlobPart], { type: 'application/pdf' });`
        `const urlBlob = window.URL.createObjectURL(blob);` 
	        Blob - representa dados binários do PDF
	        CreateObjectUrl - gera url temporaria para que o navegador possa "ver" o arquivo
	Criação de clique
		`const a = document.createElement('a');`
        `a.href = urlBlob;`
        `a.download = 'arquivo.pdf';`
        `a.click();`
	        Criação e clique automático em um link para baixar
		        Cria um `<a>` escondido e simula um clique para iniciar o download do arquivo.
	Limpeza e finalização
		 `window.URL.revokeObjectURL(urlBlob);`
         `this.carregando = false;`
        `}`
	        RevokeObjectUrl - libera memória da url temporária 
	        Carregando = false - oculta o spinner
	Tratamento de Erro
		      `},`
      `error: () => {`
        `console.error('Erro ao baixar o arquivo');`
        `this.carregando = false;`
      `}`
	      Se algo der errado no download, o erro é exibido no console e o spinner é removido.

`export class AjudaFaqComponent {`
`carregando: boolean = false;`

`constructor(private http: HttpClient){}`

`exportarPdf(): void {`

`this.carregando = true;`

`const arquivo = 'assets/files/faq-desif-fortaleza.pdf';`

`this.http.get(arquivo, { responseType: 'blob', reportProgress: true, observe: 'events'}).subscribe({`

`next: (evento) => {`

`if (evento.type === 4) {`
`const blob = new Blob([evento.body as BlobPart], { type: 'application/pdf'});`
`const arquivoBlob = window.URL.createObjectURL(blob);`

`const link = document.createElement('a');`
`link.href = arquivoBlob;`
`link.download = 'FAQ DES-IF Fortaleza 30-05-2019.pdf';`
`link.click();`

`window.URL.revokeObjectURL(arquivoBlob);`
`this.carregando = false;`
	`}`
`},`
`error: () => {}`
		`})`
	`}`
`}`


Alterando o evento do ícone para dowload
	aplica um carregamento de cache do arquivo, antes de ser clicado no ícone. 
		Evita delay do dowload

![[Captura de tela de 2025-07-31 15-12-08.png]]


![[Captura de tela de 2025-07-31 15-12-49.png]]