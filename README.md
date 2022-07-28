# trabalhoCalango
algoritmo trabalhoCalango;
// Síntese
//  Objetivo:  receber o limite de velocidade da via, a quantidade de veículos que serão contabilizados, a categoria e a velocidade de cada veículo ao
//		passar por um radar eletrônico; mostrar a quantidade de multas que serão emitidas, juntamente à velocidade flagrada e o valor de cada multa.
//  Entrada : velocidade máxima da via, quantidade de veículos, categoria e velocidade de cada veículo.
//  Saída   :  listagem dos veículos autuados, exibindo a velocidade de cada um ao passar pelo radar e o valor da multa ser aplicada.

principal

	inteiro vmi, vmi2, qvei, multados, fastest, asc[1000], auxCat, f, t, c, h, g, i, j, n, d, m;
	texto mot, car, cam, vehi[1000];
	real vfm, vrm[1000], spd[1000], vmr, aux, tot;
	caracter cat[1000], reboot;

	d = 1;
	j = 1;
	c = 1;
	h = 1;
	m = 1;
	g = 1;
	n = 1;
	f = 0;
	i = 0;
	tot = 0;
	vehi[g] = " ";
	vehi[h] = " ";
	vehi[m] = " ";
	vehi[c] = " ";
	vehi[d] = " ";
	spd[j] = 1;
	vrm[j] = 1;
	cat[j] = 'a';
	vfm = 0;
	fastest = 0;
	spd[i] = 1;
	cat[i] = 'a';
	vrm[i] = 1;
	spd[d] = 0;
	vrm[d] = 0;
	cat[d] = 'a';
	spd[m] = 1;
	vrm[m] = 1;
	cat[m] = 'a';
	spd[g] = 0;
	vrm[g] = 0;
	cat[g] = 'a';
	asc[j] = 1;
	asc[i] = 1;
	asc[d] = 1;
	asc[m] = 1;
	asc[g] = 1;
	asc[f] = 1;

	escreval("➲ BEM-VINDO AO RADAR BRASIL™!");
	escreval("Insira a velocidade máxima da via:");
	leia(vmi);

	se (vmi <= 0) entao
		escreval("✘ ERRO! Insira um número maior que zero!");
		leia(vmi);
	senao
		se (vmi <= 99) entao
			vmr = vmi + 7;
		senao
			se (vmi >= 100) entao
				vmr = vmi + vmi * 0.07;
			fimSe
		fimSe
	fimSe

	se (vmi <= 100) entao
		vmr = vmi + 7;
	senao
		se (vmi > 100) entao
			vmr = vmi + vmi * 0.07;
		fimSe
	fimSe

	escreval("Insira a quantidade de veículos que serão contabilizados:");
	leia(qvei);

	se (qvei <= 0) entao
		limpaTela();
		escreval("✘ ERRO! Insira um número maior que zero!");
		leia(qvei);
	fimSe

	limpaTela();

	para (d de 1 ate qvei passo 1) faca
		escreval("➲ INSIRA A CATEGORIA DO ", d, "° VEÍCULO:");
		escreval("A ⇋ Motocicleta");
		escreval("B ⇋ Carro");
		escreval("C ⇋ Caminhão");

		leiaCaracter(cat[d]);
		cat[d] = maiusculoCaracter(cat[d]);

		se (cat[d] != 'A' e cat[d] != 'B' e cat[d] != 'C') entao
			limpaTela();

			escreval("✘ ERRO! Insira uma alternativa válida.");
			escreval(" ");

			escreval("➲ INSIRA A CATEGORIA DO ", d, "° VEÍCULO:");
			escreval("A ⇋ Motocicleta");
			escreval("B ⇋ Carro");
			escreval("C ⇋ Caminhão");

			leiaCaracter(cat[d]);
			cat[d] = maiusculoCaracter(cat[d]);
		fimSe

		escreval("➲ Insira a velocidade do veículo (Km/H) no momento em que foi fotografado:");
		leia(spd[d]);

		se (spd[d] <= 0) entao
			limpaTela();
			escreval("✘ ERRO! Insira um número maior que zero!");
			escreval("➲ Insira a velocidade do veículo (Km/H) no momento em que foi fotografado:");
			leia(spd[d]);
		fimSe

		limpaTela();
		
		se (spd[d] < vmr + vmr * 0.2) entao
			vfm = 130.16;
		senao
			se (spd[d] >= vmr + vmr * 0.2 e spd[d] <= vmr + vmr * 0.5) entao
				vfm = 195.23;
			senao
				se (spd[d] > vmr + vmr * 0.5) entao
					vfm = 880.41;
				fimSe
			fimSe
		fimSe
		
		se (cat[d] == 'A') entao
			vrm[d] = vfm + (vfm * 0.025);
		senao
			se (cat[d] == 'B') entao
				vrm[d] = vfm + (vfm * 0.05);
			senao
				se (cat[d] == 'C') entao
					vrm[d] = vfm + (vfm * 0.075);
				fimSe
			fimSe
		fimSe
	fimPara

	limpaTela();

	para(j de 1 ate qvei  passo 1)faca
		para(m de j ate qvei passo 1)faca
			se(vrm[j] < vrm[m])entao
				aux = vrm[m];
				vrm[m] = vrm[j];
				vrm[j] = aux;
				
				aux = spd[m];
				spd[m] = spd[j];
				spd[j] = aux;
			fimSe
		fimPara
	fimPara
	
	n = 1;

	escreval("DENTRE OS ", qvei, " VEÍCULOS ANALISADOS, SERÃO EMITIDAS AS MULTAS:");

	para(g de 1 ate qvei  passo 1)faca
		se (spd[g] > vmr) entao
			se (cat[g] == 'A') entao
				escreval(n, " ▸ ", spd[g]::0, "Km/h", " ..................................... R$", vrm[g]::2);
			fimSe
			se (cat[g] == 'B') entao
				escreval(n, " ▸ ", spd[g]::0, "Km/h", " ..................................... R$", vrm[g]::2);
			fimSe
			se (cat[g] == 'C') entao
				escreval(n, " ▸ ", spd[g]::0, "Km/h", " ..................................... R$", vrm[g]::2);
			fimSe
			n = n + 1;
		fimSe
	fimPara

	escreval(" ");
	escreval("➲ DESEJA REINICIAR A EXECUÇÃO DO RADAR BRASIL™?");
	escreval("S ▸ Sim");
	escreval("N ▸ Não");
	leiaCaracter(reboot);
	reboot = maiusculoCaracter(reboot);

	se (reboot == 'S') entao
		limpaTela();
		reiniciar();
	senao
		limpaTela();
		escreval("➲ OBRIGADO POR ACESSAR O RADAR BRASIL™!");
		escreval("Finalizando execução...");
	fimSe

