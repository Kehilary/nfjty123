
package br.cefetmg.listas.lista09.r1004;

import java.util.Scanner;

enum ErroLista {
    INDICE_INVALIDO("PosicaoInvalidaException"),
    VAZIA("NenhumItemException"),
    SEM_ERRO("NenhumErro");
    
    String msgErro;
    
    ErroLista(String msg) {
        msgErro = msg;
    }
    
    public String getMessage() {
        return msgErro;
    }
}

class ErroListaWrapper {
    private ErroLista erro;
    
    public ErroListaWrapper() {
        this(ErroLista.SEM_ERRO);
    }
    
    public ErroListaWrapper(ErroLista erro) {
        this.erro = erro;
    }

    public ErroLista getErro() {
        return erro;
    }

    public void setErro(ErroLista erro) {
        this.erro = erro;
    }
}

class Lista{
    class No{
        Integer item;
        No prox;
        No ant;
        No(Integer valor, No proxs, No ants){
            item = valor;
            prox = proxs;
            ant = ants;
        }
    }
    int tam;
    No inicio = new No(null, null, null);
    No fim = new No(null, null, null);

    void adicionarFim(Integer valor){
        No novo = new No(valor, null, null);
        if(vazia()){
            inicio = novo;
            fim = novo;
        }
        else{
            No aux = fim;
            novo.ant = aux;
            aux.prox = novo;
            fim = novo; 
        }
        tam++;
    }
    void adicionarInicio(Integer valor){
        No novo = new No(valor, null, null);
        if(vazia()){
            inicio = novo;
            fim = novo;
        }
        else{
            No aux = inicio;
            novo.prox = aux;
            aux.ant = novo;
            inicio = novo;
        }
        tam++;
    }
    void adicionar(Integer valor, int posicao, ErroListaWrapper erro){
        posicao = posicao - 1;
        No novo = new No(valor, null, null);
        if(vazia())
        {
            inicio = novo;
            fim = novo;
        }
        else{
            No aux = inicio;
            int x = 0;

            if(posicao < (tam/2)){
                aux = fim;
                x = tam;
            }

            while(x >= 0 && x <=tam && x != posicao){
                if(x < posicao){
                    x++;
                    aux = aux.prox;
                }
                else if(x > posicao){
                    x--;
                    aux = aux.ant;
                }
            }
            tam++;
            erro.setErro(ErroLista.SEM_ERRO);
        }
    }
    void removerInicio(ErroListaWrapper erro){
        if(vazia())
            erro.setErro(ErroLista.VAZIA);

        else{
            No aux = inicio;
	        inicio = aux.prox;
	        inicio.ant = null;
	        tam--;
            erro.setErro(ErroLista.SEM_ERRO);
        }
    }
void remover(ErroListaWrapper erro){
            No aux = null;
            No atual = inicio;
            while((atual != null)){ 
                aux = atual;
                atual = atual.prox;
    }
        if(atual == null)
            erro.setErro(ErroLista.VAZIA);
    
    else{
        if(atual == inicio)
            inicio = atual.prox;
        
        else
            aux.prox = atual.prox;
        

        tam--;
        erro.setErro(ErroLista.SEM_ERRO);
        } 
        
    void removerFim(ErroListaWrapper erro){
        if(vazia())
            erro.setErro(ErroLista.VAZIA);

        else{
            No aux = fim;
	        fim = aux.ant;
	        fim.prox = null;
	        tam--;
            erro.setErro(ErroLista.SEM_ERRO);
        }
    }

    int tamanho(){
        return tam;
    }

    boolean vazia(){
        return tam == 0 ? true : false;
    }

    Integer[] toArray() {
        Integer[] v = new Integer[tam];
        No auxs = new No(inicio.item, inicio.prox, null);
        if(tam != 0){
        for (int x = 0; x < tam; x++) {
            v[x] = auxs.item;
            auxs = auxs.prox;
        }
        return v;
}
        else
            return null;
    }

    Integer getItem(int posicao, ErroListaWrapper erro){
        if(vazia())
            erro.setErro(ErroLista.VAZIA);
        else{
            No aux = inicio;
            int x = 0;
            while(x < posicao){
                aux = aux.prox;
                x++;
            }
            erro.setErro(ErroLista.SEM_ERRO);
            return aux.prox.item;
        }
    }

    Integer getItem(ErroListaWrapper erro){
        if(vazia())
            erro.setErro(ErroLista.VAZIA);
        else 
            erro.setErro(ErroLista.SEM_ERRO);
            return tam;
    }

}

class Main {

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        Lista lista = new Lista();
        String token;
        Integer valor;
        int posicao;
        ErroListaWrapper erro = new ErroListaWrapper();
        
        token = in.next();
        while (!token.equals("Q")) {
            erro.setErro(ErroLista.SEM_ERRO);
            switch(token) {
                case "AF":
                    valor = in.nextInt();
                    lista.adicionarFim(valor);
                    break;
                case "AI":
                    valor = in.nextInt();
                    lista.adicionarInicio(valor);
                    break;                    
                case "AP":
                    posicao = in.nextInt();
                    valor = in.nextInt();
                    lista.adicionar(valor, posicao, erro);
                    if (erro.getErro() != ErroLista.SEM_ERRO)
                        System.out.println(erro.getErro().getMessage());
                    break;          
                case "RI":
                    lista.removerInicio(erro);
                    if (erro.getErro() != ErroLista.SEM_ERRO)
                        System.out.println(erro.getErro().getMessage());
                    break;
                case "RF":
                    lista.removerFim(erro);
                    if (erro.getErro() != ErroLista.SEM_ERRO)
                        System.out.println(erro.getErro().getMessage());
                    break;
                case "RP":                    
                    posicao = in.nextInt();
                    lista.remover(posicao, erro);
                    if (erro.getErro() != ErroLista.SEM_ERRO)
                        System.out.println(erro.getErro().getMessage());
                    break;
                case "G":
                    valor = lista.getItem(erro);
                    if (erro.getErro() != ErroLista.SEM_ERRO)
                        System.out.println(erro.getErro().getMessage());
                    else
                        System.out.println(valor);
                    break;
                case "GP":
                    posicao = in.nextInt();
                    valor = lista.getItem(posicao, erro);
                    if (erro.getErro() != ErroLista.SEM_ERRO)
                        System.out.println(erro.getErro().getMessage());
                    else
                        System.out.println(valor);
                    break;
                case "T":
                    System.out.println(lista.tamanho());
                    break;
                case "V":
                    System.out.println(lista.vazia());
                    break;
                case "P":
                    Integer valores[] = lista.toArray();
                    if (valores != null) {
                        for(Integer item: valores)
                            System.out.println(item);
                    }
                    break;
            }
            token = in.next();
        }   
    }
}

