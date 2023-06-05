

package com.mycompany.main;

import java.nio.file.FileAlreadyExistsException;
import java.util.Scanner;
import java.util.Arrays;

class NenhumItemException extends RuntimeException{
    public NenhumItemException(){
        super("NenhumItemException");
    }
}

class PosicaoInvalidaException extends RuntimeException{
    public PosicaoInvalidaException(){
        super("PosicaoInvalidaException");
    }
}

interface ListaCommon {
    Object getItem( );  // throws NenhumItemException
    int tamanho();
    boolean vazia();
    Object[] toArray(); // throws NenhumItemException
}

interface ListaBasica extends ListaCommon {
    void adicionar(Object item);
    Object remover();   // throws NenhumItemException
}

interface Pilha extends ListaCommon {
    void empilhar(Object item);
    Object desempilhar();       // throws NenhumItemException   
}

class PilhaEncadeada implements Pilha 
    { 
    int tam = 0;
        class No
        {
            Object item;
            No prox;
            No(Object item, No prox)
            {
                this.item = item;
                this.prox = prox;
            }
        }
        No topo = new No(null, null);
    
       
         public void empilhar(Object item)
         {
            No novo =  new No(item, null);
            novo.prox = topo;
            topo = novo;
            tam++;
         }


         @Override
         public boolean vazia()
         { return tam == 0 ? true : false;}
         
        @Override
         public Object[] toArray()
         {
            Object[] v = new Object[tam];
            No auxs = new No(topo.item, topo.prox);
            if(tam != 0){
                for (int x = 0; x < tam; x++) {
                    v[x] = auxs.item;
                    auxs = auxs.prox;
            }
            return v;
    }
            else{
                throw new NenhumItemException();
                
            }
         }
    
          @Override
         public  Object desempilhar()
         {
            if(vazia()){
                throw new NenhumItemException();
                
         }
            else{
            Object aux = topo.item;
            No auxs =  topo;
            topo = topo.prox;
            auxs.prox = null;
            tam--;
            return aux;
            }
         }
         
          @Override
          public  Object getItem()
          {
            if(vazia())
            {
                throw new NenhumItemException();
               
            }
            return topo.item;
          }    
    }



class PilhaArray implements Pilha 
{ 
    int tam = 0;
    Object []vetor= new Object[1000];
    
    @Override
    public  void empilhar(Object item)
    {
        vetor[tam] = item;
        tam++;
    }
    
    @Override
    public boolean vazia()
    { return tam == 0 ? true : false;}

    @Override
     public  Object desempilhar()
     {
       if(vazia()){
            throw new NenhumItemException();
           
       }
        else 
        {
            int p = tam - 1;
            Object d = vetor[p];
            vetor[p] = vetor[tam--];
           return   d; 
        }

        
    }

     @Override
     public Object[] toArray()
     {
        if(vazia())
        {
            throw new NenhumItemException();
            
        }
        else{
        Object []v = new Object[tam];
        for(int a = 0; a < tam ; a++)
            v[tam - 1 - a] = vetor[a];

        return v; 
        }
     }

     @Override
    public  Object getItem()
    {
        if(!vazia()){
            int y = tam - 1;
            return vetor[y];
        }
        else {
            throw new NenhumItemException();
            
        }
    }
}

interface Fila extends ListaCommon {
    void enfileirar(Object item);
    Object desenfileirar();     // throws NenhumItemException
}

// FAZER O MESMO QUE FOI FEITO PARA Pilha
class FilaEncadeada implements Fila
    {
    int tam = 0;
        class No
        {
            Object item;
            No prox;
            No(Object item, No prox)
            {
                this.item = item;
                this.prox = prox;
            }
        }
         No inicio = new No(null, null);
         @Override
        public void enfileirar(Object item)
        {
            No novo = new No(item, null);
            if(tam == 0)
                inicio = novo;
            else
            {
                No aux = inicio;
                while(aux.prox != null)
                    aux = aux.prox;
    
                aux.prox = novo;
            }
            tam++;
        }
         @Override
        public Object desenfileirar()
        {
            if(vazia()){
                throw new NenhumItemException();
                
            }
            else{
                Object dado = inicio.item;
                No aux = inicio;
                inicio = aux.prox;
                tam--;
                return dado;
            }
        }
         @Override
        public Object getItem()
        {
            if(vazia()){
                throw new NenhumItemException();
                
            }
            else
            return inicio.item;
        }

        @Override
        public int tamanho() { return tam; }
        
        @Override
        public boolean vazia(){ return tam == 0 ? true : false;}

         @Override
        public Object[] toArray()
        {
            Object[] v = new Object[tam];
            No auxs = new No(inicio.item, inicio.prox);
            if(tam != 0){
            for (int x = 0; x < tam; x++) {
                v[x] = auxs.item;
                auxs = auxs.prox;
            }
            return v;
    }
            else{
                throw new NenhumItemException();
                
            }
        }
        }
    
class FilaArray implements Fila
{
    int tam = 0;
    Object []vetor = new Object[1000];

    @Override
        public int tamanho() { return tam; }
        
        @Override
        public boolean vazia(){ return tam == 0 ? true : false;}


