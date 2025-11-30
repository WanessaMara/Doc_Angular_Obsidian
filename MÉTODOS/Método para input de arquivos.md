Cabeçalho de Importações:
	`import { Component, ViewChild, ElementRef } from '@angular/core';`
		ViewChild - permite que acesse o 'elemento do template HTML' (como div ou input) diretamente no TS
		ElementRef - serve para manipular elementos DOM puros no Angular (tipo 'document.querySelector, mas via Angular)

Variável `nomesArquivos`
	`nomesArquivos: string = '';`
		Variável armazena os nomes dos arquivos selecionados pelo user, em formato de texto
		Ela é exibida no HTML usando interpolações: {{ nomesArquivos }}

Decorador `@ViewChild`
	`@ViewChild('inputArquivo') inputArquivoRef!: ElementRef<HTMLInputElement>;`
		Vai referenciar o elemento HTML que tem #inputArquivo
		O ! indica que você garante que essa referência 'não será' null depois que o template carregar
		ElementRef<HTMLInputElement>; - define que esse elemento é um <input type="file">
			Isso permite usar 
				`this.inputArquivoRef.nativeElement.click();`
			Ou seja, dispara um click programaticamente no campo do upload

Método abrirSeletorArquivo()
	abrirSeletorArquivo(): void {
		this.inputArquivoRef.nativeElement.click();
		}
	Simula o clique no campo de upload quando o usuário clina na 'div.upload'
				Boas práticas para utilizar melhor a área de upload e manter o input invisível no layout

Método aoSelecionarArquivos(event: Event)
	`aoSelecionarArquivos(event: Event): void {`
	  `const input = event.target as HTMLInputElement;`
		Método chamado quando o ' input type="file" ' detecta uma mudança ((change) no HTML)
		'event.target as HTMLInputElement' converte o target do evento para um input, com acesso à propriedades files.

Verificação dos arquivos
	`if (input.files && input.files.length > 0) {`
	  `const nomes = Array.from(input.files).map(f => f.name);`
	  `this.nomesArquivos = nomes.join(', ');`
	`}`
		Input.files é do tipo FileList, que precisa ser convertido para Array com 'Array.from(...)'
		Map(f => f.name) - pega o nome de cada arquivo
		Join(', ') - junta os nomes numa única string reparada por vírgula
Se nada foi selecionado:
	`else {`
	  `this.nomesArquivos = '';`
	`}`
	Limpa a variável caso o usuário cancele a seleção

Exemplo de Método aprimorado para acumular vários arquivos
	`import { Component, ElementRef, ViewChild } from '@angular/core';`
		`@Component({`
		  `selector: 'app-ajuda-upload-compactado',`
		  `templateUrl: './ajuda-upload-compactado.component.html',`
		  `styleUrl: './ajuda-upload-compactado.component.css'`
		`})`
		
		`export class AjudaUploadCompactadoComponent {`
			`arquivosSelecionados: File[] = [];`
			
		  `@ViewChild('inputArquivo') inputArquivoRef!: ElementRef<HTMLInputElement>;`
	
		  `abrirSeletorArquivo(): void {`
		    `this.inputArquivoRef.nativeElement.click();`
		  `}`
		  
		  `aoSelecionarArquivo(event: Event): void {`
		    `const input = event.target as HTMLInputElement;`
		    `if (input.files && input.files.length > 0) {`
		      `// Converte a FileList em array e adiciona os arquivos novos à lista atual`
		      `const novosArquivos = Array.from(input.files);`
		
		      `// Evita arquivos duplicados (por nome, por exemplo)`
		      `novosArquivos.forEach(novo => {`
		        `if (!this.arquivosSelecionados.find(a => a.name === novo.name && a.size === novo.size)) {`
		          `this.arquivosSelecionados.push(novo);`
		        `}`
		      `});`
	
		      `// Atualiza a string com os nomes`
		      `const nomes = this.arquivosSelecionados.map(f => f.name);`
		      `this.nomesArquivos = nomes.join(', ');`
		      
		      `// Limpa o input para permitir selecionar o mesmo arquivo novamente se quiser`
		      `input.value = '';`
		    `}`
		  `}`
			  `nomesArquivos: string = '';`
			`}`

![[Captura de tela de 2025-07-30 14-30-53.png]]


