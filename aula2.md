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

- O despacher é uma das poucas coisas no SO que é implementado em assembly.

## Processos
- é um contêiner de cursos utilizados por uma ou mais tarefas por sua execução.
- os processos são isolados entre si pelos mecanismos de proteção providos pelo hardware (isolamento de áreas de memória, níveis de operação e chamadas de sistema).
- benefícios: segurança e robustez. Se ocorrer um erro, ele vai ficar isolado ali naquele contêiner.

 ### Criação de Processos
 - processos são criados através de chamadas de sistemas, cada SO tem as suas. Ex: Padrão POSIX
 - windows: createprocess(): cria um novo processo, informando o nome do arquivo contendo o código a executar
 - unix: fork(): duplica o processo atual ; execve(file):

## Threads 
- são cada um dos fluxo de execução operando dentro de um sistema ou de um núcleo operacional.

### Tipos
- threads de usuário: cada um dos fluxos de execução dentro de um processo, geralmente associadas à execução da aplicação.
- threas de núcleo: cada um dos fluxos de execução dentro de um núcleo. Pode representar fluxos de usuários ou atividades internas do núcleo.

- Existem três modelo de implantação:

### Modelos de Threads N:1 

- biblioteca para suportar as threads em sistemas antigos.
- gerenciamento sem envolvimento do núcleo.
- muito utilizado por ser fácil e de leve implantação.
- ideal para aplicações com milhares/milhôes de threads
- ponto negativo: se der erro em uma thread, trava o programa inteiro.

### Modelos de Threads 1:1
- gerência de threads incorporadas ao núcleo, o núcleo tem controle sobre tudo, ele pode parar uma thread mal comportada se quiser
- cada thread de usuário é mapeada em uma thread de núcleo
- as threads são escalonadas de forma independente, podendo usar vários processadores
- é a implementação mais frequente nos sistemas atuais
- ponto negativo: é pouco escalável, no máximo centenas ou alguns milhares de threads.

### Modelos de Threads N:M 
- parte do escalonamento fica no gerenciador e a outra parte vai para a aplicação
- modelo híbrido: agrega características de ambos os modelos.
- uma biblioteca gerencia um conjunto de threads do usuário (dentro do processo)
- as threads de usuário são mapeadas em uma ou mais threads do núcleo.
- o número de threads do núcleo é ajustado dinamicamente conforme a demanda da aplicação
- ponto negativo: maior complexidade de implementação; maior custo de gerência das threads do núcleo. 
