# 🦦 Capivara no Capibaribe - Interatividade em Canvas 2D

Uma cena interativa 2D desenvolvida com HTML, CSS e a API do Canvas (`CanvasRenderingContext2D`). O projeto retrata uma capivara em estilo *pixel art* passeando pelas margens do Rio Capibaribe, no centro do Recife, com um cenário dinâmico inspirado nos casarões históricos e prédios locais.

## 🎮 Controles e Interatividade

A aplicação é controlada inteiramente pelo teclado. Clique na tela para garantir o foco e utilize as seguintes teclas:

*   **`↑` (Seta para Cima):** Faz a capivara andar para frente (animação de pernas e translação no eixo X).
*   **`E`:** Liga/Desliga o "Andar Automático".
*   **`Q`:** Comer. A capivara abaixa a cabeça, uma comida aparece no chão e a escala da capivara **aumenta**.
*   **`W`:** Fazer cocô. Um cocô é gerado atrás da capivara (e se afasta) e a escala da capivara **diminui**.
*   **`R`:** Reset. Limpa a tela (remove comidas e cocôs), retorna a capivara à posição inicial e reseta sua escala para `1`.

## ⚙️ Conceitos Técnicos Aplicados (Transformações Geométricas)

Este projeto foi construído para demonstrar o domínio absoluto de transformações matriciais no Canvas 2D. Nenhuma imagem ou *sprite* externo foi utilizado; todos os elementos são desenhados via código.

*   **Translação (`ctx.translate`):** Utilizada para mover a capivara globalmente pelo cenário e para calcular a posição exata de geração dos itens (comida/cocô).
*   **Escala (`ctx.scale`):** Aplicada de forma dinâmica ao apertar Q e W. A ancoragem foi rigorosamente calculada para que a capivara cresça e diminua a partir de seus pés, sem flutuar ou afundar no chão.
*   **Rotação com Ponto Fixo (Padrão $T \rightarrow Op \rightarrow T^{-1}$):**
    *   **Pernas:** Rotação pendular ancorada nas articulações (quadril/ombros) usando trigonometria (`Math.sin`) combinada com o loop de tempo.
    *   **Cabeça:** Rotação ancorada na base do pescoço para simular o movimento de descer para comer.
*   **Composição de Transformações:** Combinação em cadeia de translação global da entidade $\times$ escala global $\times$ translação local (membros) $\times$ rotação local.
*   **Gerenciamento de Estado de Matriz:** Uso sistemático de `ctx.save()` e `ctx.restore()` para garantir que as operações de um membro (ex: perna traseira) não interfiram nos demais cálculos do corpo.
*   **Animação:** Loop contínuo otimizado com `requestAnimationFrame` e limpeza de frames com `ctx.clearRect`.

## 🎨 Aspectos Visuais e Responsividade

*   **Estilo Visual:** Design em blocos (*pixel art* estilizado) para casarões coloniais, prédios modernos, margens do rio e para a própria capivara.
*   **Responsividade:** O contêiner do Canvas utiliza `aspect-ratio` e unidades relativas (`vh`, `vw`) no CSS para escalar automaticamente mantendo a proporção `8:5`. A propriedade `image-rendering: pixelated` garante que os gráficos desenhados em blocos permaneçam nítidos em monitores maiores, sem embaçar.

## 🚀 Como Executar

O projeto é de execução estática e não requer instalação de pacotes ou servidores complexos (Zero dependências).

1. Clone ou baixe este repositório.
2. Dê um duplo clique no arquivo `index.html` para abri-lo diretamente em qualquer navegador moderno (Chrome, Edge, Firefox, Safari).
3. *(Opcional)* Se preferir, abra a pasta no VS Code e utilize a extensão *Live Server* para visualização.

---
**Tecnologias utilizadas:** HTML5, CSS3, Vanilla JavaScript.