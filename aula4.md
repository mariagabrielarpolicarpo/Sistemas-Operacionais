## Monitor 

### Estrutura de um Monitor 
- Conceito de encapsulamento em orientação a objetos. Protege os dados sejam eles em conjunto ou individualmente usando um Mutex.
- Implicitamente dentro de cada uma das funções eu tenho as operações do mutex.
- Implementação do monitor em java: public synchronized ... ()

# Problemas Clássicos de Coordenação 

- Retratam situações de coordenação típicas em muitos sistemas.
- Exemplos:
## Produtores/consumidores: a ideia é: eu tenho tarefas que produzem itens de dados e tenho tarefas que consomem itens de dados.
No meio do caminho eu tenho um buffer/armazém que vai receber os itens que os produtores produzem e vai fornecer os itens que os consumidores consomem. O buffer é um recurso compartilhado e será usado tanto
no processo de produção quanto no processo de consumo. Quando eu consumo, o item sai do armazém.

## Escritores/leitores

## Jantar dos filósofos
