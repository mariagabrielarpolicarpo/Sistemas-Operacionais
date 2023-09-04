# Cooperações entre tarefas

- As tarefas em um sistema multi-tarefa precisam cooperar. Para conseguirem cooperar é necessário que haja comunicação entre elas. 

- A eficiência do sistema multitarefa vem do uso dos recursos. A eficiência está relacionada a menos tempo ocioso. 

## Motivações 

- Atender vários usuários simultâneos: servidor de bancos de dados ou de e-mail.
- Uso de computadores multi-core: para diminuir o tempo de execução de uma aplicação; fazer uso mais eficiente de recursos computacionais.
- Modularidade: dividir um problema grande e complexo em partes pequenas
- Aplicações interativas

Cooperação = comunicação + coordenação

## Aspectos da Comunicação 

- Comunicação direta: Entre A e B. A e B se conhecem. Não há nenhum intermediador e pra ela acontecer, a primitiva de enviar e recebiar possui receptor e emissor identificador.
- Comunicação indireta: Possui um canal entre A e B. Pode ser exclusivo pra dois elementos ou mais. Emissor envia dados ao canal e receptor recebe.

## Sincronismo 

- Comunicação Síncrona(Bloqueante): as operações de envio/recepção podem suspender as tarefas quando o outro lado não está pronto para a comunicação. 
- Comunicação Assíncrona (Não bloqueante): as operações de envio/recepção não bloqueiam as tarefas. Se algum dos lados começar a operação e o outro lado não estiver pronto, lançará uma mensagem de erro. A comunicação só acontece quando os dois lados estão prontos para a comunicação.
- Semissíncrono (Semibloqueante): as operações são bloqueantes durante um prazo bem definido.

## Envio por mensagens 

- Mensagem: pacote de dados recebido ou descartado pelo receptor em sua íntegra (os dados podem ser encapsulados em uma ou mais mensagens)
- O envio/recepção das mensagem é atômico (não é possível enviar uma mensagem pela metade, apenas inteira)

## Envio por fluxo 
- O canal de comunicação é visto com um arquivo (o emissor "escreve" dados no canal, que serão "lidos" na mesma ordem)
- o receptor controla a quantidade de dados que será recebida.

## Canais de comunicação 

### Capacidade dos canais
- o comportamento do canal é afetado pelos buffers para dados em trânsito.
- capacidade nula (n=0): comunicação feita por transferência direta entre receptor e emissor.
- capacidade infinita: 
- capacidade finita: uma quantidade finita de dados pode ser enviada pelo emissor, haverá bloqueio se aquilo que receber estiver vazio, mas nunca haverá bloqueio para quem transmite.

### Confiabilidade dos canais
- canal confiável: transporta ao destino todos os dados recebidos, respeitando sua integridade e ordem de envio. 
- canal não confiável: podem ocorrer vários tipos de perdas - de dados, de integridade, de ordem.

### Número de participantes

- 1:1 - há apenas dois elementos que partiicpação da comunicação através do canal. 
- M:N - vários que transmitem e vários que recebem
- Canal N:M - mailbox: cada mensagem é recebida por apenas um receptor.
- Canal de eventos: cada mensagem é recebida por todos os receptores. 

# Mecanismos de comunicação

## Pipes

- Canal de comunicação local entre dois processos(1:1), unidirecional, síncrono, orientado a fluxo, confiável e com capacidade finita
- liga a saída de um processo à entrada de outro
- stdin entrada padrão - (scanf, getchar)
- stdout saída padrão (printf, ...)
- stdout - saída de erro (perror,...)

### Pipes IPC Windows
- Canal de comunicação local entre vários processos
- Um processo grava informações e outro lê no pipe.
- Um pipe tem duas extremidades.
- Um pipe unidirecional permite que o processo em uma extremidade seja gravado no pipe e permite que o processo na outra extremidade leia do pipe.
- Um pipe bidirecional permite que um processo leia e escreva do final do pipe.
- Um pipe anônimo é um pipe unidirecional sem nome que normalmente transfere dados entre um processo pai e um processo filho.
- Um pipe nomeado é unidirecional ou bidirecional para comunicação entre o servidor de pipe e um ou mais clientes de pipe.
Todas as instâncias de um pipe nomeado compartilham o mesmo nome, mas cada instância tem seus próprios buffers
e identificadores e fornece um canal separado para comunicação cliente/servidor. 

