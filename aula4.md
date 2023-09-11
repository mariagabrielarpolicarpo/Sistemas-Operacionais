## Monitor 

### Estrutura de um Monitor 
- Conceito de encapsulamento em orientação a objetos. Protege os dados sejam eles em conjunto ou individualmente usando um Mutex.
- Implicitamente dentro de cada uma das funções eu tenho as operações do mutex.
- Implementação do monitor em java: public synchronized ... ()

# Problemas Clássicos de Coordenação 

- Retratam situações de coordenação típicas em muitos sistemas.
- Exemplos:
## Produtores/consumidores: a ideia é: eu tenho tarefas que produzem itens de dados e tenho tarefas que consomem itens de dados.
No meio do caminho eu tenho um buffer/armazém que vai receber os itens que os produtores produzem e vai fornecer os itens que os consumidores consomem. O buffer é um recurso compartilhado e será usado tanto no processo de produção quanto no processo de consumo. Quando eu consumo, o item sai do armazém.
Toda vez que eu produzo algo eu tenho antes que solicitar o mutex e depois liberar.


## Escritores/leitores

Diferença entre leitores/escritores e produtores/consumidores: As leituras podem ser feitas simultaneamente. Ele não retira o item, só lê. Quem modifica o buffer são os escritores e não os leitores.  
Mais de uma tarefa pode ler o mesmo dado. 
Implementação: Se eu estou escrevendo eu tenho que bloquear as escritas e leituras. Se eu estou lendo bloqueia-se somente as escritas. Quero permitir as leituras simultâneas e bloquear 
as escritas simultâneas. 
Solução: criar uma variável global contador de leituras e enquanta ela for diferente de zero, bloqueia as escritas. 

Leitor ao entrar: 
leitores= 0 (contador de leitores na área)
m_cont = 1 (controla o acesso ao contador)

sem_down(m_cont)
leitores++
if(leitores) == 1 
  sem_down(mutex) 
sem_up(m_cont) 

Leitor ao sair: 

sem_down(m_cont)
leitores--
if(leitores) == 0 
  sem_up(mutex) 
sem_up(m_cont) 

Problema: eu só consigo fazer qualquer escrita enquanto não tenho mais leitura. Se tiver muitas operações de leitura, as de escrita não serão realizadas. 


## Jantar dos filósofos

Recursos compartilhados: hashi 
Recursos necessários por filósofo: 2
Total de recursos: 5 

Problema: Ninguém nunca irá comer se cada um deles segurar um hashi. 
Solução do saleiro: Antes de pegar o hashi eu tenho que pegar o saleiro. Se eu tenho 1 saleiro só, apenas 1 irá pegar o hashi. 

# Impasses 

- A missão de coordenar as tarefas é suspender algumas tarefas enquanto outras acessam recursos compartilhados. 
- O acesso aos recursos é via exclusão mútua, no caso do impasse dos carros, a exclusão mútua está na ocupação de todos os espaços.
- Posse e espera: a tarefa tem um recurso e quer acessar o outro. Ex: o carro está em um cruzamento e precisa de um outro pra passar
- Não preempção: a tarefa só libera seus recursos quando quiser, sem preempção.
- Espera circular: ciclo de esperas de recursos.
- Se eu quiser evitar um impasse basta escolher alguma das condições para impasse e resolver.

## Tratando impasses 

- Ignorar: ignorar o risco de impasses.
- Prevenir: regras de programação para prevenir.
- impedir: acompanhar a alocação de recursos e impedir impasses.
- detectar: detectar a ocorrência de impasses e desfazê-los.

## Prevenção de impasses 

- Exclusão mútua: reduzir áreas de exclusão ao mínimo; usar técnicas alternativas, como spooling
- Posse e espera: usar um recurso de cada vez, ou obter todos os recursos necessários antes de iniciar.
- não preempção: poder "arrancar" os recursos dos processos
- espera circular: colocar os recursos de forma ordenada.

Basta quebrar uma condição de impasse. 

## Detectar impasses
1. observar o sistema
2. detectar a ocorrência de um impasse
3. resolver o impasse

como detectar? 
- manter um grafo de alocação de recursos

como corrigir em tempo de execução? 
- eliminar uma das duas tarefas. Mas qual tarefa eliminar?
- é melhor retroceder tarefas, retornando o sistema um estado seguro. Como dar rollback em banco de dados e voltar ao estado inicial. 

