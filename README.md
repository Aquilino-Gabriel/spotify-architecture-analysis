# spotify-architecture-analysis.

# 🎵 Análise de Arquitetura de Rede e APIs: Spotify Web

Este projeto consiste em um estudo analítico de arquitetura de software e tráfego de rede HTTP, utilizando o player web do **Spotify** como objeto de estudo. O objetivo principal foi mapear o ciclo de vida completo de uma requisição de áudio, inspecionando a comunicação entre Front-end e Back-end.

---

## 🛠️ Tecnologias e Ferramentas Utilizadas

* **Chrome DevTools:** Inspeção e captura do tráfego de rede na aba *Network*.
* **JSON / REST API:** Análise do contrato de dados e carga útil (*payload*).
* **FigJam (Figma):** Modelagem visual e diagramação do fluxograma de rede.
* **HTTP Protocol:** Mapeamento de endpoints, métodos (`POST`) e status codes (`200 OK`).

---

## 📑 Resumo Executivo da Arquitetura

### 1. A Ação no Front-end e a Requisição HTTP
Ao clicar no botão de "Play" na interface web do Spotify, o cliente (browser) captura o evento do usuário e dispara uma requisição assíncrona para a API do sistema. Essa comunicação utiliza o protocolo **HTTP** direcionado ao endpoint de controle de reprodução (`/v1/me/player/play`). Para indicar que se trata de uma instrução que altera o estado do player no servidor, é empregado o método **POST**.

### 2. A Carga Útil (Payload JSON) e o Servidor (Back-end)
Junto a essa requisição, o cliente envia ao servidor um payload no formato **JSON**. A instrução `"debug_source": "resume"` sinaliza a ação de retomar o áudio (se o usuário não tiver dado "Play" antes, a reprodução inicia em 0). A chave `"previous_position": 12506` informa ao servidor o ponto exato em que a faixa foi interrompida (em milissegundos). Por fim, o parâmetro `"seq_num": 9` permite que o servidor compreenda a sequência exata das requisições do usuário, processando as ações na ordem correta sem instabilidades na rede.

### 3. A Confirmação HTTP e o Retorno ao Cliente
Após o processamento no servidor, a API retorna uma resposta contendo o Status Code **200 OK**, confirmando que a operação foi executada com sucesso. Ao receber essa validação em milissegundos, o Front-end fornece o feedback visual instantâneo ao usuário — atualizando o botão de "Play" para "Pause" e avançando a barra de progresso —, ao mesmo tempo em que inicia a execução do áudio nos alto-falantes.

---

## 📊 Fluxograma da Comunicação de Rede

https://www.figma.com/board/XigJGFSSXewdo5ZI4HVJ1I/Back-End-Spotfy?t=YUXLVjOXwETIVvnA-0

---

## 💡 Aprendizados e Reflexão Técnica

Este projeto permitiu consolidar na prática a leitura de tráfego de dados via DevTools, a interpretação de contratos de API em JSON e o entendimento sobre como o Back-end processa requisições sequenciais.
