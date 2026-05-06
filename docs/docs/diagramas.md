# Atividade 4a — Materialização do Projeto

## Decomposição em camadas

### models/equipamento.py
Representa os dados dos equipamentos.

### models/emprestimo.py
Representa os dados dos empréstimos.

### repositories/repositorio_emprestimo.py
Gerencia armazenamento e consulta de dados.

### services/servico_emprestimo.py
Aplica regras de negócio.

### services/notificador.py
Responsável por notificações.

### main.py
Interação com usuário.

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


## UC02 — Registrar Devolução

```mermaid
sequenceDiagram
 actor Atendente
 participant main as main.py
 participant servico as ServicoEmprestimo
 participant repo as RepositorioEmprestimo
 participant notif as Notificador

 Atendente->>main: informa emprestimo_id
 main->>servico: registrar_devolucao(emprestimo_id)
 servico->>repo: buscar_emprestimo(emprestimo_id)
 repo-->>servico: Emprestimo

 alt empréstimo encontrado
     servico->>repo: marcar_devolvido(emprestimo_id)
     servico->>repo: marcar_disponivel(equip_id)
     servico->>notif: notificar_devolucao(email)
     servico-->>main: True
 else empréstimo não encontrado
     servico-->>main: False
 end


## UC03 — Listar Empréstimos em Atraso

```mermaid
sequenceDiagram
 actor Atendente
 participant main as main.py
 participant servico as ServicoEmprestimo
 participant repo as RepositorioEmprestimo

 Atendente->>main: solicitar_atrasados()
 main->>servico: listar_atrasados()
 servico->>repo: buscar_emprestimos_atrasados()
 repo-->>servico: lista_atrasados

 alt existem atrasados
     loop para cada empréstimo
         servico-->>main: exibir_dados(emprestimo)
     end
 else nenhum atraso
     servico-->>main: lista vazia
 end
