Obs: Esse método é uma melhoria do que está no arquivo Método para input de arquivos

1 - **Visualização dos Arquivos Selecionados**
Você exibe:
- **Miniatura (imagem)** se o arquivo for uma imagem (`.jpg`, `.png`, etc).
- **Nome** de todos os arquivos, inclusive não-imagens (como `.zip`, `.p7s`).
### Como?
Usamos `URL.createObjectURL(file)` para gerar um link temporário que permite mostrar a imagem selecionada antes mesmo do upload.
	`if (file.type.startsWith('image/')) {`
	  `item.urlImagem = URL.createObjectURL(file);`
	`}`

2 - **Estrutura para armazenar os arquivos**
	Substituímos a variável `nomesArquivos: string` por um array de objetos com nome e URL de imagem (opcional):
		`arquivosSelecionados: { nome: string, urlImagem?: string }[] = [];`
			Assim conseguimos mostrar tanto texto quanto imagens no HTML.

3 - **Arrastar e Soltar Arquivos (Drag & Drop)**
	Agora o usuário pode:
		- **Arrastar** arquivos até a área de upload.
		- **Soltar** e os arquivos serão processados como se fossem selecionados.
	 Como funciona:
 a) `@HostListener('dragover')`:
	Captura o momento que o mouse com arquivo entra na área de upload e evita que o navegador abra o arquivo.
	`@HostListener('dragover', ['$event'])`
		`aoArrastarSobre(event: DragEvent): void {`
		  `event.preventDefault();`
		  `this.arrastandoArquivo = true;`
		`}`
b) `@HostListener('dragleave')`:
	Reseta o visual se o usuário sair da área sem soltar.
	`@HostListener('dragleave', ['$event'])`
		`aoSairDaArea(event: DragEvent): void {`
		  `this.arrastandoArquivo = false;`
		`}`
c) `drop`:
Quando o usuário **solta** os arquivos, tratamos o evento igual ao `input` de arquivos:
	`aoSoltarArquivo(event: DragEvent): void {`
		`event.preventDefault();`
		`this.arrastandoArquivo = false;`
		  `if (event.dataTransfer?.files) {`
		    `this.processarArquivos(event.dataTransfer.files);`
		  `}`
		`}`

4 - **Estilo visual quando o arquivo está sendo arrastado**
	Quando detectamos que há um arquivo sendo arrastado, adicionamos a classe CSS `dragover`, que muda o fundo e borda para indicar interatividade:
		`[class.dragover]="arrastandoArquivo"`
	CSS aplicado:
		`.upload.dragover {`
		  `background-color: #e0f7fa;`
		  `border-color: #00acc1;`
		`}`

5 - **HTML dinâmico para mostrar os arquivos**
	`<div class="arquivo-preview" *ngFor="let arquivo of arquivosSelecionados">`
		  `<img *ngIf="arquivo.urlImagem" [src]="arquivo.urlImagem" alt="Preview" class="preview-imagem">`
		  `<span>{{ arquivo.nome }}</span>`
	`</div>`
		Isso garante que para **cada arquivo**:
			- Se for imagem: mostre a miniatura.
			- Sempre mostre o nome.

6 - **Input de arquivos escondido**
	O campo `<input type="file">` continua existindo, mas está escondido e é disparado manualmente com `click()` quando o usuário clica na área de upload:
		abrirSeletorArquivo(): void {
		  this.inputArquivoRef.nativeElement.click();
		}

![[Captura de tela de 2025-07-31 16-02-20.png]]


![[Captura de tela de 2025-07-31 16-03-21.png]]

Adicionando botão para remover arquivo
	`removerArquivo(index: number): void {`
		  `this.arquivosSelecionados.splice(index, 1);`
		`}`

`<div class="arquivo-preview" *ngFor="let arquivo of arquivosSelecionados; let i = index">`
	  `<img *ngIf="arquivo.urlImagem" [src]="arquivo.urlImagem" alt="Preview" class="preview-imagem">`
	  `<span>{{ arquivo.nome }}</span>`
	  `<button class="btn-remover" (click)="removerArquivo(i)" title="Remover arquivo">✖</button>`
`</div>`