     @Override
     public void enfileirar(Object item)
    {
        vetor[tam] = item;
        tam++;
    }
     @Override
    public Object desenfileirar()
    {
        if(vazia()){
        throw new NenhumItemException();
            
        }
        else
        {
            Object valor = vetor[0];
            
            vetor = Arrays.copyOfRange(vetor, 1, vetor.length);
            tam--;
            return valor;
        }
    }
    
    
     @Override
    public Object getItem()
    {
        if(vazia()){
        throw new NenhumItemException();
        
        }
        else
        return vetor[0];
    }

     @Override
    public Object[] toArray()
    {
        if(vazia())
        {
            throw new NenhumItemException();
          
        }
        else{
        Object []v = new Object[tam];
        for(int a = 0; a < tam ; a++)
            v[a] = vetor[a];

        return v; 
        }
    }
}


interface Lista extends ListaBasica {
    void adicionarInicio(Object item);
    void adicionarFim(Object item);
    void adicionar(Object item, int posicao);   // throws PosicaoInvalidaException
    Object removerInicio();         // throws NenhumItemException
    Object removerFim();            // throws NenhumItemException
    Object remover(int posicao);    // throws NenhumItemException, PosicaoInvalidaExeption
    Object getItem(int posicao);    // throws PosicaoInvalidaExeption
}

class ListaEncadeada implements Lista {
    class No
    {
        Object item;
        No prox;
        No(Object item, No prox)
        {
            this.item = item;
            this.prox = prox;
        }
    }
    No inicio = new No(null, null);
    No fim = new No(null, null);
    int tam  =0;

    @Override
    public  void adicionarFim(Object item)
    {
        No novo = new No(item, null);
        if(tam == 0)
            inicio = novo;

            fim.prox = novo;
            fim = novo;
        tam++;
    }

    @Override
    public int tamanho() { return tam; }
    
    @Override
    public boolean vazia(){ return tam == 0 ? true : false;}

    @Override
    public  void adicionarInicio(Object item)
    {
        No novo = new No(item, null);
        No aux = inicio;
        inicio = novo;
        novo.prox = aux;
        tam++;
    }

    @Override
    public void adicionar(Object valor, int posicao)
    {
         if(posicao >= 0 && posicao <= tam)
        {
            if(posicao == 0)
                adicionarInicio(valor);
            else{
                No novo = new No(valor, null);
                No auxProx = inicio.prox;
                No auxAnt = inicio;
                for(int num = 0; num < posicao-1; num++)
                    {
                        auxAnt = auxProx;
                        auxProx = auxProx.prox;
                    }
                    auxAnt.prox = novo;
                    novo.prox = auxProx;
                    tam++;
                    
            }
        }
        else
        throw new NenhumItemException();
        
    }

    @Override
    public Object removerInicio()
    {
         if(vazia()){
            throw new NenhumItemException();
            
         }
        else{
            Object dado = inicio.item;
            inicio = inicio.prox;
            tam--;
            
            return dado;
        }
    }

    @Override
    public Object removerFim()
    {
        if(vazia()){
            throw new NenhumItemException();
            
        }
        else{
            No auxAnt = inicio;
            No auxProx = inicio.prox;
            while(auxProx != null){
                auxAnt = auxProx;
                auxProx = auxProx.prox;
            }
            Object dado = auxAnt.prox.item;
            auxAnt.prox = null;
            tam--;
            
            return dado;
    }
    }

    @Override
    public Object remover(int posicao)
    {
         if(vazia())
         {
            throw new NenhumItemException();
            
    }
    else if(posicao == 0)
             return removerInicio();

     else if(posicao > tam || posicao < 0 || posicao == 1 && tam == 1)
        {
            throw new PosicaoInvalidaException();
            
        }
        else{
            No auxP = inicio.prox;
            No auxA = inicio;
            for(int num = 0; num < posicao-1; num++){
                auxA = auxP;
                auxP = auxP.prox;
            }
            Object dado = auxA.prox.item;
            auxA.prox = auxP.prox;
            tam--;
          
          return dado;
        }
    }
 

    @Override
    public Object getItem()
    {
        if(vazia()){
        throw new NenhumItemException();
       
        }
        else 
        return inicio.item;
    }
    
    @Override
    public Object getItem(int posicao)
    {
        if(vazia()){
            throw new NenhumItemException();
           
        }
        else{
            No aux = inicio;
            for(int num = 0; num < posicao-1; num++){
                aux = aux.prox;
            }
            Object dado = aux.item;
            
            return dado;
        }
    }
    
    @Override
    public Object[] toArray()
    {
        Object[] v = new Object[tam];
        No auxs = new No(inicio.item, inicio.prox);
        if(tam != 0){
            for (int x = 0; x < tam; x++) {
                v[x] = auxs.item;
                auxs = auxs.prox;
            }
            return v;
        }
        else{
            throw new NenhumItemException();
            
        }
    }
}

class ListaArray implements Lista {
    Object []vetor = new Object[1000];
    int tam =0;

     @Override
    public  void adicionarFim(Object item)
    {
        if(vazia())
            vetor[0] = item;
        else
            vetor[tam] = item;
        tam++;
    }

