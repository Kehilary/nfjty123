
package com.mycompany.mavenproject1;

import java.util.Scanner;

abstract class Pilha {
    
     class No
    {
        Object item;
        No prox;
        No(Object item, No prox)
        {
            this.item = item;
            this.prox = prox;
        }
        No(Object item)
        {
            this.item = item;
        }
    }
    
    
    public abstract void empilhar(Object item);
    
    public abstract Object desempilhar();
    
    public abstract Object getItem();
    
    
    public abstract int tamanho();
    

    public abstract boolean vazia();
    
    public abstract Object[] toArray();
}

class PilhaEncadeada extends Pilha
{ 
     int tam = 0;
    No topo = new No(null, null);
    @Override
     public  void empilhar(Object item)
     {
        No novo =  new No(item, null);
        novo.prox = topo;
        topo = novo;
        tam++;
     }
     
      @Override
      public  boolean vazia()
      {
          return tam == 0 ? true: false;
      }
     
     @Override
     public  int tamanho()
     {
         return tam;
     }
     
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
        else
            return null;
     }

      @Override
     public  Object desempilhar()
     {
        if(tam == 0)
            return null;
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
        return topo.item;
      }
      
      
}


class PilhaArray extends Pilha 
{ 
   int  tam = -1;
    Object []vetor= new Object[1000];
    
    @Override
    public  void empilhar(Object item)
    {
         if(tam < vetor.length - 1) 
            vetor[++tam] = item;

    }
    
    @Override
     public  Object desempilhar()
     {
       if(vazia())
            return null;
        else
        {
        Object x = vetor[--tam];
        return x;
        }
    }

     @Override
     public Object[] toArray()
     {
        return vetor;
     }

     @Override
    public  Object getItem()
    {
        if(vazia())
            return null;
        else
            return vetor[tam--];
    }
    
@Override
      public boolean vazia()
      {
         return tam == -1 ? true : false;
      }
    
 @Override
     public  int tamanho()
     {
         return tam;
     }
      
}

class Main {

    private Pilha pilha;

    public Main(Pilha pilha) {
        this.pilha = pilha;
    }

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        Main main;
        String token;
        Object valor;
        
        token = in.next();

        if (token.equals("pe"))
            main = new Main(new PilhaEncadeada());
        else
            main = new Main(new PilhaArray());

        while (!token.equals("Q")) {
            switch(token) {
                case "E":
                    valor = in.nextInt();
                    main.pilha.empilhar(valor);
                    break;
                case "D":
                    valor = main.pilha.desempilhar();
                    if (valor == null)
                        System.out.println("NenhumItemException");
                    break;
                case "G":
                    valor = main.pilha.getItem();
                    if (valor != null)
                        System.out.println(valor);
                    else
                        System.out.println("NenhumItemException");
                    break;
                case "T":
                    System.out.println(main.pilha.tamanho());
                    break;
                case "V":
                    System.out.println(main.pilha.vazia());
                    break;
                case "P":
                    Object valores[] = main.pilha.toArray();
                    if (valores != null) {
                        for(Object item: valores)
                            System.out.println(item);
                    }
                    break;
            }
            token = in.next();
        }
    }
}

