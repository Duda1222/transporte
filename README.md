# Otimização de Transporte
Sistema em Python utilizando o método Simplex para otimizar a logística de entregas em uma rede de farmácias.

# Objetivo
Desenvolvi um programa com o intuito de aplicar uma modelagem matemática voltada à minimização dos custos logísticos entre farmácias e clientes. O custo considerado foi a distância entre os pontos de origem (farmácias) e os destinos (clientes), buscando determinar quais lojas devem atender quais clientes da forma mais econômica possível, levando em conta o estoque disponível em cada farmácia e a demanda de cada pedido.

Modelagem e Funcionamento
A modelagem utilizada é baseada no problema clássico de transporte e foi resolvida com o método Simplex. 
O algoritmo requer dois arquivos .csv como entrada: farmacias.csv e solicitacoes.csv. Ambos devem conter os campos de identificação, latitude, longitude e estoque ou demanda, conforme os exemplos abaixo:

farmacias.csv
Loja	Latitude	Longitude	Estoque
1	-16.751524	-43.879035	50
2	-16.713941	-43.853944	50
3	-16.740076	-43.870815	50

solicitacoes.csv
Cliente	Latitude	Longitude	Solicitação
1	-16.690414	-43.836981	5
2	-16.713023	-43.837304	45
3	-16.730625	-43.857152	100

Após a leitura dos arquivos, o sistema armazena as coordenadas e calcula a distância entre cada farmácia e cada cliente utilizando a fórmula de Haversine — uma equação amplamente usada em navegação para medir a distância entre dois pontos na Terra, baseada em suas coordenadas geográficas. Essas distâncias representam o custo de transporte entre cada par loja-cliente.

Exemplo da tabela de entrada para o modelo
Lojas	S1	S2	S3	Estoque
L1	8	6	3	50
L2	3	2	2	50
L3	7	5	2	50
Demanda	5	45	100	---

Com esses dados, o sistema constrói a função objetivo e as restrições do problema:

Função objetivo:
Z = 8x1 + 6x2 + 3x3 + 3x4 + 3x5 + 3x6 + 7x7 + 5x8 + 2x9

Restrições:


x1 + x2 + x3 <= 50  
x4 + x5 + x6 <= 50  
x7 + x8 + x9 <= 50  

x1 + x4 + x7 = 5  
x2 + x5 + x8 = 45  
x3 + x6 + x9 = 100  

x1, ..., x9 >= 0
As restrições são formatadas automaticamente para serem compatíveis com o sistema de resolução online de transporte desenvolvido pelo CEFET-MG, disponível em: SIMO.

O algoritmo gera um arquivo .txt com a modelagem do problema, pronto para ser importado no SIMO, que por sua vez apresenta a solução de maneira visual e clara por meio de tabelas:

Exemplo de Solução
Loja	Quantidade	Cliente
1	50	3
2	5	1
2	45	2
3	50	3
Custo Total:	10.0 Km	
Nº de Farmácias:	3	
Nº de Clientes:	3	

Caso o problema esteja desbalanceado (estoque ≠ demanda total), o algoritmo realiza o balanceamento automaticamente com variáveis artificiais e informa o usuário.

Execução
Para rodar o sistema, é necessário ter Python (versão 3.7.5 ou superior) e a biblioteca NumPy (versão 1.17.4 ou superior).


Desenvolvedora
Maria Eduarda Almeida – Graduanda em Ciência da Computação – UFJ
GitHub - Maria Eduarda
