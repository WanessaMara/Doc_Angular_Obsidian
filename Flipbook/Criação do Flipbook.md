-  Seguindo a noção de ser um componente filho. 
	- Exemplo: Tenho um componente FAQ onde o seu filho é o Flipbook

**1 - Importação**
	`"scripts": [`
		`"node_modules/jquery/dist/jquery.min.js",`
		`"src/assets/js/turn.min.js"`
		`]`
		- Dowload da lib `jquery` pelo npm 
		- Dowload via github da `turn`, pois é uma lib antiga 

**2 - Criação do componente Flipbook**
	![[Captura de tela de 2025-10-06 14-42-55.png]]

**3 - Criação do HTML**
	![[Captura de tela de 2025-10-06 14-43-53.png]]

**4 - Criação do CSS**
	![[Captura de tela de 2025-10-06 14-44-22 1.png]]

**5 - Criação do Modal no componente pai**
	- Seguindo dois exemplos:
		- Componente padrão para o modal
			![[Captura de tela de 2025-10-06 14-46-53.png]]
		- Componente ao qual eu estou trabalhando, onde já tenho uma página estruturada e a imagem exposta do `flipbook`
			![[Captura de tela de 2025-10-06 14-48-05.png]]

**6 - Criação do método no componente pai**
	![[Captura de tela de 2025-10-06 14-48-58.png]]

**7 - Criação do CSS para o componente pai**
	![[Captura de tela de 2025-10-06 14-52-17.png]]
	![[Captura de tela de 2025-10-06 14-52-27.png]]