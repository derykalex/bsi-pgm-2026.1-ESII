# Resenha Aula 3 — Modelos UML e Design de Componentes  
**Aluno:** Alex da Silva Oliveira  
**Data:** 29/04/2026  

## Questão 1 — Modelos UML como ferramentas de modelagem  

### (a) Estrutura × comportamento  
No Capítulo 4, Valente explica que diagramas UML são modelos, ou seja, formas de representar um sistema destacando aspectos específicos conforme o objetivo da análise. No sistema legado de empréstimos, o diagrama de classes ajuda a entender como o sistema está organizado, mostrando entidades como Equipamento, Usuário e Empréstimo, além de seus atributos, métodos e relações. Esse modelo é importante para visualizar a estrutura e a organização do sistema, mas não mostra como as ações realmente acontecem durante o uso. Já o diagrama de sequência mostra o comportamento do sistema, revelando a ordem das interações entre interface, regras de negócio e armazenamento durante uma operação. Na prática, enquanto o diagrama de classes mostra “como o sistema é estruturado”, o diagrama de sequência mostra “como ele funciona em execução”. Segundo Valente, essas representações são complementares justamente porque cada uma revela uma dimensão diferente do projeto. No contexto analisado, entender apenas as classes não seria suficiente para visualizar todas as etapas e validações necessárias para registrar corretamente um empréstimo.

### (b) Consequência prática  
Na prática, o diagrama de classes contribui para decisões mais estruturais, como definir responsabilidades para classes como Equipamento, Usuario e Emprestimo, além de organizar melhor o domínio do sistema. Ele ajuda a transformar uma estrutura muito procedural em algo mais organizado e orientado a objetos. Já o diagrama de sequência contribui para decisões funcionais, pois mostra quais objetos participam de uma operação, em que ordem interagem e quais métodos precisam existir. Dessa forma, o diagrama de classes orienta melhor a arquitetura lógica, enquanto o de sequência ajuda diretamente na implementação dos processos.

### (c) Aplicação ao UC01  
No UC01 (Registrar Empréstimo), o casos_de_uso.md apresenta o objetivo principal da operação, mas um diagrama de sequência mostraria com mais clareza como esse processo realmente acontece. Ele revelaria, por exemplo, que o usuário solicita o empréstimo, o sistema verifica a disponibilidade do equipamento, valida condições e registra a operação. Isso deixa mais claro o fluxo entre interface, lógica de negócio e armazenamento. Também evidencia a necessidade de métodos específicos, como verificar_disponibilidade(), validar_usuario() e registrar_emprestimo(), que o texto sozinho não detalha tecnicamente.

## Questão 2 — Arquitetura, design e os princípios de decomposição  

### (a) Definições  
Segundo Valente no Capítulo 7, coesão pode ser entendida como o grau em que um módulo mantém foco em uma função específica. Em outras palavras, significa evitar que uma mesma parte do sistema faça tarefas demais ao mesmo tempo. No sistema legado, isso ajuda a evitar que cadastro, validação e persistência fiquem misturados. Acoplamento é o nível de dependência entre módulos; quanto maior essa dependência, mais difícil modificar uma parte sem afetar outra. Já o ocultamento de informação significa proteger detalhes internos, permitindo que outras partes utilizem apenas o necessário. Esses princípios ajudam a tornar o sistema mais organizado, compreensível e fácil de manter.

### (b) Relações entre os princípios  
No processo de evolução da v1.0 para a v2.0, o ocultamento de informação ajuda a reduzir acoplamento porque separa regras de negócio da forma como os dados são armazenados. Por exemplo, quando a lógica de empréstimo não depende diretamente da estrutura de armazenamento, mudanças internas geram menos impacto. A coesão também melhora porque cada camada assume uma responsabilidade mais clara. Ao mesmo tempo, dividir demais o sistema pode criar dependências extras, então o equilíbrio é essencial. Assim, arquitetura eficiente não depende apenas de separar partes, mas de organizar essa separação de forma lógica.

### (c) Aplicação ao projeto v2.0  
Com base no ADR-001, classes como Equipamento, Usuario e Emprestimo devem ficar em models/, pois representam as entidades principais do sistema. A camada services/ deve concentrar regras como registrar empréstimos, devoluções e validações. Já repositories/ deve cuidar do acesso e armazenamento de dados, reduzindo dependência direta entre lógica e persistência. O main.py deve controlar interface e fluxo principal. Comparando com a estrutura inicial, essa divisão organiza melhor o sistema, aumenta coesão, reduz acoplamento e corrige fragilidades percebidas na versão legado.

## Questão 3 — Crítica fundamentada à documentação do sistema legado  

### (a) Pontos frágeis  
Ao analisar o sistema legado descrito em projeto.md, percebe-se como fragilidade a concentração de várias responsabilidades em estruturas pouco especializadas. Quando cadastro, controle de disponibilidade e registro operacional ficam pouco separados, a manutenção se torna mais difícil e a coesão diminui. Outro problema é a dependência direta entre regras e dados, o que sugere alto acoplamento e reduz flexibilidade. Essas escolhas podem funcionar em versões iniciais, mas dificultam evolução e manutenção conforme o sistema cresce.

### (b) Ponto forte  
Um ponto positivo da documentação é reconhecer explicitamente limitações e dívida técnica da v1.0. Isso demonstra maturidade porque mostra que o projeto não trata sua primeira versão como definitiva. Segundo Valente, reconhecer dívida técnica de forma clara é importante quando existe intenção de melhorar e refatorar futuramente.

### (c) Síntese  
A identificação da dívida técnica no sistema legado mostra uma postura mais consciente de desenvolvimento, pois transforma problemas reconhecidos em base para evolução futura. Em vez de ignorar limitações, a documentação cria fundamentos para uma v2.0 mais organizada, com melhor separação de responsabilidades e arquitetura mais sólida. Dessa forma, a dívida técnica passa a ser não apenas uma falha, mas também um ponto de partida para melhorias.

## Questão 4 — Tipos como contratos: dicionários × classes  

### (a) Prevenção de erros  
No arquivo emprestimos.py da v1.0, o uso de dicionários para acessar dados como equipamento["disponivel"] mostra uma dependência de chaves textuais que pode gerar erros por digitação incorreta ou ausência de informações. Essa abordagem oferece flexibilidade, mas reduz clareza estrutural. Se classes fossem utilizadas, atributos e responsabilidades seriam mais explícitos, o que ajudaria a prevenir erros e melhoraria a organização do código.

### (b) Capacidade de evolução  
Pensando em versões futuras, classes permitiriam adicionar comportamentos como calcular_multa() ou validar_status() diretamente nas entidades do sistema. Isso torna a evolução mais organizada e reduz dispersão de regras. Já dicionários exigem que novas funcionalidades sejam implementadas em outras partes do código, o que pode aumentar fragilidade e dificultar manutenção.

### (c) Comunicação do design  
Uma classe como Equipamento comunica de forma mais clara seu papel e sua função dentro do sistema de empréstimos do que um dicionário genérico. Conforme Valente argumenta, tipos não servem apenas para armazenar dados, mas também para comunicar design e organização do projeto. No contexto deste sistema, migrar de dicionários para classes representa não só uma mudança técnica, mas uma evolução na clareza e na qualidade do modelo.
