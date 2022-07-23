# PROJETO FINAL DA DISCIPLINA DE PROCESSAMENTO DIGITAL DE SINAIS II   <br><br>

## Corretor automatizado de angulação na digitalização de documentos <br><br>
**IFSC - Curso de Engenharia Eletrônica**               <br>
**Professor: Fernando Pacheco**                         <br>
**Aluno: Eric Monteiro dos Reis**                       <br><br>

#### Objetivo
Desenvolver um programa capaz de receber um arquivo no formato pdf, contendo a digitalização de um documento que possui páginas tortas e a partir da aplicação de técnicas de processamento de imagem utilizando a lingugagem *Python*, gerar um arquivo pdf com as páginas corrigidas.

#### Fluxo de funcionamento do código

1° - Programa pede ao usuário o *path* onde se encontra o pdf que deseja ser corrigido. <br>
2° - Usuário insere no código o nome do arquivo na função de leitura do pdf. O programa utiliza atualmente a biblioteca *pdf2image*, onde a leitura utilizando uma variável com o nome do arquivo por motivo desconhecido não funcionou, portanto é necessário inserir o nome dentro da função do código. <br>
3° - Criação de pastas entituladas "pdf_images" e "pdf_output" no *path* fornecido, onde serão salvas as imagens lidas na pasta "pdf_images" e o resultado final na pasta "pdf_output". <br>
4° - Leitura e conversão das páginas do pdf para imagens no formato PNG. <br>
5° - As imagens são salvas numa lista e são lidas pelo programa utilizando a biblioteca *OpenCV*. <br>
6° - Em cada imagem é aplicada os seguintes passos: utilização da Transformada de Hough -> cálculo do ângulo de inclinação -> rotação da página -> aplicação de *frame* para limpar as bordas da imagem -> *threshold* para melhorar a qualidade da digitalização. <br>
7° - As imagens tratadas são salvas em uma lista e o programa mostra os ângulos cálculados em cada leitura de página. <br>
8° - Utilizando a biblioteca *Pillow* convertemos a lista de imagens tratadas para o formato adequado e juntamos a lista em um pdf na pasta "pdf_output".

#### Possíveis soluções que podem melhorar a qualidade do programa:

- Antes da utilização do algoritmo de Canny de detecção de bordas e da Transformada de Hough para detecção de linhas, a realização de uma operação morfológica de dilatação na imagem poderia resultar em uma captura melhor das linhas no documento, consequentemente aumentando a precisão do ângulo calculado.
- Utilização de operação morfológica de dilatação na imagem, seguido de aplicação da função do *OpenCV* *minAreaRect()* para obtermos um retângulo que representa o contorno mínimo do texto, de forma a centralizar as informações na página.
- Os parametros *minLineLength* e *maxLineGap* na função de detecção de linhas *HoughLinesP* na versão atual do projeto são valores fixos, escolhidos de forma empírica. A escolhas desses parâmetros sendo baseadas em informações obtidas do tamanho em pixel das páginas do documento, ou outra informação de interesse podem produzir resultados mais satisfatórios na obtenção da angulação do texto.
- Implementação de uma opção onde o usuário escolhe 4 pontos em alguma das páginas do pdf que sejam consideradas falhas, para aplicação funções de correção de perspectiva caso ela esteja distorcida,  e isso também corrigiria o ângulo da digitalização. 
- Utilização de modelos de aprendizado de máquinas (Tesseract por exemplo), para performar o reconhecimento de caractéres no texto e posteriormente a conversão das imagens em um documento de texto.
