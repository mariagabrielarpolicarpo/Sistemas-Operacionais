# Conteúdo
Conceitos básicos: tipos de memória, memória em processo, alocação de variáveis

## Tipos de Memória 

- Um computador possui diversos dispositivos de armazenamento de dados como registradores, caches, RAM, SSD/HD, pendrive

- Cada dispositivo possui características diferentes entre si.

- Volátil: megabytes, kb - mb ,kb
- Não volátil: gigabytes pra baixo (tera, peta etc)# Conteúdo
Conceitos básicos: tipos de memória, memória em processo, alocação de variáveis

## Tipos de Memória 

- Um computador possui diversos dispositivos de armazenamento de dados como registradores, caches, RAM, SSD/HD, pendrive

- Cada dispositivo possui características diferentes entre si.

- Volátil: megabytes, kb - mb ,kb
- Não volátil: gigabytes pra baixo (tera, peta etc)

Se eu preciso do dado por muito tempo, o dado deve estar armazenado na memória não volátil. 
Para realizar uma operação (dados de trabalho) é necessário que o dado esteja registrado em uma memória volátil, mais precisamente nos registradores.

Para fazer as operações ficarem mais rápidas, os dados são armazenados na memória cache. Então há cópia de dados em várias partes diferentes. 

## Memória de um procesos

Todo processo possui 5 áreas distintas de memória

- Text: código binário (executável), guarda instruções de máquina
- Data: variáveis globais/estáticas inicializadas (valores armazenados no programa executável)
- BSS: variáveis globais não inicializadas.
- Heap:tem tamanho variável, dados alocados dinamicamente
- Stack: pilha de execução, tem tamanho variável e cresce "para baixo".


## Alocação de variáveis 

Alocar = para reservar espaço na memória, é necessário o endereço de início da variável e quanta informação eu desejo guardar. 

Existem diversas formas de alocação de memória: 
- Alocação estática
- Alocação dinâmica: usamos funções como malloc() e free(). Operador new() em linguagens a objetos. Usa a área heap (delimitada pelo ponteiro BRK), tamanho da heap pode ser ajustada pelo SO. Irá verificar se a memória que foi
reservada ainda está me uso, senão mata essa memória. 
- Alocação automática: para variáveis usadas me funções e procedimentos: variáveis locais, parâmetros de entrada, valor de retorno; a alocação é feita na pilha (área stack).
Áreas alocadas ao invocar a função, áreas liberadas ao concluir a função, conveniente para chamadas recursivas.

### Tradução Símbolo -> Endereço

Program Source - na edição: o programador define os endereços. 
Program Source -> (Compile) Object files - na compilação o compilador define os endereços. 
Object files -> (Link) Executable - na ligação: o compilador define símbolos sem endereços, o ligador defie os endereços ao construir o executável. 
Executable -> (load) process - Na carga: o carregador carrega o código do processo na memória e define os endereços para os símbolos.
Process - Na execução: os endereços acessados pelo processo são convertidos nos endeereços efetivos em RAM.

## Hardware de Memória

A memória física é espaço de memória RAM do computador: grnade conjunto de bytes com endereços individuais. 

Conteúdo: Sistema Operacional, Aplicações em execução, Buffers de entrada/saída. 

É dividida em áreas com diferentes finalidades. 


## Espaço de endereçamento

- Faixas de endereços que o processador consegue acessar.
- Depende da arquitetura e barramentos.
- Não depende da quantidade de RAM disponível.
    - Endereço válido: existe um byte na RAM naquela posição
    - Endereço inválido: não existem RAM naquela posição
 
## Memória Virtual

- Sepração entre memória RAM e espaço de endereçamento.
    - Endereços lógicos: endereços gerados pelo processador ao executar.
    - Endereços físicos: endereços acessados na memória RAM.
 
- Ao executar, a CPU e os processos só veem os endereços lógicos.
- A memória RAM é acessada por endereços físicos.

Memória virtual: 
  - Forma como a CPU e o software veem a memória

- Por partições: é sempre associada com uma partição, então é um pedação de memória contínuo que é dado para a aplicação.
  - Implementação da MMU usa dos registradores: 1) base(B) que é o endereço físico inicial da partição ativa 2) limite(L) que é o tamanho da partição
  - Vantagens: é simples, é rápido, é barato.
  - Desvantagens: espaço sem uso quando a partição é muito maior que a demanda do processo, número de processos é limitado, como compartilhar uma variável que está dentro de um bloco de memória?

