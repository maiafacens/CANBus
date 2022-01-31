# CAN-Bus



### **<p align="center">Experimentos realizados para familiarização com STM32</p>**

A primeira coisa e a mais importante de se fazer para um bom funcionamento do projeto é  configurar o Hardware do STM32 corretamente, utilizando a interface de configuração do STM32CubeIDE é possível configurar como desejado pelo usuário as diversas funções disponíveis no STM32 como, configuração de clock, especificação dos pinos( entradas ou saidas analogicas ou digitais, interrupção, temporizadores para PWM e diversas outras funções que os diferentes pinos podem oferecer todas dependendo da vontade do usuário), diversas formas de conectividade podem ser também utilizadas pelo STM32 como rede CAN Bus, I2C, SPI, USART e USB.  


### **<p align="center">Configurações de clock</p>**

Primeiramente, ao abrir a interface deve-se habilitar os clocks (Crystal/Ceramics), o tipo de clock disponível pode variar pela placa ou meio de conexão para programação do STM32.

<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150535416-57c228de-d041-432f-931d-2acdf48837a9.png" width="500px" />
</div>
<br>

A seguir é necessário configurar a frequência do Clock, o mais normalizado é colocar na potência máxima de clock disponível.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150541020-3c605c91-18cf-4a31-9430-ac15ef5ca7e9.png" width="500px" />
</div>
<br>

Após isso já é possível configurar os ports que serão utilizados, algumas funções podem ser ativadas diretamente nos pinos da simulação, outras podem ser ativadas pelo menu lateral à esquerda, porém toda a parte de como serão configurados os pinos e funções que serão utilizadas no STM são feitas no menu lateral.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150544689-392aefb0-9336-41b6-94c9-73dff8cb5401.png" width="200px" />
</div>
<br>

### **<p align="center">Flash LED</p>**

Para o projeto de piscar LED primeiro é necessário configurar um pino de saída GPIO para programação de piscar o LED.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150545544-bc5541c3-cca6-42a4-add1-47e539eab94c.png" width="500px" />
</div>
<br>

É possível alterar a identificação dado aquele pino inserindo uma LABEL na Aba GPIO de System Core no menu lateral.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150546107-a4743ad2-f8e6-4ed5-b940-7fb1ad414f30.png" width="500px" />
</div>
<br>

Após finalizar as configurações necessárias na interface do STM, só é necessário salvar o projeto que todos os arquivos incluindo o main.c sejam gerados pelo software.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150553611-31464060-147e-485f-a9fb-2b3ff58f5035.png" width="700px" />
</div>
<br>

A programação para piscar o LED é relativamente simples, partindo das configurações já realizadas na placa.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150555236-df006290-720d-44dc-a2de-a489a7e2aabd.png" width="400px" />
</div>
<br>

Dentro do loop while, são necessárias somente duas linha de código, TogglePin faz com que a saída especificada alterne entre ligado (1) e desligado (0) enquanto Delay faz com que seja necessário esperar um tempo antes de continuar a programação, o tempo inserido deve ser em milissegundos, nesse caso depois do delay o loop reinicia executando a programação novamente, cada vez alternando o estado do pino e aguardando o Delay, fazendo com que o pino do STM 32 alterne o estado, conectando o pino a um LED e o LED ao GND, fará com que o LED pisque de acordo com a programação. 

