# Trabalho Final PDI: Detecção e Contagem de Células

Este projeto implementa um pipeline clássico de Processamento Digital de Imagens (PDI) para a detecção, separação e contagem automatizada de células em imagens microscópicas. O código-fonte, o passo a passo metodológico e a validação dos resultados encontram-se no arquivo principal do projeto, nomeado `projeto_pdi_celulas.ipynb`.

## 📋 Sobre o Projeto

O objetivo principal deste sistema é resolver o problema da contagem de agrupamentos de células, onde múltiplas células sobrepostas poderiam ser erroneamente contadas como uma única entidade. Para isso, o algoritmo utiliza uma combinação de limiarização adaptativa, operações morfológicas e a aplicação do algoritmo Watershed.

No final da execução, o sistema processa um lote de imagens, desenha os contornos das células detectadas, salva os resultados e gera um relatório comparativo validando a contagem automática contra marcações manuais de referência.

---

## 🛠️ Tecnologias e Dependências

O projeto foi desenvolvido em Python e utiliza as seguintes bibliotecas:
*   **OpenCV (`cv2`)**: Processamento principal de imagens e detecção de contornos[cite: 1].
*   **NumPy**: Manipulação de matrizes e arrays[cite: 1].
*   **Matplotlib**: Exibição das imagens e plotagem de resultados[cite: 1].
*   **SciPy (`scipy.ndimage`)**: Geração de marcadores[cite: 1].
*   **Scikit-Image (`skimage.feature`)**: Extração de picos de máximos locais para o aprimoramento do Watershed[cite: 1].

---

## ⚙️ Pipeline de Processamento

O fluxo de processamento documentado no `projeto_pdi_celulas.ipynb` segue estas etapas[cite: 1]:

1.  **Carregamento e Conversão**: Leitura das imagens `.tif` originais convertidas diretamente para tons de cinza[cite: 1].
2.  **Suavização**: Aplicação de um Filtro Gaussiano de dimensão (5, 5) para mitigar o ruído de alta frequência no fundo da imagem e preservar o formato geral das células[cite: 1].
3.  **Binarização**: Utilização do método de Limiarização de Otsu para separar dinamicamente os pixels de fundo dos pixels das células[cite: 1].
4.  **Operações Morfológicas**: 
    *   Execução de uma operação de Abertura para eliminar pequenos ruídos[cite: 1].
    *   Aplicação de uma Dilatação adicional para extrair com segurança a área pertencente ao fundo da imagem (background seguro)[cite: 1].
5.  **Transformada de Distância e Watershed**: 
    *   Aplicação da Transformada de Distância para localizar o centro isolado de cada célula[cite: 1].
    *   Detecção dos máximos locais (`peak_local_max`) para gerar sementes precisas[cite: 1].
    *   Uso do algoritmo Watershed para construir "barreiras" artificiais e separar as células aglomeradas/sobrepostas[cite: 1].
6.  **Filtragem e Contagem**: 
    *   Isolamento das marcações do Watershed[cite: 1].
    *   Extração de contornos individuais[cite: 1].
    *   Aplicação de um filtro de área (descartando ruídos com área inferior a 10 pixels) para realizar a contagem final[cite: 1].

---

## 📂 Estrutura de Diretórios

Para que o código no `projeto_pdi_celulas.ipynb` funcione corretamente, a estrutura do diretório deve seguir a seguinte organização[cite: 1]:

```text
/
├── imagens/                         # Diretório contendo as imagens originais (.tif)
│   ├── AS_09125_050118150001_A03f00d0.tif
│   └── ...
├── resultados/                      # Diretório gerado automaticamente para salvar os resultados processados
├── projeto_pdi_celulas.ipynb        # Notebook com a implementação passo a passo e o pipeline em lote
└── README.md
