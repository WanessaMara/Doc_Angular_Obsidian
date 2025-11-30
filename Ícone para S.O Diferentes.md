Ajustes no HTML, pois ícone pode mudar diante do sistema operacional.
	Antes: 
		`{{ campoSelecionado[mi][ri] === ci ? '▼' : '▶' }} {{ campo.nome }}`
	Depois:
		`<i [class]="moduloSelecionado === mi ? 'bi bi-arrow-down' : 'bi bi-arrow-right'"></i> {{ modulo.nome }}`
		No Angular, não deixa na class a tag i ter interpolação {{}}
	Aplicando tag i para ajustar ícone no bootstrap