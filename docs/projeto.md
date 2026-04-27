# Documento de Projeto
## Sistema de Gestão de Empréstimo de Equipamentos — UFRA Paragominas

**Versão:** 1.0  
**Data:** Março de 2025  
**Responsável:** João Silva (Desenvolvedor Backend)

---

## 1. Visão Geral da Arquitetura

O sistema foi desenvolvido como uma aplicação Python de linha de comando (CLI).  
A versão 1.0 concentra toda a lógica em um único arquivo (`emprestimos.py`) como estratégia para entrega rápida dentro do prazo estabelecido.

**Decisão de projeto registrada:**  
A equipe reconhece que a ausência de separação em camadas representa dívida técnica intencional.  
A refatoração para uma arquitetura em camadas (apresentação, aplicação e infraestrutura) está planejada para a versão 2.0, conforme documentado no ADR-001.

---

## 2. Estrutura Atual (v1.0)


emprestimos/
└── emprestimos.py


Todo o comportamento do sistema (entrada de dados, regras de negócio e manipulação de dados) está centralizado neste único arquivo.

---

## 3. Diagrama de Classes (v1.0)


┌─────────────────────────────────────────────────┐
│ Sistema │
├─────────────────────────────────────────────────┤
│ │
│ + registrar(equipamento_id, usuario_nome, │
│ usuario_email, dias) : bool │
│ + devolver(emprestimo_id) : void │
│ + listar_atrasados() : void │
│ │
│ [acessa diretamente as variáveis globais │
│ equipamentos[] e emprestimos_registrados[]] │
└─────────────────────────────────────────────────┘

Variáveis globais (fora da classe):
equipamentos : list[dict]
emprestimos_registrados : list[dict]


> **Observação:** O uso de variáveis globais e estruturas baseadas em dicionários foi adotado para acelerar o desenvolvimento inicial, porém reduz a modularidade, testabilidade e manutenção do sistema.

---

## 4. Decisões de Projeto Registradas

| ID | Decisão | Justificativa | Consequência conhecida |
|---|---|---|---|
| DP01 | Código em arquivo único | Rapidez na implementação inicial | Ausência de separação de responsabilidades |
| DP02 | Dados em listas de dicionários | Evitar dependência de banco de dados | Falta de tipagem e validação estruturada |
| DP03 | Notificação via print() | Ambiente sem suporte a envio de e-mail | Não há envio real de notificações |
| DP04 | Ausência de testes automatizados | Restrição de tempo na v1.0 | Alto risco de regressão |
| DP05 | Cálculo de multa com if/elif | Simplicidade inicial | Violação do princípio OCP (Open/Closed Principle) |

---

## 5. Dívida Técnica Registrada

| ID | Problema | Impacto | Prioridade |
|---|---|---|---|
| DT01 | Ausência de arquitetura em camadas | Baixa manutenibilidade | Alta |
| DT02 | Uso de variáveis globais | Alto acoplamento | Alta |
| DT03 | Mistura de lógica de negócio com saída (print) | Baixa testabilidade | Alta |
| DT04 | Lógica de cálculo duplicada | Risco de inconsistência | Alta |
| DT05 | Ausência de testes automatizados | Risco de regressão | Alta |
| DT06 | Estrutura condicional rígida para tipos | Baixa extensibilidade | Média |
| DT07 | Uso de dicionários em vez de entidades | Falta de modelagem de domínio | Média |

---

## 6. Tecnologias Utilizadas

| Tecnologia | Versão | Uso |
|---|---|---|
| Python | 3.11 | Implementação do sistema |
| datetime | nativa | Manipulação de datas |
| Git | 2.x | Controle de versão |
| GitHub | — | Hospedagem do repositório |

---

## 7. Testes

Testes automatizados não foram implementados na versão 1.0.  
Está previsto para a versão 2.0 o uso de testes unitários com pytest, permitindo validação isolada das regras de negócio.

---

## 8. Histórico de Versões

| Versão | Data | Responsável | Descrição |
|---|---|---|---|
| 1.0 | Mar/2025 | João Silva | Versão inicial funcional com dívida técnica registrada |
