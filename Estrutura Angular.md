**Criação Projetos :** 
	**ng new 'nome da pasta/projeto**' - é criado a pasta da estrutura geral do projeto, com algumas pastas especificas (css, assets, app, tsconfig, package.json....)
	Por padrão da versão 14+, os projetos são standalone (sem o arquivo NgModule), pode ser add manualmente, ou caso queira criar **no standalone**
		**ng new 'nome da pasta/projeto --no-standalone'**

**Estrutura do Sistema :** 
	***node_modules*** - onde é instalado todos os pacotes do sistema
	***public*** - vai ter o **favicon.ico**, icone do site
	***src*** - pasta principal, localiza pasta app(routes, modules, config)
		index.html, styles.css, main.ts (arquivos geral do projeto)
	alguns arquivos soltos
		angular.json
		.gitidnore
		package.json
		README.md
		tsconfig.json
		...

**Estrutura de Componentes :**
	**ng generate component 'nome do componente'** - é gerado dentro da pasta app dos componentes determinado(s).
```
	App/Componentes/MeuComponente
		MeuComponente.html
		MeuComponente.css
		MeuComponente.spec.ts
		MeuComponente.ts
```

**HTML e CSS**
	estrutura básica do html, localizado em index.html
```
	<!DOCTYPE html>
	<html lang="pt-br">
	<head>
	    <meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial scale=1.0">
    <title>Portifolio - Wanessa Mara</title>
	<link rel="icon" href="assets/favicon.png" sizes="16x16"  type="image/png">
    <base href="/">
	</head>
	<body>
	    <app-root></app-root>
	</body>
	</html>
```
no outro html, no app-component.html / app.html se localiza o resto da estrutura, sem o body, mais ou menos assim... 
composta pelo header(cabeçalho), os app (html dos componentes) e o footer(rodapé)
```
<header>
        <h1>Wanessa Mara</h1>
        <nav>
            <ul>
                <li><a href="#sobre">Sobre</a></li>
                <li><a href="#projetos">Projetos</a></li>
                <li><a href="#contato">Contato</a></li>
            </ul>
        </nav>
	</header>
	  <app-sobre></app-sobre>
	  <app-projetos></app-projetos>
	  <app-contato></app-contato>
	<footer>
	  <p>&copy; 2025 Wanessa Mara</p>
	</footer>
```

estilização em css - localizado no styles.css (padrão) ou pode ser aplicada estilizações específicas para cada componente

**Estrutura de Rotas ou Routes :** 
	Criação de rotas para navegação do sistema 
		Localizada dentro de **app - app.routes.ts / app-routing.module.ts** 
```
	export const routes: Routes = [
		{ path: '', redirecTo: 'sobre', pathMacth: 'full' },
		{ path: '**', redirecTo: 'sobre', pathMath: 'full' },
		{ path: 'sobre', component: SobreComponent},
		.......
	];
```
existe um Autocard (não sei ao certo) que pode ser colocado junto da rota, ele só faz direcionamentos caso o usuário esteja logado.

pode haver uma pasta para **NAV**, caso ocorra o sistema de ter uma barra de navegação, menu, ao algo do tipo. neste caso, após criação da rota, precisa alterar o link da nav, para ser redirecionado para a página específica..