    @Override
    public int tamanho() { return tam; }
    
    @Override
    public boolean vazia(){ return tam == 0 ? true : false;}

    @Override
    public  void adicionarInicio(Object item)
    {
        if(vazia())
            vetor[0] = item;

        else{
            Object []v = new Object[1000];
            v[0] = item;
            for(int x = 0; x < tam; x++)
                v[x+1] = vetor[x];

                vetor = v;
        }
        tam++;
    }

    @Override
    public void adicionar(Object valor, int posicao)
    {
        if(vazia()){
        throw new NenhumItemException();
        
    }

        if(posicao < 0 || posicao > tam)
        throw new PosicaoInvalidaException();

        else
        {
            Object []v = new Object[1000];
            v[posicao] = valor;
            for(int w = posicao; w < tam; w++)
                v[w+1] = vetor[w]; 
             

            for(int x = posicao; x <= tam; x++)
                vetor[x] = v[x];
                 
                
                 
        }
    tam++;
    }
    

    @Override
    public Object removerInicio()
    {
         if(vazia()){
           throw new NenhumItemException();
            
        }
        else{
        Object valor = vetor[0];
            vetor = Arrays.copyOfRange(vetor, 1, vetor.length);
            tam--;
            
            return valor;
        }
    }

    @Override
    public Object removerFim()
    {
        if(vazia()){
            throw new NenhumItemException();
             
        }
        else{
             
             return vetor[tam--];
        }
    }

    @Override
    public Object remover(int posicao)
    {
        if(vazia())
        {
            throw new NenhumItemException();
             
        }
        else if(posicao == 0)
           return removerInicio();


        else if(posicao > tam || posicao < 0 || posicao == 1 && tam == 1)
        {
            throw new PosicaoInvalidaException();
            
        }
        

        else{
            Object dado = vetor[posicao];
            for(int i = posicao; i < tam-1; i++)
                {
                    vetor[i] = vetor[i+1];
                }
                    tam--;
                    
                    return dado;
                    
                }
        }
    

    @Override
    public Object getItem()
    {
         if(vazia()){
            throw new NenhumItemException();
                
         }
        else{ 
        return vetor[0];
        }
    }
    
    @Override
    public Object getItem(int posicao)
    {
        if(vazia()){
            throw new NenhumItemException();
                
         }
        else{ 

        return vetor[posicao];
        }
    }
    
    @Override
    public Object[] toArray()
    {
        Object []v = new Object[tam];
        for(int a = 0; a < tam ; a++)
            v[a] = vetor[a];

        return v; 
    }
}

class PilhaAdapter implements ListaBasica {
    
    private final Pilha pilha;

    public PilhaAdapter(Pilha pilha) {
        this.pilha = pilha;
    }    
    
    @Override
    public void adicionar(Object item) {
        pilha.empilhar(item);
    }

    @Override
    public Object remover() {
        return pilha.desempilhar();
    }

    @Override
    public Object getItem() {
        return pilha.getItem();
    }

    @Override
    public int tamanho() {
        return pilha.tamanho();
    }

    @Override
    public boolean vazia() {
        return pilha.vazia();
    }

    @Override
    public Object[] toArray() {
        return pilha.toArray();
    }    
}

class Main {

    private final ListaBasica lista;
    
    public Main(ListaBasica lista) {
        this.lista = lista;
    }
    
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        Main main;
        String token;
        Object valor;
        
        token = in.next();
        
        switch (token) {
            case "PE": main = new Main(new PilhaAdapter(new PilhaEncadeada())); break;
            case "PA": main = new Main(new PilhaAdapter(PilhaArray())); break;
            case "FE": main = new Main(new FilaAdapter(FilaEncadeada())); break;
            case "FA": main = new Main(new FilaAdapter(FilaArray())); break;
            case "LE": main = new Main(new ListaEncadeada()); break;
            default: main = new Main(new ListaArray());
        }
        
        while (!token.equals("Q")) {
            switch(token) {
                case "A":   // adiciona um item
                    valor = in.nextInt();
                    main.lista.adicionar(valor);
                    break;      
                case "R":   // remove um item
                    try {
                        main.lista.remover();
                    } catch(NenhumItemException e) {
                        System.out.println(e.getMessage());
                    }
                    break;
                case "G":   // retorna um item, sem remover
                    try {
                        valor = (Integer) main.lista.getItem();
                        System.out.println(valor);
                    } catch (NenhumItemException e) {
                        System.out.println(e.getMessage());
                    }
                    break;
                case "T":   // numero de itens na estrutura
                    System.out.println(main.lista.tamanho());
                    break;
                case "V":   // indica se a estrutura esta vazia
                    System.out.println(main.lista.vazia());
                    break;
                case "P":   // imprime os itens da estrutura, sem remover
                    try {
                        Object valores[] = main.lista.toArray();
                        if (valores != null) 
                            for(Object item: valores)
                                System.out.println(item);
                    } catch (NenhumItemException e) {
                        System.out.println(e.getMessage());
                    }    
                    break;
            }
            token = in.next();
        }
        in.close();
    }
}

