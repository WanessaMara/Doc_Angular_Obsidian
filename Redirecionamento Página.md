Criação de rota para o nav e para app-routing
Criação do componente padrão, mas ao clicar na nav para determinada "aba", é redirecionado para uma página externa 

`export class AjudaManualComponent implements OnInit {`

`constructor(private router: Router) { }`

`ngOnInit(): void {`
`window.open('https://abrasf.org.br/arquivos/publico/DES-IF/Modelo_Conceitual/Modelo_Conceitual_Versao_3_1.pdf', '_blank');`

`this.router.navigate(['/']); }`
`}`

Criado um ngOnInit onde o retorno é void(vazio), tendo um window.open para abrir uma página externa com o _blank, para a página não fica vazia do componente, tem o 'this.router.navigate(['/']);', para redirecionar para a página padrão/home
Precisa criar o constructor para importar a biblioteca de Router do angular

![[Captura de tela de 2025-07-30 14-40-16.png]]

Alternativa para dowload de arquivo:
`<div *ngFor="let planilha of planilhas">`
	`<a [href]="planilha.url" target="_blank" rel="noopener">`
	`<i>Planilha</i>`
	`</a>`
`</div>`

![[Captura de tela de 2025-07-30 14-37-34.png]]

Cria o service dentro do componente 
`import { Injectable } from "@angular/core";`

  `@Injectable({`
`providedIn: 'root'` `})`

`export class AjudaParametrosService {`

`getParametros() {`
`return [`
`{ url: 'assets/Relatorio_20250718014224.xlsx'} ]`
`}`
`}`
	Add o arquivo desejado dentro da pasta assets.

![[Captura de tela de 2025-07-30 14-39-39.png]]

Cria o ts, com a iteração do array do objeto sendo vazio e faz o cronstructor e fora do ts, a interface, para receber a url como string (Interface com a variavel 'url?' - é para caso a variavel seja opcional 'null' ou 'undefined')  

`export class AjudaParametrosComponent {`

`planilhas: Planilha[] = [];`

`constructor(private ajudaParametrosService: AjudaParametrosService) {`

`this.planilhas = this.ajudaParametrosService.getParametros();`
	`}`
`}`

`interface Planilha {`
`url?: string;`
`}`

![[Captura de tela de 2025-07-30 14-39-21.png]]