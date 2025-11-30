Cria animação no css para interação ao fazer rolagem na página

`@keyframes scrollAnimation {`
`0% {`
`opacity: 0;`
`transform: translateY(-50px);`
`}`

`80% {`
`opacity: 1;`
`transform: translateY(5px); /* passa um pouco do destino */`
`}`

`100% {`
`transform: translateY(0);`
`}`
`}`

`.scroll-smooth {`
`animation: scrollAnimation 1s cubic-bezier(0.25, 0.1, 0.25, 1);`
`}`

`.scroll-hidden {`
`opacity: 0;`
`}`


Cria o ts para detectar quais conteúdos estão na tela para fazer animação especifica, e com a rolagem fazer animação para os conteúdos ocultos na tela

Usa a API IntersectionObserver - detecta quando os elementos aparecem e desaparecem na viewpoint 

### Como funciona?
- O **IntersectionObserver** observa os elementos com a classe `.scroll-hidden`.
- Quando um elemento entra na viewport (pelo menos 10% visível), ele:
    - Adiciona `.scroll-smooth` para animar.
    - Remove `.scroll-hidden` para ficar visível.
    - Para de observar esse elemento (não vai animar mais vezes).
### E para a animação inicial?
Como o IntersectionObserver já detecta instantaneamente se o elemento está na tela quando o componente inicia, ele vai animar os elementos que já estão visíveis assim que a página carrega, sem precisar de lógica extra.


`export class AjudaFluxoComponent implements OnInit, OnDestroy {`

`observer!: IntersectionObserver;`

`ngOnInit(): void {`
`this.observer = new IntersectionObserver((entries) => {`
`entries.forEach(entry => {`
`const elemento = entry.target as HTMLElement;`

`if (entry.isIntersecting) {`
`elemento.classList.add('scroll-smooth');`
`elemento.classList.remove('scroll-hidden');`
`this.observer.unobserve(elemento);`
`}`
`});`
`}, {`

`root: null,`
`rootMargin: '0px 0px -50px 0px',`
`threshold: 0.1`
`});`

  
`const elementos = document.querySelectorAll('.scroll-hidden');`
`elementos.forEach(el => this.observer.observe(el));`
`}`

`ngOnDestroy(): void {`
`if (this.observer) {`
`this.observer.disconnect();`
`}`
`}`
`}`

![[Captura de tela de 2025-07-30 13-39-55.png]]


