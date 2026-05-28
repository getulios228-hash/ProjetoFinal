sistema-gestao-projetos/
└── src/
    ├── model/
    │   ├── Projeto.java
    │   ├── Tarefa.java
    │   ├── Colaborador.java
    │   ├── Desenvolvedor.java
    │   ├── Analista.java
    │   └── Designer.java
    │
    ├── service/
    │   ├── Equipe.java
    │   └── GerenciadorProjetos.java
    │
    └── Main.java 
    package model;

import java.util.ArrayList;
import java.util.List;

public class Projeto {
    private String nome;
    private String status;
    private List<Tarefa> tarefas;

    public Projeto(String nome) {
        this.nome = nome;
        this.status = "Em andamento";
        this.tarefas = new ArrayList<>();
    }

    public void adicionarTarefa(Tarefa tarefa) {
        tarefas.add(tarefa);
    }

    public void atualizarStatus() {
        boolean todasConcluidas = true;

        for (Tarefa t : tarefas) {
            if (!t.isConcluida()) {
                todasConcluidas = false;
                break;
            }
        }

        this.status = todasConcluidas ? "Concluído" : "Em andamento";
    }

    public String getNome() {
        return nome;
    }

    public String getStatus() {
        return status;
    }

    public List<Tarefa> getTarefas() {
        return tarefas;
    }
}package model;

public class Tarefa {
    private String descricao;
    private boolean concluida;
    private Colaborador responsavel;

    public Tarefa(String descricao) {
        this.descricao = descricao;
        this.concluida = false;
    }

    public void concluir() {
        this.concluida = true;
    }

    public boolean isConcluida() {
        return concluida;
    }

    public void setResponsavel(Colaborador responsavel) {
        this.responsavel = responsavel;
    }

    public String getDescricao() {
        return descricao;
    }

    public Colaborador getResponsavel() {
        return responsavel;
    }
}package model;

public abstract class Colaborador {
    protected String nome;

    public Colaborador(String nome) {
        this.nome = nome;
    }

    public String getNome() {
        return nome;
    }

    public abstract void executarTarefa(Tarefa tarefa);
}package model;

public class Desenvolvedor extends Colaborador {

    public Desenvolvedor(String nome) {
        super(nome);
    }

    @Override
    public void executarTarefa(Tarefa tarefa) {
        System.out.println(nome + " desenvolvendo: " + tarefa.getDescricao());
        tarefa.concluir();
    }
}package model;

public class Analista extends Colaborador {

    public Analista(String nome) {
        super(nome);
    }

    @Override
    public void executarTarefa(Tarefa tarefa) {
        System.out.println(nome + " analisando: " + tarefa.getDescricao());
        tarefa.concluir();
    }
}package model;

public class Designer extends Colaborador {

    public Designer(String nome) {
        super(nome);
    }

    @Override
    public void executarTarefa(Tarefa tarefa) {
        System.out.println(nome + " criando interface: " + tarefa.getDescricao());
        tarefa.concluir();
    }
}package service;

import model.Colaborador;
import model.Tarefa;

import java.util.ArrayList;
import java.util.List;

public class Equipe {
    private List<Colaborador> colaboradores = new ArrayList<>();

    public void adicionarColaborador(Colaborador c) {
        colaboradores.add(c);
    }

    public List<Colaborador> getColaboradores() {
        return colaboradores;
    }

    public void distribuirTarefa(Tarefa tarefa, Colaborador c) {
        tarefa.setResponsavel(c);
        System.out.println("Tarefa '" + tarefa.getDescricao() + "' atribuída a " + c.getNome());
    }
}package service;

import model.Projeto;
import model.Tarefa;

public class GerenciadorProjetos {

    public void exibirStatusProjeto(Projeto projeto) {
        projeto.atualizarStatus();

        System.out.println("\n=== Projeto: " + projeto.getNome() + " ===");
        System.out.println("Status: " + projeto.getStatus());

        for (Tarefa t : projeto.getTarefas()) {
            System.out.println("- Tarefa: " + t.getDescricao() +
                    " | Concluída: " + t.isConcluida() +
                    " | Responsável: " +
                    (t.getResponsavel() != null ? t.getResponsavel().getNome() : "Não definido"));
        }
    }
}package service;

import model.Projeto;
import model.Tarefa;

public class GerenciadorProjetos {

    public void exibirStatusProjeto(Projeto projeto) {
        projeto.atualizarStatus();

        System.out.println("\n=== Projeto: " + projeto.getNome() + " ===");
        System.out.println("Status: " + projeto.getStatus());

        for (Tarefa t : projeto.getTarefas()) {
            System.out.println("- Tarefa: " + t.getDescricao() +
                    " | Concluída: " + t.isConcluida() +
                    " | Responsável: " +
                    (t.getResponsavel() != null ? t.getResponsavel().getNome() : "Não definido"));
        }
    }
}
