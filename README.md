# Sistemas-Operacionais

## Considerações

- Linux e Linguagem C 
- C é a linguagem de alto nível mais próxima do baixo nível possível
- Os sistemas operacionais são implentados em C, C++ e Rust

- Bibliografia: Sistemas Operacionais Modernos, 2 edição, Tanenbaum 

- Livro principal: Sistemas Operacionais: Conceitos e Mecanismos. Carlos Alberto Maziero. https://wiki.inf.ufpr.br/maziero/lib/exe/fetch.php?media=socm:socm-livro.pdf



## Abstração e gerência 

### Abstração de recursos
Servem para criar formas mais fáceis/flexíveis de usar os recursos do SO. 
Abstrair é tirar a complexidade, ignorar os detalhes sórbidos de como a coisa funciona. 

### Gerência de recursos
Significa que o recurso é sempre finito, há sempre limitações. É papel do SO fazer com que os recursos sejam divididos para qualquer um dos processos/usuários que desejam usar esse recurso.  
Ex: processamento, memória, entrada e saída, rede, arquivos, imagens, telas

#### Processador: executar as tarefas dos usuários e do sistema.  
#### Memória: fornecer áreas de memória isoladas para as aplicações.  
#### Dispositivos: configurar e criar abstrações de dispositivos físicos  
#### Arquivos: criar e manter arquivos e diretórios.   
#### Proteção: definir garantir regras de acesso aos recursos.

## Tipos de Sistemas Operacionais (ou Classificações) 

Tendem a dizer um objetivo/foco pro SO

- Batch: um dos primeiros SO criados na década de 70, naquela época não tinha processos concorrentes/paralelos. Então executa tarefas em sequência (transações, jobs, etc).
Exemplo: patch de atualização
- De rede: fornece serviços de comunicação entre máquinas e sistemas operacionais.
- Distribuído: interconectado em rede, a diferença é que o de rede possui diretórios compartilhados em outra máquina, ex: uma impressora que está em um outro servidor
e vc manda as instruções para aquele servidor.
No sistema distribuído vc não precisa mais saber onde estão os recursos.
Exemplo: não sabemos onde estão armazenados nosso email de gmail, pode estar no brasil, nos eua, na china. Como a AWS que vc não precisa saber onde os dados estão, precisa apenas ter
acesso a eles. 

- Multiuser: cada recurso tem um "dono" e regras de acesso.
- Desktop: o objetivo é fornecer interatividade, fornecer serviços para interfaciar o usuário e o recurso computacional. Possuem interfáce gráfica e texto, mas é um local em que é possível
executar comandos e o computador responder a essa comandos.
- Servidor: não se preocupa em ser bonito pro usuário e sim eficiente, pois gerencia grande quantidade de recursos.
- Embarcados: só serve para mandar comandos para um determinado local. É um sistema restrito que possui um número limitado de funcionalidades. Acontece em tempo real. 
Ex: controle do projetor

## 3 grandes componentes
- Núcleo/kernel: o executável, binário do SO. Vai estar na memória rodando as tarefas.
- Código de inicialização: roda ao ligarmos à máquina, configura o hardware para ser utilizado, inicializa o software (variáveis, estruturas de dados, funções)

- O driver nada mais é do que um software, como uma biblioteca só irá carregar as funções se alguma função é utilizada, assim também funciona o driver. 

- Aplicativos: fornecem pro usuário aquilo que ele quer, seja desenhar, jogar. Mas existem os utilitários como powershell. A interface é um utilitário.
Exemplo de utilitários: windows explorer, powershell, painel de controle, compactador de arquivos, ferramenta de backup.

## Gerenciamento = Políticas + Mecanismos

- Filosofia: separar políticas dos mecanismos.
- Políticas:
  - Algoritmo de alto nível para tomar decisões abstratas: decidir a quantidade de memória para cada aplicação, o próximo pacote de rede a enviar, etc.
  - As políticas devem ser independentes dos mecanismos existentes.
  - Deve-se ter uma interface de configuração que irá criar as regras e implementar uma política
