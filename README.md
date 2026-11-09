# Mission Control Console
O projeto trata-se de um projeto de pré-candidatura para o Rocket Experiment Division (RED), núcleo de estudandes do Instituto Superior Técnico, Universidade de Lisboa, em que consiste na criação de um Mission Control Console (MCC) para a Ground Station do RED. O objetivo é criar o MCC e entregá-lo pronto a encomendar e fabricar.

## Cronograma
- [X] Semana 1: 31 de Outubro a 7 de Novembro
- [ ] Semana 2: 8 de Novembro a 14 de Novembro
- [ ] Semana 3: 15 de Novembro a 21 de Novembro
- [ ] Semana 4: 22 de Novembro a 27 de Novembro

<img width="2177" height="808" alt="timeline" src="https://github.com/user-attachments/assets/c0becd8a-5fde-4bd3-85c6-166e5a1dc2f5" />

## Lista de Tarefas
### Preparação
- [x] Transferir o projeto CAD da caixa
- [x] Criar o documento de planeamento do projeto
- [x] Instalar as aplicações necessárias
- [x] Criar o repositório (https://github.com/CristianPopovici18/MissionControlConsole)

### Arquitetura eletrónica e interfaces
- [X] Criar uma lista de cada funcionalidade a ser implementada
- [X] Criar uma lista dos componentes necessários
- [X] Agrupar componentes em interfaces
- [X] Definir como cada interface funciona e como interage com o microcontrolador
- [X] Definir interface com a GS
- [X] Fazer um orçamento de potência
- [ ] Unir tudo num diagrama de blocos
- [ ] Fazer um diagrama de estados ou tabela de verdade da lógica de armamento
- [ ] Exportar para imagem ou PDF
- [ ] Pedir feedback

### Esquemático elétrico
- [ ] Importar componentes e atribuir footprints no KiCad
- [ ] Criar o esquema para cada interface
- [ ] Unir interfaces à alimentação e ao microcontrolador
- [ ] Unir o MCC com a GS
- [ ] Exportar para PDF
- [ ] Pedir feedback

### Desenho e encaminhamento da PCB
- [ ] Definir dimensões
- [ ] Colocar conectores
- [ ] Organizar por grupos
- [ ] Implementar integração com Raspberry Pi Pico removível
- [ ] Traçar caminhos
- [ ] Exportar arquivo Gerber (para fabricação e entrega), Drill (para perfuração das placas) e STEP (para integração ao CAD)
- [ ] Pedir feedback
- [ ] Reunião de revisão de progresso

### Projeto CAD
- [ ] Criar um esboço do projeto
- [ ] Importar a caixa no SolidWorks
- [ ] Definir dimensões
- [ ] Desenhar as placas, furos, encaixes
- [ ] Importar ou criar componentes
- [ ] Juntar os componentes às placas
- [ ] Juntar as placas à caixa
- [ ] Criar vistas explodidas dimensionadas
- [ ] Exportar arquivo STEP (para entregar) e DXF (para furação)
- [ ] Pedir feedback

### Relatório
- [ ] Definir o esqueleto do relatório
- [ ] Descrever a arquitetura global do MCC, acompanhando com o diagrama de blocos e imagens do PCB e da explosão do CAD
- [ ] Apresentar as principais decisões de conceção e respetiva justificação
- [ ] Apresentar o orçamento de potência
- [ ] Adicionar o diagrama de estados ou a tabela de verdade
- [ ] Explicar como mandar fabricar
- [ ] Explicar como funciona a montagem, acompanhado com um mapeamento das ligações (From-To Table)
- [ ] Apresentar limitações, pressupostos e aspetos que necessitem de validação posterior.
- [ ] Exportar para PDF
- [ ] Pedir feedback

### Entrega
- [ ] Exportar tudo o que é pedido, unir numa pasta e zipar
- [ ] Verificar tudo uma última vez
- [ ] Entregar o projeto


## Arquitetura eletrónica e interfaces
### Componentes do painel, funcionamento e integração
| Componentes do Painel            | Funcionalidade                                                            | Integração                                                                                                                      | Componentes                                         |
| -------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| Deadman Switch                   | Identifica se a pessoa a controlar o MCC está na capacidade de o manusear | Bloqueia o armamento se estiver OFF                                                                                             | Interruptor Dead Man Switch                         |
| 3 Funções (Launch, Vent e Abort) | Indicação, armamento e execução da função                                 | O LED identifica o estado da armação, o interruptor ativa ou desativa a armação e o botão que executa a ação ao ser pressionado | LEDs                                                |
| Indicadores gerais               | Indicam se a MCC está ligado                                              | LED vermelho para Power, LED verde para Comms                                                                                   | LEDs                                                |
| Interfaces externas              | Ligação à energia e à comunicação com a GS                                | Ligação à energia através da entrada Jack DC e à comunicação com a GS através do connector micro-usb                            | Conector micro-usb, Entrada de alimentação Jack DC. |
| Logótipo do RED                  | Identidade visual                                                         | Representa a equipa                                                                                                             | Autocolante                                         |

### Lista preliminar de componentes
| Componente                           | Referência |
| ------------------------------------ | ---------- |
| Interruptor Dead Man Switch          | 010-0109   |
| Interruptor ON-OFF com indicador LED | 010-0385   |
| Capa Interruptor Alavanca - Vermelha | 010-0314   |
| Botão de Pressão OFF-(ON) Azul       | 010-0333   |
| Botão de Pressão OFF-(ON) Vermelho   | 010-0337   |
| Botão de Pressão OFF-(ON) Amarelo    | 010-0339   |
| Botão de Pressão OFF-(ON) Verde      | 010-0334   |
| Interruptor de Chave                 | 010-0443   |
| LED 29 mm M22 - Branco               | 017-1313   |
| LED 29 mm M22 - Vermelho             | 017-1312   |
| LED 29 mm M22 - Verde                | 017-1311   |
| LED 29 mm M22 - Azul                 | 017-1314   |
| Conjunto de LEDs de 5 mm             | 004-1797   |
| Raspberry Pi Pico baseado no RP2040  | 095-0596   |
| Cabo Micro-USB                       | 047-2625   |
| Conector Jack DC                     | 011-0512   |
| Regulador Buck TPS56837HRPAR         | 001-3847   |
| Conectores Molex de 4 pinos          | 43045-0408 |
| Conectores Molex de 2 pinos          | 43045-0206 |

### Interfaces e a sua integração com o microcontrolador
| Interface   | Função                                                                                                      | Componentes                                                          |
| ----------- | ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| Alimentação | Gerir a alimentação do circuito, tanto a entrada de alimentação, potenciais conversões e ligação do MCC     | Conector Jack DC, Regulador Buck TPS56837HRPAR, Interruptor de Chave |
| Controlo    | Gerir o encaixe do microcontrlolador e a integração da GS e das restantes interfaces com o microcontrolador | Conector Micro-USB, Raspberry Pi Pico                                |
| Ativação    | Gerir o armamento e a ativação das funções (Launch, Vent e Abort)                                           | Dead Man Switch, Capa Interruptor Alavanca, Botões de Pressão        |
| Indicação   | Indicar os estados de armamemnto, das funções, de Power, de Comms e estados adicionais                      | LEDs                                                                 |

| Interface   | Integreção com o microcontrolador                           |
| ----------- | ----------------------------------------------------------- |
| Alimentação | Fornece alimentação ao microcontrolador                     |
| Controlo    | Fornece encaixe ao microcontrolador                         |
| Ativação    | Comunica a ativação de alguma função ao microcontrolador    |
| Indicação   | Ativa ou desativa LEDs, consoante o microcontrolador mandar |

### Orçamento de Potência
| Componente                          | Quantidade | Tensão      | Tipo | Corrente Unitária | Corrente Total | Potẽncia        |
| ----------------------------------- | ---------- | ----------- | ---- | ----------------- | -------------- | --------------- |
| LED 29 mm M22                       | 6          | 24V         | DC   | 20mA              | 120mA          | 2.88W           |
| LED Vermelho e Amarelo 5mm          | 2          | 3.0V - 3.2V | DC   | 20mA              | 40mA           | 0.12W - 0.128W  |
| LED Verde 5mm                       | 1          | 1.8V - 2.2V | DC   | 20mA              | 20mA           | 0.036W - 0.044W |
| Raspberry Pi Pico baseado no RP2040 | 1          | 5V          | DC   | 50mA              | 50mA           | 0.25W           |
| Regulador Buck TPS56837HRPAR        | 1          | 3.5V - 60V  | DC   | 1.5A              | 1.5A           | 5.25W - 90W     |
