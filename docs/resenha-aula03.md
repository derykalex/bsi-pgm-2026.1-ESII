# Resenha Aula 3 — Modelos UML e Design de Componentes  
**Aluno:** Alex da Silva Oliveira  
**Data:** 29/04/2026  

## Questão 1 — Modelos UML como ferramentas de modelagem  

### (a) Estrutura × comportamento  
No Capítulo 4, Valente apresenta que diagramas UML são modelos, isto é, abstrações construídas para destacar aspectos específicos de um sistema conforme determinado propósito. No contexto do sistema legado de empréstimos analisado, o diagrama de classes permite compreender sua estrutura estática ao representar entidades centrais como Equipamento, Usuário e Empréstimo, além de seus atributos e relações. Esse modelo favorece entendimento organizacional, mas não explicita como o processo de empréstimo ocorre operacionalmente. Já o diagrama de sequência enfatiza comportamento dinâmico, revelando a ordem das interações entre interface, regras de negócio e armazenamento durante a execução de uma funcionalidade. Assim, enquanto o diagrama de classes evidencia organização estrutural, o de sequência demonstra fluxo funcional. Conforme Valente argumenta, essas representações são complementares porque respondem perguntas distintas: “como o sistema está organizado” e “como o sistema opera”. No projeto analisado, essa diferença é relevante porque compreender apenas entidades como equipamento ou empréstimo não revela, por exemplo, a sequência de validações necessárias para registrar corretamente uma operação.

### (b) Consequência prática  
Na prática, o diagrama de classes contribui para decisões sobre decomposição estrutural, como definir responsabilidades de Equipamento, Usuario e Emprestimo dentro do domínio. Ele ajuda a estruturar melhor o sistema legado ao substituir organização excessivamente procedural por entidades mais claras. Já o diagrama de sequência auxilia decisões sobre implementação do UC01, permitindo identificar ordem de execução, dependências entre objetos e métodos obrigatórios. Dessa forma, classes orientam arquitetura lógica, enquanto sequências orientam comportamento operacional.

### (c) Aplicação ao UC01  
No UC01 (Registrar Empréstimo), o casos_de_uso.md descreve o objetivo geral da operação, mas um diagrama de sequência revelaria de maneira mais detalhada como o usuário solicita o empréstimo, como o sistema verifica disponibilidade do equipamento, valida condições e registra a operação. Isso evidencia interação entre interface principal, lógica de negócio e estrutura de armazenamento presente no sistema legado. Também torna explícita a necessidade de métodos como verificar_disponibilidade(), validar_usuario() e registrar_emprestimo(), elementos que o texto descritivo não detalha tecnicamente.

## Questão 2 — Arquitetura, design e os princípios de decomposição  

### (a) Definições  
Conforme Valente discute no Capítulo 7, coesão representa o grau em que um módulo concentra responsabilidades relacionadas a uma finalidade específica. No sistema legado, isso significa evitar que um mesmo componente controle cadastro, validação e persistência simultaneamente. Acoplamento corresponde ao nível de dependência entre módulos; quanto maior, mais difícil modificar partes isoladamente. Já o ocultamento de informação consiste em proteger detalhes internos, como regras de armazenamento ou manipulação de dados, expondo apenas o necessário. Esses princípios são fundamentais para transformar o sistema legado em uma estrutura mais sustentável.

### (b) Relações entre os princípios  
No contexto da migração da v1.0 para a v2.0, o ocultamento de informação reduz acoplamento ao impedir que regras de negócio dependam diretamente da estrutura de armazenamento. Por exemplo, ao separar lógica de empréstimo da manipulação direta de dados, mudanças em persistência causam menos impacto. A coesão também melhora porque cada camada assume responsabilidade mais clara. Entretanto, decomposição excessiva pode gerar dependências adicionais. Assim, o equilíbrio entre esses princípios é essencial para evolução arquitetural eficiente.

### (c) Aplicação ao projeto v2.0  
Com base no ADR-001, classes como Equipamento, Usuario e Emprestimo devem permanecer em models/, pois representam entidades do domínio do sistema de empréstimos. A camada services/ deve concentrar regras como registrar empréstimos, devoluções e validações de uso. Em repositories/, devem ficar componentes responsáveis pelo acesso e persistência de dados, reduzindo dependência direta entre lógica e armazenamento. Já o main.py deve controlar interface e fluxo principal. Em comparação à estrutura inicial, essa divisão fortalece coesão, reduz acoplamento e corrige fragilidades do sistema legado.

## Questão 3 — Crítica fundamentada à documentação do sistema legado  

### (a) Pontos frágeis  
Ao analisar o sistema legado descrito em projeto.md, percebe-se como fragilidade a concentração de múltiplas responsabilidades em estruturas pouco especializadas, caracterizando baixa coesão. Quando cadastro, controle de disponibilidade e registro operacional coexistem de forma pouco separada, manutenção e evolução tornam-se mais difíceis. Outro ponto frágil é o uso de estruturas com dependência direta entre regras e dados, o que sugere alto acoplamento e violação de ocultamento de informação. Essas escolhas reduzem flexibilidade arquitetural.

### (b) Ponto forte  
Um aspecto positivo da documentação é reconhecer explicitamente limitações e dívida técnica da v1.0. Essa transparência demonstra maturidade, pois o projeto não apresenta suas limitações como solução definitiva. Conforme Valente discute, reconhecer dívida técnica deliberada é importante quando existe intenção clara de refatoração.

### (c) Síntese  
A identificação explícita de dívida técnica no sistema legado demonstra postura analítica relevante, pois transforma fragilidades em base para evolução. Em vez de ignorar limitações estruturais, a documentação estabelece fundamentos para que a v2.0 seja construída com arquitetura mais robusta, maior separação de responsabilidades e manutenção mais sustentável.

## Questão 4 — Tipos como contratos: dicionários × classes  

### (a) Prevenção de erros  
No arquivo emprestimos.py da v1.0, o uso de dicionários para acessar informações como equipamento["disponivel"] evidencia dependência de chaves textuais, o que amplia risco de erros por digitação, ausência de campos ou inconsistência estrutural. Essa abordagem oferece flexibilidade, mas reduz clareza de contrato. Caso classes fossem utilizadas, atributos e responsabilidades seriam mais explícitos, fortalecendo prevenção de erros e clareza de modelo.

### (b) Capacidade de evolução  
No contexto da evolução para versões futuras, classes permitiriam incorporar comportamentos como calcular_multa() ou validar_status() diretamente à entidade Equipamento ou Emprestimo. Isso favorece crescimento organizado do sistema. Já dicionários exigem expansão funcional dispersa, aumentando fragilidade e dificultando manutenção.

### (c) Comunicação do design  
Uma classe como Equipamento comunica semanticamente papel, responsabilidade e função dentro do sistema de empréstimos, enquanto um dicionário representa apenas armazenamento genérico. Conforme Valente argumenta, clareza de tipos faz parte do design porque comunica arquitetura e fortalece entendimento entre desenvolvedores. No contexto deste projeto, migrar de estruturas genéricas para classes representa não apenas mudança técnica, mas evolução conceitual do modelo.