### Pipes nomeados (FIFOs)

- cria um pipe nomeado, cujo nome é/tmp/pipe  
$ mkfifo /tmp/pipe  

- mostra o nome do pipe no diretório  
$ ls -l /tmp/pipe  
prw-rw-r-- 1 maziero maziero 0 sept. 6 18:14 pipe  

- envia dados (saída do comando date) para o pipe nomeado  
$ date > /tmp/pipe  

 - EM OUTRO TERMINAL, recebe dados do pipe nomeado  
 $ cat < /tmp/pipe  
 Thu Sep 6 2018, 18:01:50 (UTC+0200)  

- remove o pipe nomeado  
16 $ rm /tmp/pipe  


## Fila de mensagens: POSIX

- fila de mensagens no linu: mecanismo de comunicação entre vários procesoss, confiáveis, orientadas a mensagens e com capacidade finita. 
- implementar o conceito de mailbox

## Memória compartilhada 
- processos leem e escrevem na mesma área de memória
- normalmente proibido pelos mecanismos de hardware
- núcleo ajusta mapas de memória para criar área compartilhada


# Coordenação entre tarefas

Execução concorrente - exemplo: operação de depósito em uma conta bancária 

Race conditions [adicionar]

### Condições de disputa são erros dinâmicos: 
- não aparecem no código fonte
- só se manifestam durante a execução
- são difíceis de detectar
- podem ocorrer raramente ou nunca
- sua depuração pode ser muito complexa

### Condições de Bernstein 
- formalizam as condições de disputa
- t1 e t2: duas tarefas executando em paralello
- r(t): conjunto de variáveis lidas por t
- w(t): conjunto de variáveis escritas por t


               R(t1) ∩ W(t2) = ∅ (t1 não lê as variáveis escritas por t2)
  t1 || t2 ⇐⇒  R(t2) ∩ W(t1) = ∅ (t2 não lê as variáveis escritas por t1)
               W(t1) ∩ W(t2) = ∅ (t1 e t2 não escrevem nas mesmas variáveis)

  ### Seções críticas
  - São trechos de código de cada tarefa que acessa dados compartilhados, onde podem ocorrer condições de disputa.
  - Exclusão mútua: impedir o entrelaçamento de seções críticas, de modo que apenas uma tarefa esteja na seção crítica a cada instante.
 
  ### Exclusão mútua
  - Cada seção crítica i pode ser associada a um identificador csi.
 
  - Primitivas de controle:
  - a) enter: a tarefa deseja entrar na seção crítica
  - b) leave: a tarefa está saindo da seção crítica
  - A primitiva enter é bloqueante: t(a) fica esperando até que cs(i) esteja livre.

é necessário avisar que a tarefa está entrando e saindo:

void depositar (long conta, long *saldo, long valor)  
2 {  
3 enter (conta) ; // entra na seção crítica "conta"  
4 (*saldo) += valor ; // usa as variáveis compartilhadas  
5 leave (conta) ; // sai da seção crítica  
6 }  


- Exclusão mútua: somente uma tarefa pode estar dentro da seção crítica em cada instante.
- Espera limitada: uma tarefa que aguarda acesso a uma seção crítica deve recebê-la em tempo finito.
- Independência de outras tarefas: a decisão sobre o uso de uma seção crítica deve
depender somente das tarefas que estão tentando usá-la.
- Independência de fatores físicos: mecanismo não deve depender da velocidade do sistema, de temporizações, do número de processadores ou de outros fatores físicos.

## Inibição de interrupções 

- inibir as interrupções durante acesso às seções críticas. 
- impede as trocas de contexto dentro da seção crítica.
- desabilitar algumas interrupções, mas deixar outras funcionando.

### Solução: alternância de uso 

- Usar uma variável turno para indicar quem pode entrar na seção crítica


### Operações atômicas

- Instruções de máquinas específicas: a) tsl - test and set lock (testa um valor e o configura) b) cas - compare and swap c) xchg - exchange

### Quais os problemas destas implementações? 

- Ineficiência: processador testa continuamente uma condição (espera ocupada) 
- Injustiça: não garantem ordem no acesso à seção crítica 
- Dependência: na solução por alternância, tarefas desejando acessar a seção crítica
podem ser impedidas de fazê-lo por tarefas que não têm interessa na seção
crítica naquele momento.
