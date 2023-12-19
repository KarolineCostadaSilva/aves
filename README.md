# 🐦‍⬛🦜🦢🦅🦃🐓🦆 Classificação de imagens de pássaros 🐧🐦🦤🦉🦚🦩🪿

## Introdução 🪶
Nesse projeto, o objetivo foi classificar 524 classes de pássaros utilizando Redes Neurais Convolucionais. Escolhi o conjunto de dataset disponível no [Kaggle](https://www.kaggle.com/datasets/gpiosenka/100-bird-species), onde o conjunto de dados contém 525 espécies de aves. 84.635 imagens de treinamento, 2.625 imagens de teste (5 imagens por espécie) e 2.625 imagens de validação (5 imagens por espécie. Utilizei o [Pytorch](https://pytorch.org/) como Framework, o [Optuna](https://optuna.org/) como framework para otimização de hiperparâmetros e [MLFlow](https://mlflow.org/) como plataforma de código aberto para gerenciar o ciclo de vida de modelos de aprendizado de máquina de ponta a ponta.

Resultados das métricas:
Acurácia: 99.16%
F1-Score: 96.47%
Precisão: 96.93%
Recall: 96.17%

## Motivação 🪶
Mudanças climáticas estão ocorrendo em todo o mundo em um ritmo muito acelerado, e muitas espécies de aves correm sério risco de extinção. A identificação automática de espécies de pássaros pode ser uma ferramenta valiosa para ecologistas e biólogos na monitorização da biodiversidade e na realização de estudos ambientais. Além disso, pássaros apresentam uma enorme variedade de cores, padrões, tamanhos e formas. Isso torna a classificação multiclasse de pássaros um excelente teste para as capacidades de reconhecimento visual das redes neurais. E, por fim, eu adoro pássaros! 

## Dependências 🪶
- Python 3.6.8
- Pytorch 1.10.0
- Torchvision 0.11.0
- Optuna 3.0.6
- OpenCV 3.4.13.47
- Pillow 8.4.0
- Timm 0.6.12
- GPU GeForce RTX 4090

## Sobre o dataset (extraído na descrição do dataset no Kaggle) 🪶
Todas as imagens são imagens coloridas de 224 x 224 x 3 em formato jpg. O conjunto de dados inclui um conjunto de treinamento, um conjunto de testes e um conjunto de validação. Cada conjunto contém 525 subdiretórios, um para cada espécie de ave. O conjunto de dados também inclui um arquivo birds.csv. Este arquivo cvs contém 5 colunas. A coluna filepaths contém o caminho relativo do arquivo para um arquivo de imagem. A coluna de rótulos contém o nome da classe da espécie de ave associada ao arquivo de imagem. A coluna do rótulo científico contém o nome científico latino da imagem. A coluna do conjunto de dados indica em qual conjunto de dados (treinamento, teste ou válido) o caminho do arquivo reside. A coluna class_id contém o valor do índice de classe associado à classe do arquivo de imagem. As imagens foram coletadas de pesquisas na internet por nome de espécie. Uma vez baixados os arquivos de imagem de uma espécie, eles foram verificados quanto à presença de imagens duplicadas ou quase duplicadas. Todas as imagens duplicadas ou quase duplicadas detectadas foram excluídas para evitar que fossem imagens comuns entre os conjuntos de treinamento, teste e validação.

Depois disso as imagens foram recortadas para que o pássaro na maioria dos casos ocupe pelo menos 50% do pixel da imagem. Em seguida as imagens foram redimensionadas para 224 X 224 X3 no formato jpg. O recorte garante que quando processado por uma CNN haja informações adequadas nas imagens para criar um classificador altamente preciso. Todos os arquivos também foram numerados sequencialmente a partir de um para cada espécie. Portanto, as imagens de teste são nomeadas de 1.jpg a 5.jpg. Da mesma forma para imagens de validação. As imagens de treinamento também são numeradas sequencialmente com preenchimento de "zeros". Por exemplo 001.jpg, 002.jpg….010.jpg, 011.jpg…..099.jpg, 100jpg, 102.jpg etc. O conjunto de treinamento não é balanceado, possuindo um número variável de arquivos por espécie. Porém cada espécie possui pelo menos 130 arquivos de imagens de treinamento.

Uma deficiência significativa no conjunto de dados é a proporção entre imagens de espécies masculinas e imagens de espécies femininas. Cerca de 80% das imagens são masculinas e 20% femininas. Os machos típicos têm cores muito mais diversas, enquanto as fêmeas de uma espécie são tipicamente insípidas. Consequentemente, as imagens masculinas e femininas podem parecer totalmente diferentes. Quase todas as imagens de teste e validação são tiradas do macho da espécie.

obs.: Há uma pasta chamada Looney Birds que não são sobre pássaros, portanto foi removida, totalizando 524 classes.

## Códigos 🪶
1. EDA
2. Criação e treinamento com seleção de hiperparâmetros com Optuna
3. Aplicação e avaliação do modelo com melhor resultado na métrica de avaliação no MLFlow

## Como executar o código 🪶
1. Como disse anteriormente, o dataset está disponível no Kaggle. Utilizei o API do Kaggle para realizar o download do dataset. Para mais informações acesse [aqui](https://www.kaggle.com/docs/api).
2. Coloque o dataset na pasta `./100-bird-species`
   
   obs.: Não esqueça de alterar o caminho correto no seu computador.
3. Execute o arquivo .ipynb para uma análise exploratória dos dados.

```
EDA_bird_classification.ipynb
```

4. Execute o arquivo .ipynb para executar o treinamento com seleção de hiperparâmetros. Como essa etapa é para seleção de hiperparâmetros, cada treinamento teve 1 época, mas fiz 100 trials no Optuna.

```
bird_classification.ipynb
```
   obs.: Para a escolha dos 4 algoritmos de predição, escolhi as Redes Neurais Convolucionais VGG16, ResNet50, EfficientNet e DenseNet. Todas com Aprendizado por Transferência e descongelamento da última camada.
   
   obs2.: Esse arquivo pode demorar um pouco. O seu tempo de execução ficou, em média, 4 horas.

5. Execute o arquivo .ipynb para aplicar o melhor modelo com o melhor hiperparâmetro no dataset de test no MLFlow.

```
mlflow_bird_classification.ipynb
```

## Ferramentas utilizadas 🪶
<p align="left"> <a href="https://matplotlib.org/" target="_blank" rel="noreferrer"> <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/01/Created_with_Matplotlib-logo.svg/2048px-Created_with_Matplotlib-logo.svg.png" alt="matplotlib" width="40" height="40"/> </a> <a href="https://numpy.org/" target="_blank" rel="noreferrer"> <img src="https://user-images.githubusercontent.com/50221806/86498201-a8bd8680-bd39-11ea-9d08-66b610a8dc01.png" alt="numpy" width="40" height="40"/> </a> <a href="https://opencv.org/" target="_blank" rel="noreferrer"> <img src="https://github.com/opencv/opencv/wiki/logo/OpenCV_logo_no_text.png" alt="opencv" width="40" height="40"/> </a> <a href="https://www.python.org/" target="_blank" rel="noreferrer"> <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c3/Python-logo-notext.svg/1869px-Python-logo-notext.svg.png" alt="python" width="40" height="40"/> </a> <a href="https://scipy.org/" target="_blank" rel="noreferrer"> <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/b2/SCIPY_2.svg/1200px-SCIPY_2.svg.png" alt="scipy" width="40" height="40"/> </a> <a href="https://pytorch.org/" target="_blank" rel="noreferrer"> <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/10/PyTorch_logo_icon.svg/640px-PyTorch_logo_icon.svg.png" alt="scipy" width="35" height="40"/> </a> <a href="https://seaborn.pydata.org/installing.html" target="_blank" rel="noreferrer"> <img src="https://seeklogo.com/images/S/seaborn-logo-244EB2DEC5-seeklogo.com.png" alt="seaborn" width="40" height="40"/> </a> <a href="https://scikit-learn.org/stable/" target="_blank" rel="noreferrer"> <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/05/Scikit_learn_logo_small.svg/2560px-Scikit_learn_logo_small.svg.png" alt="scikitlearn" width="75" height="40"/> </a> <a href="https://anaconda.org/anaconda/python" target="_blank" rel="noreferrer"> <img src="https://anaconda.org/static/img/anaconda-symbol.svg" alt="anaconda" width="40" height="40"/> </a> </p>




<p align="center">
  <i>"Aqueles que contemplam a beleza da terra encontram reservas de força que durarão enquanto a vida durar."</i><br>
  Rachel Carson, <em>Primavera Silenciosa</em>
</p>
