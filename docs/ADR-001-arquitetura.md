# ADR-001 — Arquitetura do Sistema

## Contexto
O sistema precisa permitir evolução sem modificar vários módulos (RNF03) e permitir testes independentes de estado externo (RNF04).  
Além disso, será executado em linha de comando (CLI) e desenvolvido por uma equipe iniciante.

## Opções consideradas

### Arquivo único
Simples de implementar, porém centraliza toda a lógica em um único arquivo, dificultando manutenção e evolução.  
Qualquer nova funcionalidade exige alteração direta no mesmo arquivo, violando o RNF03.  
Também dificulta a realização de testes isolados, prejudicando o RNF04.

### MVC
Oferece boa separação entre modelo, visão e controle.  
Porém, adiciona complexidade desnecessária para um sistema simples em CLI e pode dificultar o entendimento para uma equipe iniciante.

### Arquitetura em camadas
Organiza o sistema em partes independentes com responsabilidades bem definidas.  
Facilita manutenção, evolução e testes, atendendo aos requisitos RNF03 e RNF04.

## Decisão
Foi escolhida a arquitetura em camadas, organizada da seguinte forma:

- apresentação: responsável pela interação com o usuário (CLI)
- aplicação: responsável pela lógica de negócio e regras do sistema
- infraestrutura: responsável pelo acesso a dados e serviços externos

Essa separação permite que novas funcionalidades sejam adicionadas sem modificar múltiplos módulos, atendendo o RNF03.  
Além disso, possibilita testar as regras de negócio de forma isolada, sem dependência de estado externo, atendendo o RNF04.

## Consequências

### Positivas
- Melhor organização do código
- Facilidade de manutenção e evolução
- Possibilidade de testes isolados
- Separação clara de responsabilidades

### Negativas
- Aumento da complexidade inicial
- Necessidade de disciplina na separação das camadas
