# ADR-001 — Arquitetura do Sistema

## Contexto
O sistema precisa permitir evolução sem modificar vários módulos (RNF03) e permitir testes independentes de estado externo (RNF04).

## Opções consideradas

### Arquivo único
Simples de implementar, mas dificulta manutenção e testes.

### MVC
Separa bem responsabilidades, mas é mais complexo e mais indicado para aplicações com interface gráfica.

### Em camadas
Organiza o sistema em partes independentes, facilitando manutenção e testes.

## Decisão
Será utilizada arquitetura em camadas com:

- apresentacao: interface com o usuário
- aplicacao: regras de negócio
- infraestrutura: acesso a dados

## Consequências
- Código mais organizado
- Facilita testes
- Facilita manutenção e evolução
