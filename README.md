# Simulador de Lista de Tarefas

## 🧠 Conceito Geral

Este projeto em Java simula uma lista de tarefas, permitindo ao usuário:

* Cadastrar tarefas com descrição, status e data de entrega;
* Visualizar todas as tarefas;
* Atualizar o status das tarefas para "Pendente", "Em andamento", "Concluída" ou "Cancelada";
* Filtrar tarefas por status;
* Receber alerta de tarefas em atraso.

---

## 📂 Estrutura de Arquivos

```
SimuladorTarefas/
├── README.md           # Documentação do projeto
└── src/
    ├── Tarefas.java    # Superclasse: define atributos e comportamento básico de uma tarefa
    ├── Personal.java   # Subclasse: tarefas pessoais
    ├── Study.java      # Subclasse: tarefas de estudo
    └── Main.java       # Classe principal: interface de usuário e lógica de controle
```

> **Observação:** Há referência a `Work` em `Main.java`. Caso exista `Work.java`, adicione no diretório `src/` como outra subclasse de `Tarefas`.

---

## 🧱 Descrição dos Módulos

* **Tarefas.java**

  * Atributos: `descricao`, `status`, `deadline` (`LocalDate`).
  * Construtor: inicializa os campos.
  * `getResumoTarefa()`: retorna informações básicas e alerta de atraso.
  * Getters e setters para manipulação dos atributos.

* **Personal.java**

  * Subclasse de `Tarefas` para tarefas pessoais.
  * Herdar construtor de `Tarefas`.

* **Study.java**

  * Subclasse de `Tarefas` para tarefas de estudo.
  * Herdar construtor de `Tarefas`.

* **Main.java**

  * Método `main`: ponto de entrada.
  * Cria lista de `Tarefas` e pré-popula alguns exemplos de `Personal`, `Study` (e `Work`, se aplicável).
  * Loop de menu com opções:

    1. Adicionar nova tarefa (define tipo, descrição e deadline).
    2. Listar todas as tarefas.
    3. Atualizar status de uma tarefa existente.
    4. Exibir somente tarefas pendentes.
    5. Exibir somente tarefas em andamento.
    6. Exibir somente tarefas concluídas.
    7. Sair.
  * Validações de entrada numérica e de formato de data.

---

## 🚀 Tecnologias

* Java 11+ (usa `java.time.LocalDate` e `java.time.format`)
* Biblioteca padrão do JDK sem dependências adicionais

---

## ⚙️ Como Executar

1. **Clone** o repositório:

   ```bash
   git clone https://seu-repositorio.git
   cd SimuladorTarefas
   ```
2. **Compile** os arquivos Java:

   ```bash
   javac src/*.java
   ```
3. **Execute** a aplicação:

   ```bash
   java -cp src Main
   ```

---

## 🎯 Funcionalidades

* **Adicionar Tarefa**: descrição, escolha de tipo e deadline;
* **Listar Tarefas**: exibe todas com resumo e alerta de atraso;
* **Atualizar Status**: altera estado de uma tarefa por índice;
* **Filtrar Tarefas**: pendentes, em andamento ou concluídas;
* **Sair**: encerra o programa.

---

## 🤝 Contribuição

1. Fork este projeto.
2. Crie uma branch: `git checkout -b feature/nome-da-feature`.
3. Commit suas mudanças: `git commit -m 'Descrição da mudança'`.
4. Envie para o repositório remoto: `git push origin feature/nome-da-feature`.
5. Abra um Pull Request descrevendo as alterações.

---

## 📄 Licença

Este projeto está licenciado sob a [MIT License](LICENSE).





