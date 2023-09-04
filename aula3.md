# Conceitos : Cooperações entre tarefas

As tarefas em um sistema multi-tarefa precisam cooperar. Para conseguirem cooperar é necessário que haja comunicação entre elas. 

A eficiência do sistema multitarefa vem do uso dos recursos. A eficiência está relacionada a menos tempo ocioso. 

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

