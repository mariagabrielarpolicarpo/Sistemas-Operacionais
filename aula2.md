# Conceitos 

- Em um sistema de computação, é frequente a necessidade de executar várias tarefas distintas simultaneamente.
- Um processador convencional trata somente um fluxo de instruções por vez, é sequencial.
- Até os processadores com vários núcleos (ou threads) têm mais atividades a executar que o número de processadores disponíveis.
- Um programa de computador é um conjunto de instruções.


## Programas e Tarefas 
- O Programa está armazenado no disco, se está no disco eu não consigo fazer nada com ele, ele está parado, quando eu quero executar aquelas sequências de instruções
eu tenho que criar uma tarefa pra isso. Quem vai dizer o estado interno de uma tarefa são as variáveis. 

### Programa: conjunto de sequências de instruções para resolver um problema específico
- são aplicações ou utilitários
- conceito estático, sem um estado interno definido.
- exemplo C:\Windows\notepad.exe

### Tarefas: 
- execução, pelo processador, das sequências de instruções definidas em um programa.
- conceito dinâmico, que possui estado interno bem definido a cada instante.

## Gerência de Tarefas
- controla a evolução do estado interno das tarefas.
- em um computador, o processador tem de executar todas as tarefas submetidas pelos usuários.
- as tarefas geralmente têm comportamento, duração e importâncias distintas.
- O sistema operacional organiza as tarefas e executa-as. 
aplicando política (conjunto de regras que eu vou usar para decidir sobre alguma coisa), ou seja, qual tarefa deve ser realizada agora e o
mecanismo (como eu aplico as regras) para o escalonamento.

## Sistema Monotarefa 
- É sequencial e executa apenas uma tarefa por vez. Os primeiros sistemas de computação executavam apenas uma tarefa de cada vez.
- Tipo de problemas: se uma tarefa tiver um loop infinito, a tarefa nunca irá parar; o que fazer com o recurso quando está ocioso?
 dependência de tarefas: uma tarefa só pode ser executada depois que outra for executada;
- o processador ficava ocioso durante os períodos de transferência de informação entre disco e memória.
- a velocidade de processamento superava a velocidade de comunicaçao com dispositivos de I/O

## Sistema Multitarefa
- Os sistemas passam a ser preemptivos
- Preempção: ato de retirar um recurso de uma tarefa forçadamente, neste caso o recurso é o processador.

- Nova -> Pronta -> Executando -> Suspensa -> Terminada
  Nova: a tarefa está sendo carregada na memória
  Nova -> Pronta: termina de ser carregada em memória  
  Pronta -> Executando: inicia a execução  
  Executando -> suspensa termina a execução  
  Suspensa -> terminada dado disponível ou evento ocorreu
  Terminada - aguarda um dado externo ou outro evento

### Sistema de Tempo Compartilhado
- A ideia é monitorar o tempo que uma tarefa tá executando e se o tempo esgotou, a tarefa será interrompida e dará a vez para uma outra tarefa.
- Para isso é necessário que o SO tenha uma noção que o tempo passa, é possível utilizar um timer que de tempos em tempos irá gerar uma interrupção de tempo que é o timeout e aí
deve-se inserir uma variável global.
- para cada tarefa há um contador individual de tempo que é o quantum. Quando o quantum chega a 0 é que a tarefa é interrompida.

## Contexto de Execução 
- Toda tarefa possui estados internos.
- contexto: é o estado interno da tarefa, que se modifica conforme a execução da tarefa evolui
- registradores do processador (contador de programa, flag etc) 
- áreas de memória
- recursos em uso

### Task Control block 

- identificador da tarefa (geralmente um inteiro);
- estado da tarefa (nova, pronta, executando, suspensa, terminada);
- informações de contexto do processador (valores contidos nos registradores);
- lista de áreas de memória usadas pela tarefa;
Sistemas Operacionais: Conceitos e Mecanismos cap. 5 – pg. 52
- listas de arquivos abertos, conexões de rede e outros recursos usados pela tarefa
(exclusivos ou compartilhados com outras tarefas);
- informações de gerência e contabilização (prioridade, usuário proprietário, data
de início, tempo de processamento já decorrido, volume de dados lidos/escritos,
etc.).

