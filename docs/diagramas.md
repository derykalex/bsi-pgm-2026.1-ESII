# Atividade 4a — Materialização do Projeto

## Decomposição em camadas

### models/equipamento.py
Responsável por representar os equipamentos do sistema como entidade de domínio.
Fica na camada de modelo porque guarda apenas dados e regras básicas do equipamento.

### models/emprestimo.py
Responsável por representar os empréstimos realizados.
Fica na camada de modelo porque define a estrutura dos dados de empréstimo.

### repositories/repositorio_emprestimo.py
Responsável por armazenar, buscar e atualizar dados de equipamentos e empréstimos.
Fica na camada de repositório porque centraliza acesso aos dados.

### services/servico_emprestimo.py
Responsável pelas regras de negócio dos empréstimos e devoluções.
Fica na camada de serviço porque coordena processos e aplica regras.

### services/notificador.py
Responsável por enviar notificações ao usuário.
Fica na camada de serviço porque executa comunicação externa.

### main.py
Responsável pela interação com o atendente.
Fica na camada principal porque controla entrada e saída do sistema.

---

# Diagramas de sequência

## UC01 — Registrar Empréstimo

```mermaid
sequenceDiagram
 actor Atendente
 participant main as main.py
 participant servico as ServicoEmprestimo
 participant repo as RepositorioEmprestimo
 participant notif as Notificador

 Atendente->>main: informa equip_id, nome, email, dias
 main->>servico: registrar(equip_id, nome, email, dias)
 servico->>repo: buscar_equipamento(equip_id)
 repo-->>servico: Equipamento

 alt equipamento disponível
     servico->>repo: salvar_emprestimo(emprestimo)
     servico->>repo: marcar_indisponivel(equip_id)
     servico->>notif: notificar_emprestimo(email, data_devolucao)
     servico-->>main: True
 else equipamento indisponível
     servico-->>main: False
 end
