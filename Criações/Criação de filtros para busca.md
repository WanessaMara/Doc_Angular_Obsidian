HTML
	`<div class="filtros">`
		`<select class="form-select me-2" [(ngModel)]="filtroModuloSelecionado">`
			`<option [ngValue]="null" disabled>Selecione um módulo</option>`
			`<option [ngValue]="null">Todos os Módulos</option>`
			`<option *ngFor="let modulo of modulos; let i = index" [ngValue]="i">`
			`{{ modulo.nome }}`
			`</option>`
		`</select>`
		`<select class="form-select" [(ngModel)]="filtroRegistroSelecionado" [disabled]="filtroModuloSelecionado === null">`
		    `<option [ngValue]="null">Todos os registros</option>`
		    `<option *ngFor="let registro of modulos[filtroModuloSelecionado || 0]?.registros; let j = index" [ngValue]="j">`
		      `{{ registro.nome }}`
		    `</option>`
		  `</select>`
	`</div>`

- `[(ngModel)]="filtroModuloSelecionado"` controla o valor do select.
- `ngValue="null"` é a forma correta de passar valores especiais como `null`.
- A primeira `<option>` com `disabled` serve como “placeholder” e não pode ser selecionada de novo.
- A segunda `<option>` com `ngValue=null` permite buscar em **todos os módulos**, que é o comportamento que você deseja.

Desabilitar o método de busca para apenas funcionar com o uso do filtro
	pode desabilitar no input do html direto:
		`[disabled]="filtroModuloSelecionado === null || filtroRegistroSelecionado === null"`
	ou diretamente no método dentro do ts
		  `if (this.filtroModuloSelecionado === null || this.filtroRegistroSelecionado === null) {`
		    `this.semErro = 'Selecione o módulo e o registro antes de buscar.';`
		    `return;`
		  `}`