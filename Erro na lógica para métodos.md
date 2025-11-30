`if (this.filtroModuloSelecionado === null) {`
  `this.semErro = 'Selecione o módulo.';`
  `return;`
`} else if (this.filtroRegistroSelecionado === null) {`
  `this.semErro = 'Selecione o registro.';`
  `return;`
`} else if (this.filtroModuloSelecionado === null || this.filtroRegistroSelecionado === null) {`
  `this.semErro = 'Selecione o módulo e o registro para buscar.';`
  `return;`
`}`

Por que essa lógica não funciona?
	O terceiro else if nunca será executado

1 - Se `this.filtroModuloSelecionado === null` for verdadeiro, ele **entra no primeiro `if`** e faz `return`.
    
2 - Se não for, mas `this.filtroRegistroSelecionado === null` for verdadeiro, ele **entra no segundo `else if`** e faz `return`.
    
3 - **O terceiro `else if` nunca será atingido**, porque:
    - Se qualquer uma das duas condições (`modulo` ou `registro` ser `null`) for verdadeira, **já caiu em um dos `if` anteriores e saiu da função** com `return`.

`if (this.filtroModuloSelecionado === null && this.filtroRegistroSelecionado === null) {`
  `this.semErro = 'Selecione o módulo e o registro para buscar.';`
  `return;`
`}`

`if (this.filtroModuloSelecionado === null) {`
  `this.semErro = 'Selecione o módulo.';`
  `return;`
`}`

`if (this.filtroRegistroSelecionado === null) {`
  `this.semErro = 'Selecione o registro.';`
  `return;`
`}`
