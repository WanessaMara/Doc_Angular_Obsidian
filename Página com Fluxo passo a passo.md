HTML Iniciao para fluxo
	`<div class="timeline-container" id="timeline">`
		`<div class="timeline-item">`
		`<div class="timeline-icone-verde">`
		`<i class="bi bi-keyboard"></i>`
		`</div>`
			`<div class="timeline-conteudo scroll-escondido">`
			`<h4>Logon</h4>`
			`<p>A instituição faz logon via representante. O site PVN faz a atualização automaticamente das versões.</p>`
			`<span>1° Passo</span>`
			`</div>`
	`</div>`

![[Captura de tela de 2025-07-30 14-35-26.png]]

Css 
	`.timeline-container {`
		`position: relative;`
		`max-width : 70%;`
		`margin: 0 auto;`
		`padding: 20px 0 100px;`
		`overflow: hidden;`
		`display: block;`
		`}`

	.timeline-container::before {
		content: '';
		position: absolute;
		top: 0;
		bottom: 0;
		left: 50%;
		width: 4px;
		background: #ddd;
		transform: translateX(-50%);
		z-index: 1;
		}

	.timeline-item {
		display: flex;
		position: relative;
		margin: 40px 0;
		}

	.timeline-item:nth-child(odd) {
		flex-direction: row-reverse;
		}

	.timeline-icone-verde,
	.timeline-icone-azul,
	.timeline-icone-amarelo,
	.timeline-icone-cinza {
		background: #4CAF50;
		color: white;
		font-size: 20px;
		border-radius: 50%;
		width: 50px;
		height: 50px;
		display: flex;
		align-items: center;
		justify-content: center;
		position: absolute;
		top: 0;
		left: 50%;
		transform: translate(-50%, 0);
		z-index: 2;
		box-shadow: 0 0 5px rgba(0,0,0,0.3);
		}

	.timeline-icone-azul {
		background: #5196CC;
		}
		
	.timeline-icone-amarelo {
		background: #f0ca45;
		}

	.timeline-icone-cinza {
		background: #acb7c0;
		}

	.timeline-conteudo {
		background: #f0f0f0;
		padding: 15px 20px;
		border-radius: 10px;
		width: 45%;
		box-shadow: 0 2px 8px rgba(0,0,0,0.1);
		position: relative;
		z-index: 0;
		}

	.timeline-item:nth-child(odd) .timeline-conteudo {
		text-align: right;
		}

	.timeline-conteudo p {
		margin: 0;
		color: #555;
		text-align: justify;
		}

	span {
		display: block;
		text-align: right;
		width: 100%;
		}

	.timeline-conteudo h4 {
		margin-top: 0;
		text-align: justify;
		}

	@keyframes scrollAnimation {
		0% {
		opacity: 0;
		transform: translateY(-50px);
		}
		80% {
		opacity: 1;
		transform: translateY(5px);
		}
		100% {
		transform: translateY(0);
		}
	}

	.scroll-suave {
		animation: scrollAnimation 1s cubic-bezier(0.25, 0.1, 0.25, 1);
		}

	.scroll-escondido {
		opacity: 0;
		}


Invertendo os campos (odd para even)
	Inverte a direção dos container visualmente, antes estava direita para esquerda. agr está esquerda para direita
	`.timeline-item:nth-child(even) {`
		  `flex-direction: row-reverse;`
	`}`

	.timeline-item:nth-child(even) .timeline-conteudo {
		  text-align: right;
	}


TypeScript 
	`import { Component, OnDestroy, OnInit } from '@angular/core';`

	@Component({
	selector: 'app-ajuda-fluxo',
	templateUrl: './ajuda-fluxo.component.html',
	styleUrl: './ajuda-fluxo.component.css'
	})

	export class AjudaFluxoComponent implements OnInit, OnDestroy {

	observer!: IntersectionObserver;

	ngOnInit(): void {
		this.observer = new IntersectionObserver((entries) => {
			entries.forEach(entry => {
				const elemento = entry.target as HTMLElement;
	
				if (entry.isIntersecting) {
				elemento.classList.add('scroll-suave');
				elemento.classList.remove('scroll-escondido');
				this.observer.unobserve(elemento);
				}
			});
		}, {
			root: null,
			rootMargin: '0px 0px -50px 0px',
			threshold: 0.1
		});

		const elementos = document.querySelectorAll('.scroll-escondido');
		elementos.forEach(el => this.observer.observe(el));
	}

	ngOnDestroy(): void {
		if (this.observer) {
				this.observer.disconnect();
			}
		}
	}

![[Captura de tela de 2025-07-30 14-36-30.png]]