fimPrincipal

funcao texto reiniciar()
	inteiro vmi, vmi2, qvei, multados, fastest, asc[1000], auxCat, f, t, c, h, g, i, j, n, d, m;
	texto mot, car, cam, vehi[1000];
	real vfm, vrm[1000], spd[1000], vmr, aux, tot;
	caracter cat[1000], reboot;

	d = 1;
	j = 1;
	c = 1;
	h = 1;
	m = 1;
	g = 1;
	n = 1;
	f = 0;
	i = 0;
	tot = 0;
	vehi[g] = " ";
	vehi[h] = " ";
	vehi[m] = " ";
	vehi[c] = " ";
	vehi[d] = " ";
	spd[j] = 1;
	vrm[j] = 1;
	cat[j] = 'a';
	vfm = 0;
	fastest = 0;
	spd[i] = 1;
	cat[i] = 'a';
	vrm[i] = 1;
	spd[d] = 0;
	vrm[d] = 0;
	cat[d] = 'a';
	spd[m] = 1;
	vrm[m] = 1;
	cat[m] = 'a';
	spd[g] = 0;
	vrm[g] = 0;
	cat[g] = 'a';
	asc[j] = 1;
	asc[i] = 1;
	asc[d] = 1;
	asc[m] = 1;
	asc[g] = 1;
	asc[f] = 1;

	escreval("➲ BEM-VINDO AO RADAR BRASIL™!");
	escreval("Insira a velocidade máxima da via:");
	leia(vmi);

	se (vmi <= 0) entao
		escreval("✘ ERRO! Insira um número maior que zero!");
		leia(vmi);
	senao
		se (vmi <= 99) entao
			vmr = vmi + 7;
		senao
			se (vmi >= 100) entao
				vmr = vmi + vmi * 0.07;
			fimSe
		fimSe
	fimSe

	se (vmi <= 100) entao
		vmr = vmi + 7;
	senao
		se (vmi > 100) entao
			vmr = vmi + vmi * 0.07;
		fimSe
	fimSe

	escreval("Insira a quantidade de veículos que serão contabilizados:");
	leia(qvei);

	se (qvei <= 0) entao
		limpaTela();
		escreval("✘ ERRO! Insira um número maior que zero!");
		leia(qvei);
	fimSe

	limpaTela();

	para (d de 1 ate qvei passo 1) faca
		escreval("➲ INSIRA A CATEGORIA DO ", d, "° VEÍCULO:");
		escreval("A ⇋ Motocicleta");
		escreval("B ⇋ Carro");
		escreval("C ⇋ Caminhão");

		leiaCaracter(cat[d]);
		cat[d] = maiusculoCaracter(cat[d]);

		se (cat[d] != 'A' e cat[d] != 'B' e cat[d] != 'C') entao
			limpaTela();

			escreval("✘ ERRO! Insira uma alternativa válida.");
			escreval(" ");

			escreval("➲ INSIRA A CATEGORIA DO ", d, "° VEÍCULO:");
			escreval("A ⇋ Motocicleta");
			escreval("B ⇋ Carro");
			escreval("C ⇋ Caminhão");

			leiaCaracter(cat[d]);
			cat[d] = maiusculoCaracter(cat[d]);
		fimSe

		escreval("➲ Insira a velocidade do veículo (Km/H) no momento em que foi fotografado:");
		leia(spd[d]);

		se (spd[d] <= 0) entao
			limpaTela();
			escreval("✘ ERRO! Insira um número maior que zero!");
			escreval("➲ Insira a velocidade do veículo (Km/H) no momento em que foi fotografado:");
			leia(spd[d]);
		fimSe

		limpaTela();
		
		se (spd[d] < vmr + vmr * 0.2) entao
			vfm = 130.16;
		senao
			se (spd[d] >= vmr + vmr * 0.2 e spd[d] <= vmr + vmr * 0.5) entao
				vfm = 195.23;
			senao
				se (spd[d] > vmr + vmr * 0.5) entao
					vfm = 880.41;
				fimSe
			fimSe
		fimSe
		
		se (cat[d] == 'A') entao
			vrm[d] = vfm + (vfm * 0.025);
		senao
			se (cat[d] == 'B') entao
				vrm[d] = vfm + (vfm * 0.05);
			senao
				se (cat[d] == 'C') entao
					vrm[d] = vfm + (vfm * 0.075);
				fimSe
			fimSe
		fimSe
	fimPara

	limpaTela();

	para(j de 1 ate qvei  passo 1)faca
		para(m de j ate qvei passo 1)faca
			se(vrm[j] < vrm[m])entao
				aux = vrm[m];
				vrm[m] = vrm[j];
				vrm[j] = aux;
				
				aux = spd[m];
				spd[m] = spd[j];
				spd[j] = aux;
			fimSe
		fimPara
	fimPara
	
	n = 1;

	escreval("DENTRE OS ", qvei, " VEÍCULOS ANALISADOS, SERÃO EMITIDAS AS MULTAS:");

	para(g de 1 ate qvei  passo 1)faca
		se (spd[g] > vmr) entao
			se (cat[g] == 'A') entao
				escreval(n, " ▸ ", spd[g]::0, "Km/h", " ..................................... R$", vrm[g]::2);
			fimSe
			se (cat[g] == 'B') entao
				escreval(n, " ▸ ", spd[g]::0, "Km/h", " ..................................... R$", vrm[g]::2);
			fimSe
			se (cat[g] == 'C') entao
				escreval(n, " ▸ ", spd[g]::0, "Km/h", " ..................................... R$", vrm[g]::2);
			fimSe
			n = n + 1;
		fimSe
	fimPara

	escreval(" ");
	escreval("➲ DESEJA REINICIAR A EXECUÇÃO DO RADAR BRASIL™?");
	escreval("S ▸ Sim");
	escreval("N ▸ Não");
	leiaCaracter(reboot);
	reboot = maiusculoCaracter(reboot);

	se (reboot == 'S') entao
		limpaTela();
		reiniciar();
	senao
		limpaTela();
		escreval("➲ OBRIGADO POR ACESSAR O RADAR BRASIL™!");
		escreval("Finalizando execução...");
	fimSe

	retorna(" ");

fimFuncao
