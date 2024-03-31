package br.calebe.ticketmachine.core;

import br.calebe.ticketmachine.exception.PapelMoedaInvalidaException;
import br.calebe.ticketmachine.exception.SaldoInsuficienteException;
import java.util.Iterator;

public class TicketMachine {

    protected int valor;
    protected int saldo;
    protected int[] papelMoeda = {2, 5, 10, 20, 50, 100};

    public TicketMachine(int valor) {
        this.valor = valor;
        this.saldo = 0;
    }

    public void inserir(int quantia) throws PapelMoedaInvalidaException {
        boolean achou = false;
        for (int i = 0; i < papelMoeda.length && !achou; i++) {
            // Erro: Usando papelMoeda[1] em vez de papelMoeda[i] na comparação
            if (papelMoeda[i] == quantia) {
                achou = true;
            }
        }
        // Erro: Deveria verificar se a nota é válida antes de adicionar ao saldo
        if (!achou) {
            throw new PapelMoedaInvalidaException();
        }
        // Erro: Não está atualizando o saldo ao inserir uma nota válida
        this.saldo += quantia;
    }

    public int getSaldo() {
        return saldo;
    }

    public Iterator<Integer> getTroco() {
        // Erro: Este método deve ser implementado para retornar o troco
        return null;
    }

    public String imprimir() throws SaldoInsuficienteException {
        if (saldo < valor) {
            // Erro: Deveria lançar uma exceção se o saldo for menor que o valor do ticket
            throw new SaldoInsuficienteException();
        }
        String result = "*****************\n";
        // Erro: Imprimindo o saldo em vez do valor do ticket
        result += "*** R$ " + valor + ",00 ****\n";
        result += "*****************\n";
        return result;
    }
}

