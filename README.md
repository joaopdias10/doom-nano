# Switch-Ino — Console Emulador de Doom em Arduino

Console portátil que roda uma versão reduzida de **Doom** em um Arduino
(ATmega328P). O projeto foi desenvolvido como trabalho prático da disciplina
de **Sistemas Embarcados** do curso de Engenharia de Computação da
**UTFPR – Campus Toledo (2025)**, atendendo aos requisitos de construção de
uma PCB própria, uso de pelo menos dois periféricos e implementação de uma
interface homem-máquina (IHM).

> O motor de renderização (raycasting) usado no jogo é o **doom-nano**, escrito
> em C++ por [daveruiz](https://github.com/daveruiz/doom-nano). Este repositório
> parte desse motor e o adapta para o hardware do console Switch-Ino.

---

## O que foi feito

A partir do motor doom-nano original, montamos e validamos o jogo em protoboard
e, em seguida, projetamos e fabricamos uma **PCB personalizada** que funciona
como um *shield*: ela se encaixa diretamente sobre o Arduino e passa a servir
como a própria estrutura física do console, dispensando uma carcaça.

Principais atividades do projeto:

- **Montagem e validação em protoboard** do jogo com o display OLED e botões
  temporários, confirmando o funcionamento antes de partir para a placa
  definitiva.
- **Projeto da PCB no EasyEDA**: montagem do circuito elétrico, geração da placa
  pela ferramenta do software e roteamento/aterramento manual das trilhas.
- **Fabricação da placa** a partir do Gerber, usinada em CNC no laboratório,
  seguida do acabamento manual (lixamento das bordas, furação, aplicação de
  Bombril nas trilhas e soldagem dos componentes).
- **Integração dos periféricos e da IHM**: display OLED como saída gráfica e
  quatro botões para o controle do jogador.
- **Otimização do código C++** para caber na memória do microcontrolador,
  removendo funções não essenciais e mantendo uma resolução reduzida para
  preservar o FPS.
- **Reforço mecânico da montagem**: soldagem reforçada dos pinos do Arduino
  (ilhas reforçadas, solda extra e ordem de soldagem controlada) para manter o
  Arduino firme e alinhado sobre a placa.

O módulo **Bluetooth** chegou a ser previsto no planejamento, mas foi descartado
na versão final, já que os botões integrados ao console se mostraram mais
adequados ao uso.

## Como se joga

O jogo mantém a estrutura básica do gameplay original dentro das limitações do
Arduino. Os quatro botões controlam:

- **Andar para frente**
- **Virar para a esquerda**
- **Virar para a direita**
- **Atirar**

## Telas do jogo

![Doom rodando no Switch-Ino](/images/screen-4.jpg?raw=true)
![Doom rodando no Switch-Ino](/images/screen-5.jpg?raw=true)
![Doom rodando no Switch-Ino](/images/screen-6.jpg?raw=true)

## Hardware

| Componente | Função |
| --- | --- |
| Arduino (ATmega328P) | Processamento, lógica do jogo e leitura dos controles |
| Display OLED I²C 128×64 | Saída gráfica |
| 4 botões | IHM / controle do jogador |
| PCB personalizada (shield) | Estrutura física e interligação dos componentes |
| Fonte de 9 V | Alimentação externa |
| Buzzer | Som (opcional — suportado pelo código) |

### Custo aproximado

Cerca de **R$ 210 – 250** no total (Arduino, display, botões, alto-falante,
PCB e itens extras).

## A PCB

A placa foi desenhada no EasyEDA no formato de *shield* para o Arduino. As
imagens abaixo mostram a placa finalizada; o arquivo com o desenho da PCB
exportado está em `images/PCB_PCB_SW-ino_2_2025-11-18.pdf`.

![PCB — frente](/images/PCB.jpeg?raw=true)
![PCB — verso](/images/PCB%20Verso.jpeg?raw=true)

## Documentação

O relatório técnico completo do projeto está em
[`images/Relatório Doom.pdf`](images/Relat%C3%B3rio%20Doom.pdf).

## Melhorias futuras

- Botão dedicado para andar para trás.
- Ativação do sistema de som (já presente no código original).
- Case para acabamento estético.

## Créditos

- Motor de raycasting **doom-nano** — [daveruiz](https://github.com/daveruiz/doom-nano)
- Versão enxuta da biblioteca SSD1306 e suporte a som —
  [@miracoly](https://github.com/miracoli)
- Sprites de https://www.spriters-resource.com
- Referência sobre raycasting: https://lodev.org/cgtutor

> **Observação:** este não é o Doom original. Trata-se de um motor de
> renderização no estilo Wolfenstein 3D com alguns sprites inspirados em Doom,
> bastante simplificado para rodar no Arduino.
