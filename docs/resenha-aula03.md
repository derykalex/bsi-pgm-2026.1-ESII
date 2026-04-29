# Resenha Aula 3 — Modelos UML e Design de Componentes  
**Aluno:** Alex da Silva Oliveira  
**Data:** 29/04/2026  

## Questão 1 — Modelos UML como ferramentas de modelagem  

### (a) Estrutura × comportamento  
No Capítulo 4, Valente apresenta que modelos UML são formas de abstração, ou seja, representações que destacam certos aspectos de um sistema e deixam outros em segundo plano dependendo do objetivo. O diagrama de classes enfatiza a estrutura estática, mostrando classes, atributos, métodos e relações entre componentes. Ele é importante para compreender como o sistema está organizado, quais entidades existem e como se conectam. Porém, esse modelo não evidencia como ocorre o fluxo de execução das funcionalidades. Já o diagrama de sequência destaca o comportamento dinâmico, revelando como objetos interagem, em qual ordem as mensagens acontecem e quais operações são executadas. Dessa forma, ele mostra o funcionamento temporal do sistema. Valente considera esses dois diagramas complementares porque cada um responde perguntas diferentes: o diagrama de classes mostra “como o sistema está estruturado”, enquanto o de sequência mostra “como o sistema se comporta em ação”. No contexto do projeto, usar apenas um deles seria insuficiente, pois compreender somente a estrutura não garante entendimento operacional, e analisar apenas comportamento não esclarece a organização arquitetural.

### (b) Consequência prática  
Na prática, o diagrama de classes contribui para decisões relacionadas ao design estrutural, como definição de responsabilidades, separação de entidades e organização lógica do sistema. Por exemplo, ele ajuda a decidir quais atributos pertencem à classe Equipamento ou Usuário. Já o diagrama de sequência auxilia decisões funcionais, como identificar métodos necessários e ordem de execução em processos específicos. Assim, enquanto o diagrama de classes orienta a construção da base estrutural, o de sequência contribui para implementação dos fluxos de uso.

### (c) Aplicação ao UC01  
No UC01 (Registrar Empréstimo), um diagrama de sequência revelaria de maneira mais precisa quais objetos participam do processo, como interface, serviço e repositório, além da ordem das interações. Isso mostraria etapas como verificar disponibilidade, registrar empréstimo e salvar dados. O casos_de_uso.md textual explica o objetivo geral, mas não detalha tecnicamente quais métodos precisam existir nem como ocorre a comunicação entre componentes.

## Questão 2 — Arquitetura, design e os princípios de decomposição  

### (a) Definições  
Coesão pode ser entendida como o nível em que um módulo mantém foco em uma responsabilidade principal, evitando reunir funções excessivamente diferentes. Acoplamento refere-se ao grau de dependência entre módulos; quanto menor essa dependência, mais fácil é manter e modificar o sistema. Já o ocultamento de informação consiste em proteger detalhes internos de implementação, expondo apenas o necessário para interação externa.

### (b) Relações entre os princípios  
O ocultamento de informação favorece baixo acoplamento porque impede que módulos dependam diretamente de detalhes internos de outros componentes. Isso reduz impactos quando mudanças são feitas. A coesão também contribui para organização, pois módulos mais focados tendem a ter responsabilidades mais claras. Entretanto, existe certa tensão, já que dividir excessivamente o sistema pode gerar comunicação demais entre módulos, aumentando dependências. Portanto, o equilíbrio entre esses princípios é essencial.

### (c) Aplicação ao projeto v2.0  
Na camada models/, classes como Equipamento, Usuario e Emprestimo devem representar entidades centrais do domínio. Em services/, classes como EmprestimoService devem concentrar regras de negócio. Em repositories/, classes como EquipamentoRepository devem lidar com persistência de dados. Já o main.py deve controlar a interação com o usuário. Essa divisão fortalece coesão, reduz acoplamento e melhora ocultamento de informação.

## Questão 3 — Crítica fundamentada à documentação do sistema legado  

### (a) Pontos frágeis  
Na análise do sistema legado, percebe-se que a presença de baixa coesão quando múltiplas responsabilidades ficam concentradas em uma única estrutura. Outro problema é o alto acoplamento entre partes do sistema quando componentes dependem diretamente uns dos outros sem abstrações claras. Essas decisões dificultam manutenção e evolução.

### (b) Ponto forte  
Um ponto positivo é o reconhecimento explícito da dívida técnica na documentação. Isso demonstra consciência de que certas decisões são provisórias e precisam ser melhoradas futuramente. Segundo Valente, reconhecer limitações de forma transparente é uma postura importante para evolução arquitetural.

### (c) Síntese  
A transparência sobre a dívida técnica mostra maturidade do desenvolvedor, pois evidencia compreensão de que a versão inicial possui limitações estruturais. Em vez de ignorar problemas, a documentação cria base para uma v2.0 mais organizada, com melhorias planejadas e foco em refatoração consciente.

## Questão 4 — Tipos como contratos: dicionários × classes  

### (a) Prevenção de erros  
No sistema baseado em dicionários, erros como digitação incorreta em chaves ou ausência de campos podem ocorrer com maior facilidade. Por exemplo, uma chave escrita incorretamente pode gerar falhas difíceis de detectar. Classes reduzem esse problema porque organizam atributos de forma mais controlada, fortalecendo clareza estrutural.

### (b) Capacidade de evolução  
Classes permitem adicionar novos comportamentos, como métodos específicos, sem comprometer toda a estrutura de uso. Isso facilita evolução do sistema. Já dicionários são mais limitados, pois armazenam dados sem representar comportamento diretamente.

### (c) Comunicação do design  
Uma classe chamada Equipamento comunica melhor sua função dentro do projeto do que um dicionário genérico. Ela representa não apenas dados, mas também intenção de design. Conforme Valente discute, clareza de modelo é parte essencial do projeto, pois melhora comunicação, manutenção e compreensão do sistema.
