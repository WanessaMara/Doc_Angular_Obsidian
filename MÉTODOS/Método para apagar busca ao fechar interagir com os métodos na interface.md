`alterarModulo(index: number) {`
	`this.moduloSelecionado = this.moduloSelecionado === index ? null : index;`
	`if (this.moduloSelecionado !== index){`
		`this.registroSelecionado[index] = null;`
		`this.campoSelecionado[index] = {};`
		`this.erroSelecionado[index] = {};`
	`}`
	`this.busca = '';`
`}`

`alterarRegistro(moduloIndex: number, registroIndex: number) {`
	`this.registroSelecionado[moduloIndex]`
	`= this.registroSelecionado[moduloIndex] === registroIndex ? null : registroIndex;`
	`if (this.registroSelecionado[moduloIndex] !== registroIndex) {`
		`this.campoSelecionado[moduloIndex] = {};`
		`this.erroSelecionado[moduloIndex] = {};`
		`}`
	`this.busca = '';`
`}`

`alterarCampo(moduloIndex: number, registroIndex: number, campoIndex: number) {`
	`this.iniciarObjeto(this.campoSelecionado, moduloIndex);`
	`this.campoSelecionado[moduloIndex][registroIndex] =`
	`this.campoSelecionado[moduloIndex][registroIndex] === campoIndex ? null : campoIndex;`
	`this.iniciarObjeto(this.erroSelecionado, moduloIndex, registroIndex);`
	`if (this.campoSelecionado[moduloIndex][registroIndex] !== campoIndex) {`
		`this.fecharObjeto(this.erroSelecionado, moduloIndex, registroIndex, campoIndex);`
	`}`
	`// this.busca = '';`
	`}`

`alterarErro(moduloIndex: number, registroIndex: number, campoIndex: number, erroIndex: number) {`
	`this.iniciarObjeto(this.erroSelecionado, moduloIndex, registroIndex);`
	`this.erroSelecionado[moduloIndex][registroIndex][campoIndex] =`
	`this.erroSelecionado[moduloIndex][registroIndex][campoIndex] === erroIndex ? null : erroIndex;`
	`// this.busca = '';`
	`}`