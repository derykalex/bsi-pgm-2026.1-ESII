# Atividade 4A — Materializar Projeto

## Decomposição em camadas

### modelos/equipamento.py
Responsável por representar os dados de equipamentos, garantindo contrato tipado.

### modelos/emprestimo.py
Representa formalmente os empréstimos.

### servicos/servico_emprestimo.py
Centraliza regras de negócio.

### servicos/notificador.py
Responsável por notificações.

### repositorios/repositorio_emprestimo.py
Gerencia persistência e consultas.

### main.py
Camada de entrada.

---

## Diagramas de sequência

### UC01 — Registrar Empréstimo

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
```

### UC02 — Registrar Devolução

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

 alt empréstimo ativo
    servico->>repo: marcar_devolvido(emprestimo_id)
    servico->>repo: marcar_disponivel(equip_id)
    servico->>notif: notificar_devolucao(email)
    servico-->>main: True
 else empréstimo já devolvido
    servico-->>main: False
 end
```

### UC03 — Listar Empréstimos em Atraso

```mermaid
sequenceDiagram
 actor Atendente
 participant main as main.py
 participant servico as ServicoEmprestimo
 participant repo as RepositorioEmprestimo

 Atendente->>main: solicita atrasados
 main->>servico: listar_atrasados()
 servico->>repo: buscar_emprestimos_atrasados()
 repo-->>servico: lista_emprestimos

 alt existem atrasados
    loop para cada empréstimo
        servico-->>main: exibir_emprestimo(atrasado)
    end
 else sem atrasados
    servico-->>main: lista_vazia
 end
```
