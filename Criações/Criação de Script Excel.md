- Criação de um service para receber uma imagem convertida em Base64 (transferindo de binário para string) para o script do Excel conseguir receber a imagem no arquivo
	- Após gerar o componente, add no module do componente pai,

![](imagens/Captura de tela de 2025-08-25 16-51-46.png)

![[Captura de tela de 2025-08-25 16-51-46.png]]

- Todo o componente foi criado com formatação especifica para linhas e colunas,  recebendo os Pipes para o array dos dados apresentados da página.
- Formatação com as cores, e gerando o arquivo pela biblioteca do ExcelJs e File-Saver

![[Captura de tela de 2025-08-25 16-52-14.png]]

![[Captura de tela de 2025-08-25 16-52-28.png]]

![[Captura de tela de 2025-08-25 16-52-36.png]]

Segue a estrutura do html para exportar o excel no botão e seu css
![[Captura de tela de 2025-09-04 13-36-20.png]]

![[Captura de tela de 2025-09-04 13-36-44.png]]