# Resultados

A tabela abaixo apresenta um resumo dos principais resultados obtidos na compara��o das imagens geradas por cada modelo testado com as imagens reais (e.g.: imagens da classe B, noite, transformadas em imagens da classe A, dia, comparadas com as imagens reais da classe A). Todas as m�tricas foram calculadas usando as imagens de treino e de teste.

|Transforma��o |Modelo | FID | LPIPS |
|-|-|-:|-:|
|A?B|CycleGAN |     .0 | 0. � 0. |
||ReCycleGAN 1 |     .0 | 0. � 0. |
||ReCycleGAN 2 |     .0 | 0. � 0. |
||ReCycleGAN 3 |     .0 | 0. � 0. |
||ReCycleGAN 4 |     .0 | 0. � 0. |
||ReCycleGAN 5 |     .0 | 0. � 0. |
||ReCycleGAN 6 |     .0 | 0. � 0. |
||ReCycleGAN 7 |     .0 | 0. � 0. |
||ReCycleGAN 8 |     .0 | 0. � 0. |
||ReCycleGAN 9 |     .0 | 0. � 0. |
|B?A|CycleGAN-turbo |     .0 | 0. � 0. |
||CycleGAN |     .0 | 0. � 0. |
||ReCycleGAN 1 |     .0 | 0. � 0. |
||ReCycleGAN 2 |     .0 | 0. � 0. |
||ReCycleGAN 3 |     .0 | 0. � 0. |
||ReCycleGAN 4 |     .0 | 0. � 0. |
||ReCycleGAN 5 |     .0 | 0. � 0. |
||ReCycleGAN 6 |     .0 | 0. � 0. |
||ReCycleGAN 7 |     .0 | 0. � 0. |
||ReCycleGAN 8 |     .0 | 0. � 0. |
||ReCycleGAN 9 |     .0 | 0. � 0. |
||CycleGAN-turbo |     .0 | 0. � 0. |

A coluna das transforma��es � preenchida apenas na primeira linha do respectivo conjunto de resultados para reduzir a polui��o visual da tabela. Para a m�trica LPIPS s�o apresentados o valor m�dio e o desvio padr�o.

## Mapas de Modelos

*Abusando* da ideia de dist�ncias das m�tricas, s�o montados mapas 2d com a posi��o relativa dos modelos. O mapa � constru�do a partir das dist�ncias entre todos os poss�veis conjuntos de imagens (reais x modelos, modelos x modelos) e aplicando MDS (Multidimensional scaling) para reduzir a informa��o a duas dimens�es.

<div>
<p align="center">
<img src='assets/evaluation/fid_map_images_A.png' align="center" alt="Mapa FID imagens A" width=300px>
</p>
<p align="center">
  <strong>Mapa dos modelos avaliados com FID para imagens da classe A.</strong>
</p>
</div>

<div>
<p align="center">
<img src='assets/evaluation/fid_map_images_B.png' align="center" alt="Mapa FID imagens B" width=300px>
</p>
<p align="center">
  <strong>Mapa dos modelos avaliados com FID para imagens da classe B.</strong>
</p>
</div>

Os mapas de modelos baseados nas m�dias da m�trica LPIPS n�o geraram bons resultados. Foi preciso introduzir um ajuste antes de montar o mapa das dist�ncias. A m�dia dos valores de LPIPS n�o � zero quando se compara um conjunto de imagens com o mesmo conjunto. Desta forma o LPIPS se aproxima mais de uma medida de *coer�ncia* entre as imagens do que uma dist�ncia.

O formato dos histogramas dos valores de LPIPS � aproximadamente de uma Gaussiana. Optou-se por usar a dist�ncia de Wasserstein como medida de dist�ncia entre a distribui��o das imagens reais entre si ($G_{RR}$) e a distribui��o entre as imagens reais e as imagens falsas ($G_{RF}$).

$$
  W(G_{RR},G_{RF}) = \sqrt{(\mu_{RR} - \mu_{RF})^2 + (\sigma_{RR} - \sigma_{RF})^2}
$$

<div>
  <p align="center">
    <img src='assets/evaluation/lpips_map_images_A.png' align="center" alt="Mapa LPIPS imagens A" width=300px>
  </p>
  <p align="center">
    <strong>Mapa dos modelos avaliados com LPIPS para imagens da classe A.</strong>
  </p>
</div>

<div>
  <p align="center">
    <img src='assets/evaluation/lpips_map_images_B.png' align="center" alt="Mapa LPIPS imagens B" width=300px>
  </p>
  <p align="center">
    <strong>Mapa dos modelos avaliados com LPIPS para imagens da classe B.</strong>
  </p>
</div>

## Histogramas de LPIPS

Uma outra tentativa de an�lise dos resultados foi comparar as distribui��es dos valores de LPIPS entre as imagens reais e falsas, por modelo testado.

<div>
  <p align="center">
    <img src='assets/evaluation/lpips_histograms_A.png' align="center" alt="Histograma LPIPS imagens A" width=300px>
  </p>
  <p align="center">
    <strong>Histogramas de valores de LPIPS para imagens da classe A.</strong>
  </p>
</div>

<div>
  <p align="center">
    <img src='assets/evaluation/lpips_histograms_B.png' align="center" alt="Histograma LPIPS imagens B" width=300px>
  </p>
  <p align="center">
    <strong>Histogramas de valores de LPIPS para imagens da classe B.</strong>
  </p>
</div>

## Amostragem de Imagens

A �ltima an�lise foi a da coer�ncia do LPIPS com a qualidade perceptual das imagens. Foi constru�do um histograma do valor m�dio do LPIPS entre todas as imagens reais e cada uma das imagens falsas geradas por um dos modelos de teste. Foram amostradas imagens com diferentes valores de LPIPS m�dio.

<div>
  <p align="center">
    <img src='assets/evaluation/lpips_histograms_samples_A.png' align="center" alt="Amostras de imagens A de um modelo" width=300px>
  </p>
  <p align="center">
    <strong>Amostras com diferentes valores de LPIPS m�dio para imagens da classe A geradas com o modelo XXXXX.</strong>
  </p>
</div>

<div>
  <p align="center">
    <img src='assets/evaluation/lpips_histograms_samples_B.png' align="center" alt="Amostras de imagens B de um modelo" width=300px>
  </p>
  <p align="center">
    <strong>Amostras com diferentes valores de LPIPS m�dio para imagens da classe B geradas com o modelo XXXXX.</strong>
  </p>
</div>

## Exemplos

Exemplos de imagens transformadas aleat�rias s�o apresentados abaixo.

<div>
  <p align="center">
    <img src='assets/evaluation/Samples_A.png' align="center" alt="Imagens A" width=600px>
  </p>
  <p align="center">
    <strong>Exemplos de imagens transformadas de dia para noite.</strong>
  </p>
</div>


<div>
  <p align="center">
    <img src='assets/evaluation/Samples_B.png' align="center" alt="Imagens B" width=600px>
  </p>
  <p align="center">
    <strong>Exemplos de imagens transformadas de noite para dia.</strong>
  </p>
</div>
