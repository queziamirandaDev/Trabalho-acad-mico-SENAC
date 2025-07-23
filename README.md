🧠 Conceito geral

° Neste trabalho apresentamos um simulador de lista de tarefas onde a pessoa cadastra as tarefas podendo ver totas  que cadastrou e, tambem, marcar as mesmas como concluida ou pendentes(sera possivel filtrar todas pendentes e concluidas)


🧱 1. Estrutura da Classe Tarefa

1º Passo

°Criar uma classe tarefa com os seguintes Atributos:

    public class Tarefa {
    private String descricao;
    private String status;
    private LocalDate deadline; 

   
 °Fazer um construtor com todos os atributos:

     public Tarefa(String descricao, String status, LocalDate deadline) {
        this.descricao = descricao;
        this.status = status;
        this.deadline = deadline;
    }
    
  2º Passo
  
  °Método para exibir um resuo amigavel da tarefa:

    public String getResumoTarefa() {
        return "To Do: " + descricao + "\n"
                + "Status: " + status + "\n"
                + "Deadline: " + deadline + "\n";
    }


3º Passo

 °Aplicando gets e sets:
 
       public String getDescricao() {
        return descricao;
    }

    public void setDescricao(String descricao) {
        this.descricao = descricao;
    }

    // Getter e Setter para status
    public String getStatus() {
        return status;
    }

    public void setStatus(String status) {
        this.status = status;
    }

    // Getter e Setter para deadline
    public LocalDate getDeadline() {
        return deadline;
    }

    public void setDeadline(LocalDate deadline) {
        this.deadline = deadline;
    }
  


🧱 1. Estrutura da SubClasse Agenda

1º Passo

  ° Criar a classe Agenda e adicionar o metodo Main e dentro desse metodo colocaremos a função scanner e ArrayList para a armazenagem:

    public class Agenda {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in); // Para leitura de dados do teclado
        ArrayList<Tarefa> tarefas = new ArrayList<>(); 

2º Passo

  ° Adicionando a varial int opcao faremos um loop com do While

        int opcao;   // Armazena a opção escolhida pelo usuário no menu

        // Loop principal do menu, só termina quando o usuário digita 0
        do {
            // Exibição do menu de opções
            System.out.println("\nBem-vindo à sua agenda!");
            System.out.println("--------------------------------");
            System.out.println("1 - Adicionar tarefa");
            System.out.println("2 - Listar todas");
            System.out.println("3 - Marcar tarefa como concluída");
            System.out.println("4 - Tarefas pendentes");
            System.out.println("5 - Tarefas em andamento");
            System.out.println("6 - Tarefas concluídas");
            System.out.println("0 - Sair");
            System.out.println("--------------------------------");
            System.out.print("Escolha uma opção: ");

            // Valida se a entrada é um número inteiro
            while (!scanner.hasNextInt()) {
                System.out.println("Por favor, digite um número válido.");
                scanner.next(); // Limpa entrada inválida
            }

3° Passo 

  ° Declarar a variavel opcao colocando a função scanner para ler a opção e usar os metodos  swith case 
  (colocar os dados)  e try para aplicar um padrão de recebimento de informação no prompt, adicionamos tambem o If Else para termos condiçoes assim teremos controle das inforções que o usuario ira aplicar:

            opcao = scanner.nextInt(); // Lê a opção
            scanner.nextLine(); // Limpa o buffer após a leitura do número
            // Switch com as opções do menu
            switch (opcao) {

                // Adicionar uma nova tarefa
                case 1:
                    System.out.print("Digite a descrição da tarefa: ");
                    String descricao = scanner.nextLine(); // Lê a descrição

                    System.out.print("Digite a data de entrega (formato: DD-MM-AAAA): ");
                    String dataStr = scanner.nextLine(); // Lê a data como string

                    LocalDate deadline; // Variável para armazenar a data convertida
                    DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy"); // Define o formato esperado

                    try {
                        deadline = LocalDate.parse(dataStr, formatter); // Converte a string em data
                    } catch (DateTimeParseException e) {
                        System.out.println("Formato de data inválido. Tarefa não adicionada.");
                        break; // Volta ao menu se a data estiver errada
                    }
                   // Cria a tarefa usando os setters
                    Tarefa novaTarefa = new Tarefa("", "", null);
                    novaTarefa.setDescricao(descricao);
                    novaTarefa.setStatus("Pendente");
                    novaTarefa.setDeadline(deadline);

                    // Adiciona a tarefa à lista
                    tarefas.add(novaTarefa);

                    // Confirmação ao usuário
                    System.out.println("Tarefa adicionada com sucesso! \n Data de entrega: " + novaTarefa.getDeadline().format(formatter));
                    break;

                // Listar todas as tarefas
                case 2:
                    System.out.println("\n--- Todas as tarefas ---");
                    if (tarefas.isEmpty()) {
                        System.out.println("Nenhuma tarefa cadastrada.");
                    } else {
                        for (int i = 0; i < tarefas.size(); i++) {
                            System.out.println("[" + i + "]\n" + tarefas.get(i).getResumoTarefa());
                        }
                    }
                    break;

                // Atualizar o status de uma tarefa
                case 3:
                    if (tarefas.isEmpty()) {
                        System.out.println("Nenhuma tarefa cadastrada.");
                        break;
                    }
                     // Mostra a lista de tarefas com índice
                    System.out.println("\nTarefas cadastradas:");
                    for (int i = 0; i < tarefas.size(); i++) {
                        Tarefa t = tarefas.get(i);
                        System.out.println("[" + i + "] " + t.getDescricao() + " (" + t.getStatus() + ")");
                    }

                    // Solicita o índice da tarefa a ser modificada
                    System.out.print("Digite o número da tarefa para atualizar o status: ");
                    if (!scanner.hasNextInt()) {
                        System.out.println("Entrada inválida.");
                        scanner.nextLine(); // limpa o buffer
                        break;
                    }
                    int indice = scanner.nextInt();
                    scanner.nextLine();

                    // Verifica se o índice é válido
                    if (indice >= 0 && indice < tarefas.size()) {
                        // Exibe as opções de status
                        System.out.println("Escolha o novo status:");
                        System.out.println("1 - Em andamento");
                        System.out.println("2 - Concluída");
                        System.out.println("3 - Cancelada");

                        int escolhaStatus = scanner.nextInt();
                        scanner.nextLine(); // limpa o buffer

                        // Converte número em texto
                        String novoStatus = switch (escolhaStatus) {
                            case 1 -> "Em andamento";
                            case 2 -> "Concluída";
                            case 3 -> "Cancelada";
                            default -> "Pendente";
                        };

                        tarefas.get(indice).setStatus(novoStatus); // Atualiza o status da tarefa
                        System.out.println("Status atualizado para: " + novoStatus);
                    } else {
                        System.out.println("Índice inválido.");
                    }
                    break;

                // Listar tarefas pendentes
                case 4:
                    System.out.println("\n--- Tarefas pendentes ---");
                    for (Tarefa t : tarefas) {
                        if (t.getStatus().equalsIgnoreCase("Pendente")) {
                            System.out.println(t.getResumoTarefa());
                        }
                    }
                    break;

                // Listar tarefas em andamento
                case 5:
                    System.out.println("\n--- Tarefas em andamento ---");
                    for (Tarefa t : tarefas) {
                        if (t.getStatus().equalsIgnoreCase("Em andamento")) {
                            System.out.println(t.getResumoTarefa());
                        }
                    }
                    break;

                // Listar tarefas concluídas
                case 6:
                    System.out.println("\n--- Tarefas concluídas ---");
                    for (Tarefa t : tarefas) {
                        if (t.getStatus().equalsIgnoreCase("Concluída")) {
                            System.out.println(t.getResumoTarefa());
                        }
                    }
                    break;

                // Encerrar o programa
                case 0:
                    System.out.println("Encerrando o programa...");
                    break;

                // Opção inválida
                default:
                    System.out.println("Opção inválida.");
            }

        } while (opcao != 0); // Continua até o usuário digitar 0

        scanner.close();

            





