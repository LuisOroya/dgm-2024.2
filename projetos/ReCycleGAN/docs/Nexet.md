
# Nexet 2017

A base de dados **Nexet 2017** cont�m 50.000 imagens, e 99,8% tem resolu��o 1280x720. Todas as imagens tem dados de condi��o de luz (dia, noite, ocaso) e local (Nova York, S�o Francisco, Tel Aviv, Resto do mundo). Tamb�m existem dados anotados da posi��o (*box*) dos ve�culos que aparecem em cada imagem. Para o treinamento e teste das redes propostas foram utilizadas apenas as imagens 1280x720 de Nova York, nas condi��es de luz **dia** (4885 imagens) e **noite** (4406 imagens).

<div>
    <p align="center">
        <img src='assets/nexet_imgs.png' align="center" alt="Imagens Nexet" width=600px>
    </p>
</div>

<p align="center">
    <strong>Exemplos de imagens da base Nexet 2017 (dia acima e noite abaixo).</strong>
</p>

## Imagens com Problemas

Algumas das imagens da base de dados parecem ter tido problemas na sua captura. Em diversas imagens o conte�do da mesma se encontrava em um dos cantos da imagem. Para tratar estas imagens � feita uma busca pela linhas e colunas da imagem buscando *informa��o*. Uma linha ou coluna � considerada *sem informa��o* quando a imagem equivalente em escala de cinza n�o tinha nenhum pixel com valor maior que 10 (em uma escala at� 255). A imagem original � ent�o cortada na regi�o *com informa��o* antes de escalar e cortar as imagens para 256x256. Imagens recortadas com menos de 256 pixeis de altura ou largura foram ignoradas (imagem � esquerda abaixo).

<div>
    <p align="center">
        <img src='assets/nexet/bad_image01.jpg' align="center" alt="Imagem ruim" width=250px>
        <img src='assets/nexet/bad_image02.jpg' align="center" alt="Imagem ruim" width=250px>
    </p>
</div>

<p align="center">
    <strong>Exemplos de imagens com problemas.</strong>
</p>

## Filtro de Imagens

Observou-se que algumas imagens da base de dados Nexet apresentavam caracter�sticas que poderiam comprometer a qualidade do treinamento. Foi feito um trabalho *semi*-manual de filtragem destas imagens. Muitas das an�lises foram feitas com base nas *dist�ncias* entre as imagens de cada grupo. Estas dist�ncias foram calculadas a partir da sa�da da pen�ltima camada de uma rede classificadora de imagens pr�-treinada ResNet18 [[13]](https://doi.org/10.1109/CVPR.2016.90), disponibilizada diretamente no [PyTorch](https://pytorch.org/vision/main/models/generated/torchvision.models.resnet18.html). Esta extra��o de caracter�sticas foi realizada com as imagens j� escaladas e recortadas para o formato de treinamento.

### Imagens muito parecidas

* Foram listados os pares de imagens que apresentavam menores dist�ncias entre si.
* Foi definido por inspe��o visual, para a classe **dia**, que os 93 pares mais pr�ximos eram de imagens muito semelhantes. Para cada par uma das imagens � exclu�da da base de dados.
* Para a classe **noite** esta abordagem n�o se mostrou muito eficiente. Imagens com pequena dist�ncia entre si n�o eram consideradas parecidas em uma inspe��o visual. Para esta classe nenhuma imagem foi retirada.

<div>
    <p align="center">
        <img src='assets/nexet/close_pair_day_01.png' align="center" alt="Imagens pr�ximas dia 1" width=350px>
        <img src='assets/nexet/close_pair_day_02.png' align="center" alt="Imagens pr�ximas dia 2" width=350px>
    </p>
</div>

<p align="center">
  <strong>Exemplos de pares de imagens muito parecidas na classe dia.</strong>
</p>

<div>
    <p align="center">
        <img src='assets/nexet/close_pair_night_01.png' align="center" alt="Imagens pr�ximas noite 1" width=350px>
        <img src='assets/nexet/close_pair_night_02.png' align="center" alt="Imagens pr�ximas noite 2" width=350px>
    </p>
</div>

<p align="center">
    <strong>Exemplos de pares de imagens muito parecidas na classe noite.</strong>
</p>

### Imagens *Dif�ceis*

* Para *facilitar* o treinamento da rede, foram exclu�das imagens com caracter�sticas consideradas *dif�ceis* ou que n�o ajudam no treinamento: chuva *forte*, t�neis, desfoque, objetos bloqueando a vis�o.
* Para esta an�lise as imagens de cada classe foram agrupadas em 20 classes, com **k-Means**. Para cada classe foram sorteadas 36 imagens e foi feita uma an�lise visual de cada grupo.
* A partir da an�lise visual, os grupos que foram considerados *problem�ticos* s�o novamente divididos com k-means. A an�lise visual dos subgrupos � que define que conjuntos de imagens s�o exclu�dos do treinamento.

<div>
    <p align="center">
        <img src="assets/nexet/bad_cluster_day.jpg" align="center" alt="Imagens dif�ceis dia" width=350px>
        <img src="assets/nexet/bad_cluster_night.jpg" align="center" alt="Imagens dif�ceis noite" width=350px>
    </p>
</div>

<p align="center">
    <strong>Exemplos de grupos de imagens consideradas dif�ceis para o treinamento.</strong>
</p>

Os filtros aplicados retiraram 146 (3%) das imagens da classe **Dia** e 216 (5%) das imagens da classe **Noite**. Os totais de imagens para cada classe s�o apresentados abaixo.

| Classe       | Treino | Teste | Total |
|--------------|--------|-------|-------|
|**Dia** (A)   | 3788   | 949   | 4737  |
|**Noite** (B) | 3316   | 842   | 4158  |

Todo o procedimento de filtro das imagens est� codificado em um �nico [Notebook](../src/notebooks/Filter_DayNight.ipynb).

A base de dados utilizada pode ser encontrada neste [link](https://github.com/TiagoCAAmorim/dgm-2024.2/releases/download/v0.1.1-nexet/Nexet.zip). Foram utilizadas as imagens listadas nos arquivos com *\_filtered.csv* no final do nome.