Pasta com os arquivos do [FlashLed](https://github.com/maiafacens/FlashLed) ou acesso direto ao [main.c](https://github.com/maiafacens/FlashLed/blob/master/Core/Src/main.c)


### **<p align="center">Botão LED</p>**

O programa botão LED não é complexo, após configuração do STM32 do pino C13 como entrada GPIO e do pino A5 como saída GPIO.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150557032-0d56e5f5-8dc2-42dc-8ad6-f0f9b016ac94.png" width="308px" />
<img src="https://user-images.githubusercontent.com/68281710/150557256-9d6415ab-7fce-40a0-8489-5c158ee24779.png" width="300px" />
</div>
<br>
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150557871-84861a94-9f47-474d-ab9d-ade22a19d481.jpg" width="500px" />
</div>
<br>

A programação é relativamente simples. 
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150562365-9268f4cc-a106-43aa-ae41-6b0de76ea518.png" width="500px" />
</div>
<br>

A condição para o if é de que, caso o botão (que deve ser montado conectado no pino C13) seja acionado assim enviando sinal alto para o pino, a função WritePin vai mandar sinal de RESET para o pino do LED fazendo com que enquanto o botão permanecer sendo pressionado a saída do pino A5 conexão do LED ficará com sinal lógico baixo, em qualquer outra condição em que o botão não esteja pressionado o programa segue para o else no qual a função TogglePin seguida de um Delay faz com que o pino de saída A5 alterne seu estado assim piscando o LED baseado no tempo do delay.

Pasta com os arquivos do [BotaoLed](https://github.com/maiafacens/BotaoLed) ou acesso direto ao [main.c](https://github.com/maiafacens/BotaoLed/blob/master/Core/Src/main.c)


### **<p align="center">Single Serial</p>**

Neste projeto foi utilizado um conector FTDI como conversor USB serial para conectar o STM32 ao computador e assim estabelecer uma comunicação entre o STM e um terminal serial.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150569121-51870170-46b9-432a-81f3-e3b153767183.jpg" width="500px" />
</div>
<br>
  
Foram realizadas as configurações no STM para serem utilizados 2 botões como entradas de GPIO Port e 4 LEDs como saídas e ativar as funções de conectividade utilizando FTDI para comunicação USB com o  UART para serem utilizadas para comunicação Serial com o terminal.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150569300-e946380d-7112-43e9-b943-8244c441eed0.jpg" width="395px" />
<img src="https://user-images.githubusercontent.com/68281710/150569504-9845534c-1858-4c40-ba1c-20c1822e0721.png" width="350px" />
</div>
<br>

Explicando a primeira parte da programação, o primeiro passo foi criar vetores de string para servirem como armazenamento das informações a serem transmitidas entre o STM e o computador. 
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150569935-26cedc06-0d79-4f25-82d1-9dbfe6ae1037.png" width="500px" />
</div>
<br>

O HAL_UART_Receive recebe no STM o sinal dos botões conectados às entradas, para depois enviar a informação coletada para o monitor Serial, caso o Vetor DadoRx receba alguma informação vinda do monitor serial que está sendo utilizado no computador a condição do if é atendida, assim submetendo a string recebida ao switch case da programação, a condição para entrar em cada case é um número e cada case está relacionado a um LED de cor diferente, se a informação recebida for um dos casos especificados, o pino em questão será submetido a um Toggle Pin assim alternando o estado do LED, seguindo com uma linha que zera a string para aguardar o próximo dado a ser recebido e  o break fecha o case.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150570077-de84aac0-5feb-44c0-ba3f-a98a9de6c26a.png" width="500px" />
</div>
<br>

Logo após o if e o switch case é feita a montagem da tela utilizando um sprintf, todos as informações contidas no sprintf estão sendo alocadas no vetor DadoTX logo no início, depois é feito a montagem do texto que vai ser exibido na tela como estado dos LEDs e dos botões, e por último no sprintf os %d são associados com o correspondente GPIO Read Pin que verifica o estado do pino especificado assim exibindo o estado atual dos LEDs e dos botões que estão conectados nos pinos, e para finalizar enviando as informações a  função HAL_UART_Transmit envia do STM os dados armazenados no vetor da string DadoTX via FTDI USB para ser exibido via terminal serial no computador, os estados dos LEDs baseados nos dados que estão sendo recebidos pelo STM pelo serial como dos botões.

Pasta com os arquivos do [SingleSerial](https://github.com/maiafacens/SingleSerial) ou acesso direto ao [main.c](https://github.com/maiafacens/SingleSerial/blob/master/Core/Src/main.c)


### **<p align="center">CAN entre dois dispositivos</p>**

Este projeto utiliza de dois STM32F103C8 para realizar comunicação de protocolo CAN Bus entre si, a programação de cada um foi feita separadamente sendo que um dos STM foi utilizada uma função de interrupção externa em conjunto com a comunicação CAN para justamente ser o sinal para iniciar a comunicação, primeiramente configurar o STM no MX.

<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150570846-11529054-d09e-4d30-91a6-84532e559215.jpg" width="500px" />
<img src="https://user-images.githubusercontent.com/68281710/150570954-17e6c908-496d-4ae7-a99f-f572702dc529.png" width="300px" />
</div>
<br>

Na configuração do STM é preciso habilitar o modo de conexão CAN, e especificar algumas informações importantes para a programação e um funcionamento corretos do módulo CAN, primeiramente habilitar a conexão de CAN e padronizar o baud, pois o Baud de todos os módulos conectados na rede CAN devem ser iguais para ser possível a comunicação e depois de especificar o Baud é preciso setar qual canal FIFO será utilizado (entre RX0 e RX1) , pois na programação é necessário manter o mesmo canal.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150571554-3b46e4f9-8642-45ce-9570-aa006a6a6897.png" width="400px" />
</div>
<br>

O pino C13 declarado como saída para servir como ativação do LED onboard presente no STM32F103C8 e o pino A2 no modo de interrupção externa, a interrupção faz com que os processos ocorrendo na programação do STM sejam pausados para executar a ação dita pela interrupção, um botão será conectado no pino A2 para executar a interrupção.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150572029-2f416f4d-50ce-440a-b458-f36e0d6b0a44.png" width="300px" />
</div>
<br>

Tendo feitas as configurações, já é possível iniciar a programação setando as primeiras partes da CAN e a parte da interrupção.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150572180-85af1c70-1736-44cf-a47d-600c9a800f6a.png" width="250px" />
</div>
<br>


Configurar o Handle Type Def da CAN, definir os Reader's de TX e RX, criar os vetores para as mensagens de TX e RX para recebimento e envio, e o vetor de string para armazenar as string a serem enviadas no TX, a variavel datacheck criada como uma flag para checar se uma mensagem foi recebida no RX, depois dessas primeiras configurações é programado a função de interrupção para o botão nessa interrupção a mensagem será montada e enviada pelo TX, e a função de recebimento de mensagens do CAN, importante lembrar o canal configurado para o FIFO(RX0 ou RX1).
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150572601-e6be8484-ec52-4a4a-bbf6-01f87f608127.png" width="400px" />
</div>
<br>

A função de interrupção impõe que quando o pino especificado na condição da função receber uma interrupção externa os valores pré-programados e setados dentro da função serão inseridos nos espaços 0 e 1 do vetor TxData e a função AddTxMessage irá realizar o envio desses dados.

A função de recebimento de mensagem também age um tanto como uma interrupção, quando dados são recebidos no canal RX da rede CAN, eles são analisados e depois armazenados no vetor RxData, uma condição verifica o tamanho da mensagem recebida ( indicado pelo DLC recebido na mensagem) e condizente com o tamanho de mensagem esperado a flag datacheck é ativada.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150573189-d7c2550a-69ab-42c0-9af6-280b63d2676a.png" width="450px" />
</div>
<br>

Já dentro da função main é necessário iniciar a função CAN com o HAL_CAN_Start e ativar as notificações, a ativação de notificação está relacionada com o FIFO e o recebimento de mensagens declaradas antes.

É necessário parametrizar as mensagens de TX, como serão feitos os envios das mensagens, cada mensagem pode conter até 8 bytes o DLC faz a definição de quantos Bytes serão enviados na mensagem, essa quantidade definida será a quantidade enviada independente dos dados presentes nos bytes do vetor, é necessário definir o ID e o tipo de ID da mensagem, a rede CAN conta com dois tipos de ID, o Standard (padrão) CAN_STD_ID e o Extended (estendido), em conjunto com o tipo do ID graças ao método de funcionamento da rede CAN vários dispositivos podem estar conectados e comunicarem entre si numa rede CAN, para uma comunicação funcional entre por exemplo dois dispositivos cada dispositivo deve ter seu próprio ID, por isso é necessário definir um ID para cada STM do projeto, para parametrização do TX também é preciso definir o RTR, para definir o tipo de frame em que a mensagem será enviada, o padrão seria o CAN_RTR_DATA.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150573579-b0d94193-81c3-4bbb-89d1-195b6a05bb3b.png" width="390px" />
</div>
<br>

Para demonstração da comunicação entre os dois STM, um LED irá piscar indicando que uma mensagem foi recebida pelo RX da rede CAN, isso será feito através de um loop for com a função Toggle Pin no pino C13 do LED onboard do STM32F103, esse for só será iniciado quando a condição do if for atendida, isso será quando a flag datacheck for alterada para 1 na função de recebimento de mensagens HAL_CAN_RxFifo0MsgPendingCallback.

O seguinte passo será declarar e configurar os filtros da rede CAN para recebimento e envio de mensagens. 
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150576471-4b4740ed-1927-4b1b-98b7-16e8a51059e7.png" width="500px" />
</div>
<br>

Primeiro FilterTypeDef indica qual será o termo usado nas definições dos filtros, nesse caso foi utilizado canfilterconfig mas isso pode ser definido a livre escolha, após isso se inicia a definição dos parâmetros dos filtros, FilterActivation para habilitar ou desabilitar a ativação dos filtros, FilterBank define qual dos bancos de filtro será utilizado o módulo CAN do STM32F103 contém 14 bancos de filtros, então o valor inserido precisa estar entre 0 e 13, FilterFIFOAssignment precisa do FIFO que esta sendo utilizado para comunicação (FIFO0 para RX0 e FIFO1 para RX1), as seções FilterId são justamente um dos propósitos mais importantes dos filtros pois isso irá indicar IDs específicos para comunicação na rede CAN, como vários dispositivos podem estar conectados juntos e comunicando entre si nos barramentos de CANH e CANL os IDs servem como identificação para cada dispositivo e so filtros verificam os IDs comunicando e selecionam as mensagens do ID que for especificado caso o valor indicado seja 0 os filtros vão aceitar mensagens de qualquer ID, a função SlaveStartFilterBank é para controladores que contenham mais de um módulo CAN o que não é o caso do STM32F103C8 utilizado no projeto.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150574822-6deb1820-5c4f-4e0e-a772-5f5fe78955bf.png" width="500px" />
</div>
<br>

Partindo para o segundo STM as parametrizações e programação do código não fogem de como foi feito no primeiro, na parte de configuração dos pinos e conexões no MX a única diferença é que não será preciso um pino para um botão, mas sempre ficar atento com configuração de clock, FIFO (determinar qual RX sera utilizado FIFO0 para RX0 e FIFO1 para RX1)  e o Baud (Para estabelescer a comunicação entre os dispositivos o valor do Baud deve ser igual).
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150575344-2a71c696-4db2-464c-ab43-b3fd46932936.png" width="400px" />
</div>
<br>

Na parte da programação não muda muita coisa, declarar as funções e variáveis necessárias para o funcionamento da rede CAN como no primeiro STM, atenção ao detalhe do FIFO novamente, no primeiro havia sido utilizado RX0 portanto FIFO0, nesse caso será utilizado RX1 portanto FIFO1, porém vale reinterar que a escolha do RX para o FIFO é opcional ambos podem ser RX0 ou RX1.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150575633-1298daaf-85c2-494f-871a-16b6113fce3b.png" width="400px" />
</div>
<br>

Inicialização da função main, iniciar a rede CAN a função de notificações, e como não tem a função de callback do botão como no primeiro  STM os dados são inseridos no vetor de envio da mensagem aqui para depois ser enviada, um fator muito importante novamente é a declaração do ID este será o ID que deverá ser inserido nos filtros do primeiro STM e o ID no primeiro deverá ser inserido nos filtros desse segundo STM.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150574256-dbe99636-c5bf-4967-a0bf-48ca1e6b1cb4.png" width="500px" />
</div>
<br>

E por último o loop while da função main do segundo STM.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150576314-d1e3e9c9-5ee2-492f-a5f4-fa254f81378f.png" width="500px" />
</div>
<br>

Quando a flag datacheck for alterada para 1 na função de recebimento de mensagens HAL_CAN_RxFifo1MsgPendingCallback a condição vai ser verdadeira, entrando em um for similar ao do primeiro onde o LED irá piscar indicando que uma mensagem foi recebida pelo RX da rede CAN, isso será feito através de um loop for com a função Toggle Pin no pino C13 do LED onboard do STM32F103, saindo do for a flag é zerada para esperar uma nova mensagem ser recebida e uma mensagem com os dados que haviam sido gravados anteriormente é enviada para o outro STM.

Assim o funcionamento principal do código será então, quando o botão de interrupção do STM Master for acionado assim ativando a interrupção e enviando uma mensagem pelo TX para o outro STM, quando o segundo STM receber a mensagem será ativada um flag datacheck entrando na condição do main e piscando o LED de acordo com o loop for, saindo do loop o STM secundário envia de volta uma mensagem para o STM Master, que passará pelo mesmo processo da flag, entrar na condição, loop for piscando o LED, encerrando dessa forma e acionando novamente essa sequência quando é reconhecida uma interrupção no pino do STM Master.

Pasta com os arquivos do [Master](https://github.com/maiafacens/TUT_CAN_MASTER) ou acesso direto ao [main.c](https://github.com/maiafacens/TUT_CAN_MASTER/blob/master/Core/Src/main.c)

Pasta com os arquivos do [Slave](https://github.com/maiafacens/TUT_CAN_F103) ou acesso direto ao [main.c](https://github.com/maiafacens/TUT_CAN_F103/blob/master/Core/Src/main.c)


### **<p align="center">ADC e PWM</p>**

O projeto do PWM foi desenvolvido como uma aplicação da comunicação CAN entre dois dispositivos com mais etapas, e mais processos, o procedimento da parte da rede CAN é o mesmo configuração inicial, parametrização da mensagem de envio e definição dos filtros. o que será diferente e detalhado a seguir serão duas funções novas, cada um inserida em um dos dois STM32 que serão utilizados no projeto, o primeiro STM terá uma função de Conversor Analogio Digital (ADC) que lerá o valor de um potenciômetro e vai gravar o valor num vetor para ser enviado como uma mensagem pela rede CAN para o segundo STM que vai utilizar uma função de PWM para passar o sinal recebido pela CAN no formato de onda a saída do PWM pode ser conectada a um osciloscópio para visualização.

#### Montagem do projeto no Proteus e protoboard
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150583126-e4ca1043-2778-4272-8b12-ea9403952982.jpg" width="600px" />
<img src="https://user-images.githubusercontent.com/68281710/150583207-4f42484e-b603-4d5f-bbce-7e1c915c1c4e.jpg" width="500px" />
</div>
<br>

Primeiro o STM32 que utilizará o ADC, um pino deve ser definido como entrada analógica e deve ser configurado, selecionar um ADC e o canal daquele ADC será utilizado, neste exemplo foi-se ativado também a modo de conversão contínua.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150584428-73ef8e0d-e07c-469b-883d-dacaf522d02c.png" width="500px" />
</div>
<br>

A parte da programação do ADC não é muito complicada.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150584869-c74b0775-3a63-46c2-ae15-297bb14ba373.png" width="400px" />
</div>
<br>

Realizar a configuração da CAN para comunicação entre os dois STMs e declarar as variáveis necessárias como o datacheck para verificação do recebimento de mensagens e uma variável tick para contagem de intervalos de tempo com a função HAL_GetTick utilizada posteriormente.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150586169-739de27f-e571-4a8f-9ca2-581090d185d1.png" width="400px" />
</div>
<br>

Após o start da função de ADC, dentro do while a função HAL_ADC_PollForConversion verifica os dados a serem lidos e a função HAL_ADC_GetValue vai coletar o valor atual recebido no pino e gravar na variável intermediária, o valor da variável então é gravado no vetor TxData e os dados de TxData são enviados pela rede CAN, como não existe algo que irá iniciar as comunicações ambas as partes irão comunicar entre si constantemente e como forma de verificar se as comunicações estão funcionando uma condição foi programada, caso o controlador receba uma mensagem pelo RX e a mensagem recebida seja a esperada uma função togglepin vai alterar o estado do LED onboard da placa de ligado para desligado a cada 500 milissegundo. 
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150586344-45ed6815-48db-47f8-9a82-3c23651b5e3c.png" width="400px" />
</div>
<br>

Para o correto funcionamento do projeto é preciso configurar corretamente o sistema de mensagens de rede CAN e as funções utilizadas na programação como o HAL_GetTick  que deve ser igualado a variável de controle tick antes do início do loop while.

Em relação ao STM com a função PWM a programação e parametrização dele também é relativamente simples após todas as questões relacionadas a CAN serem configuradas e definidas, primeiramente é necessário habilitar o timer com o PWM, selecionar qual timer será utilizado, qual canal do timer será ativado e configurar o prescaler e o counter period do timer após finalizadas essas configurações já é possível iniciar a programação.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150586703-b794ae67-0e54-45f4-90c6-8c314c6758a7.png" width="400px" />
</div>
<br>

O código da parte do PWM é bem simples o mais complexo realmente é a parametrização da rede CAN, agora o PWM após gerado código só precisa de algumas configurações, a função __HAL_TIM_SET_COMPARE prepara os dados recebidos no RX para o timer do PWM e o HAL_TIM_PWM_Start inicia a transmissão do PWM para a saída do Pino, a condição de recebimento de mensagem acionada pela flag manda de volta uma mensagem ao outro STM o que ativa a condição de piscar o LED no STM com o ADC conectando o ground do osciloscópio ao GND do STM e a entrada de Sinal ao pino da placa é possível observar a onda gerada pela variação do sinal do potenciômetro.

#### Programação do PWM
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150587791-52eb8087-3ed1-4ac3-8d9b-6759675ba97c.png" width="450px" />
</div>
<br>

#### Leitura da saída PWM no osciloscópio com potênciometro no máximo (esquerda) e no mínimo (direita).
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150588017-482a99ca-a341-4727-b7ef-e14932814d34.jpg" width="400px" />
<img src="https://user-images.githubusercontent.com/68281710/150588093-a032cdd5-af65-4010-bf9b-4d1119e45bcb.jpg" width="400px" />
</div>
<br>

Pasta com os arquivos do [PWM](https://github.com/maiafacens/PWM) ou acesso direto ao [main.c](https://github.com/maiafacens/PWM/blob/master/Core/Src/main.c)

Pasta com os arquivos do [ADC](https://github.com/maiafacens/ADC-do-PWM) ou acesso direto ao [main.c](https://github.com/maiafacens/ADC-do-PWM/blob/master/Core/Src/main.c)

### **<p align="center">Lora e ADC</p>**


O objetivo deste projeto visa estabelecer e transmitir dados por módulos de comunicação Lora, o principal é realizar as conexões corretamente, será usando modo UART para comunicar os dados com os módulos de Lora, dois STM32F103C8 fazem as comunicações um servindo como transmissor utilizando os dados coletados de uma port ADC conectada a um transistor, tratando esses dados e enviando para o módulo Lora por UART, enquanto o segundo recebe os dados por essa mesma conexão modulo Lora para UART com várias conexões para testar os dados recebidos em um sistema de LEDs.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150803537-d6c64fed-80a8-47a6-b870-8d1d7faf45d8.png" width="600px" />
</div>
<br>

As configurações iniciais devem ser realizadas nos dois STMs da parte de clock e debug por conexão serial, em relação ao primeiro STM ele deve ser configurado para leitura do transistor programando a port ADC desejada nesse caso foi utilizado o port B1 programando ADC1 no IN9, importante também para o ADC é que deve ser habilitada a configuração de modo de conversão contínua, também deve ser configurado o UART para comunicação e um ponto muito importante é definir o Baud Rate para comunicação pois o UART do outro STM deve ser igual.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150803221-57ddd437-3440-49d1-8881-6ed0842a8841.png" width="250px" />
</div>
<br>

O módulo Lora pode ser alimentado pelo 3V3 do próprio STM, TX e RX do módulo Lora devem ser conectados as Ports A10 e A9 responsáveis pela transmissão e envio de dados UART.

Em relação ao segundo STM suas configurações iniciais e a parte de UART podem ser feitas iguais ao primeiro STM, importante ressaltar que o Baud Rate para o UART deve ser realmente igual, para o sistema de LEDs para a verificação dos dados recebidos, somente é necessário configurar 5 GPIO Ports como saídas para conexão com LEDs.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150803911-4e27650d-1c3c-489e-9931-d5f7592af4ea.png" width="650px" />
</div>
<br>

Na programação do primeiro STM primeiramente devem ser criadas duas variáveis: uma para coletar o valor do transistor e outra para servir como vetor para armazenamento e envio de dados pelo Lora,  após isso iniciar o sistema de leitura e conversão de porta analógica, o ADC.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150804234-0db4e2bc-7508-4ef3-87a3-67a746d42073.png" width="200px" />
</div>
<br>
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150804381-1c2f5b22-35bc-4550-87ec-18c34dce8bc6.png" width="500px" />
</div>
<br>

A programação do Loop é relativamente simples o valor coletado será armazenado na primeira Variável, depois tratado e armazenado no vetor charToTransmit para então o caractere armazenado ser enviado pelo UART via Lora para o outro STM.

O segundo STM deve ter uma variável para armazenamento dos dados recebidos via Lora.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150804501-adfb40b6-4d71-43fc-a5e1-bd66eec92a95.png" width="200px" />
</div>
<br>

A partir do caractere recebido a programação irá acionar uma das saídas GPIO assim acionando um dos 5 LEDs diferentes a partir do valor atual retirado do transistor pelo primeiro STM. 
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150804893-a6e046b3-b2ac-45e1-8646-a902faa53f59.png" width="317px" />
<img src="https://user-images.githubusercontent.com/68281710/150804975-4f4bc737-6814-4d6f-91d5-df442fa618c9.png" width="298px" />
</div>
<br>

### **<p align="center">CAN e UART Master</p>**
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150805858-0481b54b-45ea-4aea-aeee-95afc159cd5f.png" width="400px" />
</div>
<br>

Para programação do STM master para uso de CAN com UART, primeiramente os pinos devem ser configurados corretamente, o clock deve ser habilitado e configurado de acordo com a preferência (configuração usual para o clock seria inserir os valores no máximo).
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150806096-d800f38f-df62-410d-88f8-da37e9aad645.png" width="250px" />
</div>
<br>

Na sessão de conectividade é necessário habilitar a comunicação CAN e o Canal USART desejado e no modo desejado (para esse projeto o canal USART será configurado no modo assíncrono), assim como ter atenção para configuração de interrupções e Baud tanto de CAN quanto da USART, um detalhe opcional mas que foi implementado para o o projeto é o pino C13 associado ao LED onboard.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150806497-aa982757-6ec4-4e7f-b361-b46eec1d7104.jpg" width="400px" />
</div>
<br>

#### Configurações da CAN
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150806804-072c9871-2ec4-4675-b066-eec2c3bcceb6.png" width="450px" />
<img src="https://user-images.githubusercontent.com/68281710/150806984-58b80d89-67ca-4beb-855a-a546ade31800.png" width="520px" />
</div>
<br>

#### Configurações USART
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150807576-f8bb5c89-ebeb-4922-b3fa-2e4060e4648f.png" width="500px" />
<img src="https://user-images.githubusercontent.com/68281710/150807859-fffc91a6-9ad4-41ce-87df-37038a84c8f1.png" width="550px" />
</div>
<br>

#### Programação
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150808706-43e9683e-95d2-440b-b0d7-1ef7e0869e6e.png" width="300px" />
</div>
<br>

Verificar a declaração do CAN_HandleTypeDef e realizar a declaração de variáveis e função de recebimento de mensagens da rede CAN.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150808965-0f533b61-99c6-4392-9d40-7ef2ed9e8e6f.png" width="400px" />
</div>
<br>

A declaração de variáveis é importante para o correto funcionamento do projeto, os vetores são de suma importância para o envio e recebimento das comunicações, tanto via CAN quanto via UART, dentro do recebimento de mensagens uma condição é programada para somente identificar uma mensagem como apropriada se estiver com o ID especificado na condição, caso a condição esteja correta o valor do ID (que deve ser pré-programado), será salvo em um vetor e datacheck será alterado para 1, para acionar a condição de datacheck no loop while.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150809499-f262bba3-e31d-497f-9aeb-4912574e34c1.png" width="400px" />
</div>
<br>

Inicialização de todos os periféricos configurados, GPIO para o pino correspondente ao LED, comunicação CAN e as portas de comunicação UART, HAL_CAN_Start(&hcan) inicia os processos internos associados a CAN assim o STM estara pronto para interpretar os comandos e funções associados a rede CAN que forem programados.

HAL_CAN_ActivateNotification é necessário para ativar o sistema de notificações no STM para o recebimento de comunicações da rede CAN, enquanto as funções de TxHeader são de suma importância para a montagem das mensagens a serem transmitidas pela mesma.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150810116-65d77955-22b5-4cfe-900f-52ca1c41bbe8.png" width="450px" />
</div>
<br>

No início da função while, o primeiro comando é o HAL_UART_Receive_IT, a cada vez que loop recomeça esse comando salva qualquer dado que possa ter sido enviado via UART em um buffer, esse buffer é então testado em um loop for com os últimos dados recebidos via CAN, para os testes outro STM32 foi programado para receber a mensagem enviada pelo master e de maneira simples enviar a mesma mensagem de volta, por essa razão o master verifica se o Buffer diferencia dos últimos dados enviados via CAN, dessa forma novos dados recebidos via UART são salvos e a prioridade de envio via CAN se mantém para dados novos em vez dos dados já armazenados.
	
Então uma condição com uma função HAL_GetTick é utilizada para contar tempo dentro no projeto sem atrasar o resto da programação assim como acontece com o HAL_Delay, (HAL_GetTick conta o tempo decorrido da programação, ao salvar o valor de tempo da função em uma variável, ao salvar o valor novamente variável no final do if, cada vez que o valor de tempo inserido na condição ultrapassa o último valor de HAL_GetTick salvo então o programa consegue entrar no if novamente, dessa forma uma nova mensagem só será enviada via CAN a cada contagem de tempo.
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150811594-250decf2-ebfd-4c51-9831-a3363b656a42.PNG" width="700px" />
</div>
<br>

Após verificar a condição de datacheck (que é ativada quando uma mensagem via CAN apropriada é recebida, é montada uma mensagem para ser enviada via UART e ser exibida em um terminal serial, o pino C13 é acionado como um meio de checar cada vez que uma mensagem apropriada é recebida, duas strings são declaradas que serão utilizadas para montagem da mensagem a ser enviadas, dois sprintf cada um seguido por uma função HAL_UART_Transmit são programados para então montar a mensagem a ser enviada pelo UART, uma para o ID e outra para os bytes de dados, assim finalizando a montagem da tela a ser exibida no terminal serial.  
  
  
<div align="center">
<img src="https://user-images.githubusercontent.com/68281710/150812078-3927aa54-c580-4564-8b44-c9c12e239f12.png" width="550px" />
</div>
<br>

Como um método de identificação do ID foi estabelecido no recebimento de mensagens e para a possibilidade de trabalhar com múltiplos ID’s simultaneamente, os filtros de ID nas configurações de canfilterconfig foram programados como 0 (zero), pois dessa forma essa função de filtro de ID que ocorre internamente na programação do STM irá aceitar qualquer ID recebido, então o que irá condicionar a filtragem de ID’s e mensagens serão as partes programadas no projeto.

Pasta com os arquivos do [CAN_UART_Master](https://github.com/maiafacens/CAN_UART_Master) ou acesso direto ao [main.c](https://github.com/maiafacens/CAN_UART_Master/blob/master/Core/Src/main.c)