- Por segmentos: cada processo tem um conjunto de áreas:
  - Text, Data, BSS, heap, Stack.
  - Não preciso a priori alocar as partições, é possível fazer alocação dinâmica.
 
  Usa endereços lógicos bidimensionais [S:O]
  - S: número do segmento na tabela do processo.
  - Vantagens: flexibilidade: alocação das áreas conforme a necessidade.
  - Desvantagens: mais complexo de implementar, são necessários mais acessos à memória RAM. 

Se eu preciso do dado por muito tempo, o dado deve estar armazenado na memória não volátil. 
Para realizar uma operação (dados de trabalho) é necessário que o dado esteja registrado em uma memória volátil, mais precisamente nos registradores.

Para fazer as operações ficarem mais rápidas, os dados são armazenados na memória cache. Então há cópia de dados em várias partes diferentes. 

## Memória de um procesos

Todo processo possui 5 áreas distintas de memória

- Text: código binário (executável), guarda instruções de máquina
- Data: variáveis globais/estáticas inicializadas (valores armazenados no programa executável)
- BSS: variáveis globais não inicializadas.
- Heap:tem tamanho variável, dados alocados dinamicamente
- Stack: pilha de execução, tem tamanho variável e cresce "para baixo".


## Alocação de variáveis 

Alocar = para reservar espaço na memória, é necessário o endereço de início da variável e quanta informação eu desejo guardar. 

Existem diversas formas de alocação de memória: 
- Alocação estática
- Alocação dinâmica: usamos funções como malloc() e free(). Operador new() em linguagens a objetos. Usa a área heap (delimitada pelo ponteiro BRK), tamanho da heap pode ser ajustada pelo SO. Irá verificar se a memória que foi
reservada ainda está me uso, senão mata essa memória. 
- Alocação automática: para variáveis usadas me funções e procedimentos: variáveis locais, parâmetros de entrada, valor de retorno; a alocação é feita na pilha (área stack).
Áreas alocadas ao invocar a função, áreas liberadas ao concluir a função, conveniente para chamadas recursivas.

### Tradução Símbolo -> Endereço

Program Source - na edição: o programador define os endereços. 
Program Source -> (Compile) Object files - na compilação o compilador define os endereços. 
Object files -> (Link) Executable - na ligação: o compilador define símbolos sem endereços, o ligador defie os endereços ao construir o executável. 
Executable -> (load) process - Na carga: o carregador carrega o código do processo na memória e define os endereços para os símbolos.
Process - Na execução: os endereços acessados pelo processo são convertidos nos endeereços efetivos em RAM.

## Hardware de Memória

A memória física é espaço de memória RAM do computador: grnade conjunto de bytes com endereços individuais. 

Conteúdo: Sistema Operacional, Aplicações em execução, Buffers de entrada/saída. 

É dividida em áreas com diferentes finalidades. 


## Espaço de endereçamento

- Faixas de endereços que o processador consegue acessar.
- Depende da arquitetura e barramentos.
- Não depende da quantidade de RAM disponível.
    - Endereço válido: existe um byte na RAM naquela posição
    - Endereço inválido: não existem RAM naquela posição
 
## Memória Virtual

- Sepração entre memória RAM e espaço de endereçamento.
    - Endereços lógicos: endereços gerados pelo processador ao executar.
    - Endereços físicos: endereços acessados na memória RAM.
 
- Ao executar, a CPU e os processos só veem os endereços lógicos.
- A memória RAM é acessada por endereços físicos.

Memória virtual: 
  - Forma como a CPU e o software veem a memória

- Por partições: é sempre associada com uma partição, então é um pedação de memória contínuo que é dado para a aplicação.
  - Implementação da MMU usa dos registradores: 1) base(B) que é o endereço físico inicial da partição ativa 2) limite(L) que é o tamanho da partição
  - Vantagens: é simples, é rápido, é barato.
  - Desvantagens: espaço sem uso quando a partição é muito maior que a demanda do processo, número de processos é limitado, como compartilhar uma variável que está dentro de um bloco de memória?

- Por segmentos: cada processo tem um conjunto de áreas:
  - Text, Data, BSS, heap, Stack.
  - Não preciso a priori alocar as partições, é possível fazer alocação dinâmica.
 
  Usa endereços lógicos bidimensionais [S:O]
  - S: número do segmento na tabela do processo.
  - Vantagens: flexibilidade: alocação das áreas conforme a necessidade.
  - Desvantagens: mais complexo de implementar, são necessários mais acessos à memória RAM. 
