<!DOCTYPE html>
<html>
    <head>
        <title>Cadastro Funcionário</title>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <link rel="stylesheet" href="estilos.css">
        <link rel="icon" href="leme.png" type="image/webp">
    </head>
    <body>
         <header id="headerUsuario">
             <h1 id="altoMare">Alto Mare</h1>
            <h2 id="embarcacoes">EMBARCAÇÕES</h2>
            <img id="leme" src="leme.png" />
            <div id="linha"></div>
        </header>
        <div id="barraDeTarefas">
            <div id="imagemBarra">
           <img class="imgg" src="funcionarios.png">
           <img class="imgg" src="passageiros.webp">
           <img class="imgg" src="pacotes.png">
           <img class="imgg" src="iconeSeguranca.png">
           <img class="imgg" src="cronograma.png">
            </div>
        </div>
        <h1 id="cadastro">Cadastro Passageiro</h1>
        <div id="dados">
        <form name="formInsereFuncionario" method="post">
                <input type='hidden' name='table' value='funcionario'>
                <input type='hidden' name='acao' value='gravar'>
                    <tr>
                        <td>
                            Nome:
                        </td>
                        <td>
                            <input type='text' name='nome' placeholder="digite o nome completo">
                        </td>
                    </tr>
                    <tr>
                        <td>
                           Data de nascimento:
                        </td>
                        <td>
                            <input type="date" name="dataAdmissao" value="">
                           
                        </td>
                    </tr>
                    <tr>
                        <td>
                            Sexo:
                        </td>
                        <td>
                            <select name="sexo">
                                <option value="">Escolher</option>
                                <option value="masculino">Maculino</option>
                                <option value="feminino">Feminino</option>
                                <option value="naoInformado">Prefiro não informar</option>
                            </select>
                        </td>
                    </tr>
                     <tr>
                        <td>
                            Estado Civil:
                        </td>
                        <td>
                            <select name="estadoCivil">
                                <option value="">Escolher</option>
                                <option value="casado">Casado</option>
                                <option value="solteiro">Solteiro</option>
                                <option value="divorciado">Divorciado</option>
                                <option value="viuvo">Viúvo</option>
                            </select>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            CPF:
                        </td>
                        <td>
                            <input type='text' name='cpf'  data-ls-module="charCounter" maxlength="14" placeholder="ex: xxx.xxx.xxx-xx">
                        </td>
                    </tr>
                    <tr>
                        <td>
                           RG:
                        </td>
                        <td>
                            <input type='text' name='rg'  data-ls-module="charCounter" maxlength="13" >
                        </td>
                    </tr>
                    <tr>
                        <td>
                            Data de Nascimento:
                        </td>
                        <td>
                            <input type='date' name='dataNascimento' value=''>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            Email:
                        </td>
                        <td>
                            <input type='email' name='email' value=''>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            Telefone:
                        </td>
                        <td>
                            <input type='tel' name='telefone'  placeholder="ex: (xx) xxxxx-xxxx">
                        </td>
                    </tr>
                    <tr>
                        <td colspan='2' aling='center'>
                            <input type='button' onclick="GravarAlterarTabela(document.frmInserirCliente)" value='Cadastrar'>&nbsp;
                           
                        </td>
                    </tr>
                </table> 
        </form>
    </div>
    </body>

 @import url('https://fonts.googleapis.com/css2?family=Alegreya+SC&family=Dancing+Script&display=swap');
 @import url('https://fonts.googleapis.com/css2?family=Alegreya+SC&family=Pathway+Gothic+One&display=swap');

html, body{
    min-height: 100%;
    margin: 0;
}


.imgg{
    height: 70px;
}

#headerUsuario{
    background-color: rgb(5, 50, 112);
    margin-bottom: -2%;
    padding-top: 0.2%;
    padding-bottom:-1%;
    text-align: center;
    margin-top: -1%;
}

#barraDeTarefas{
    background-color: rgb(5, 50, 112);
    margin-top: 2%;
    padding-bottom: 2%;
   
    
}
#imagemBarra{
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    padding-top: 1%
   
}

#foto{
    border: 1px solid black;
    margin-top: 3%;
    padding-top: 10%;
    padding-bottom: 5%;
    padding-left: 5%;
    background-color: white;
}

main{
    display: flex;
    flex-direction: row-reverse;
    justify-content:  center;
}

#cadastro{
    margin-left: 45%;
}
#telefone{

    background-color: blue;
}

#setor-admissao{

    background-color: red;
}

#foto-botao{
   
    background-color: green;
}
#dados{
    display: flexbox;
    
    background-color: rgb(138, 145, 142);
}
#embarcacoes{
   font-size: 3em;
   color: white;
   margin-top: 0%;
   font-family: 'Pathway Gothic One', sans-serif;
}

#altoMare{
    font-size: 4em;
    color: white;
    font-family: 'Dancing Script', cursive;
    font-style: italic;  
    margin: 0%;
   
}

.campos{
  height: 20px;
  font-size: 60%;
}

#embarcacoesUsuarios{
   font-size: 150%;
   color: white;
   padding-top: 3%;
   margin-top: -7%;
}

#lemeUsuarios{
    width: 8%;
    float: left;
    margin-top: -9%;
    margin-left: 10%;
}

#altoMare{
    padding-bottom: -30%;
    margin-top: 2%;
    font-size:600%;
    color: white;
    font-family: Dancing Script;
    font-style: italic; 
}

#leme{
    width: 10%;
    float: left;
    margin-top: -12%;
    margin-left: 10%;
}

#linha{
    background-color: rgb(114, 146, 189);
    padding-top: 0.40%;
    margin-top: -1%;
}

#header1{
    background-color: rgb(5, 50, 112);
    margin-bottom: -2%;
    padding-top: 0.2%;
    padding-bottom:-1%;
    text-align: center; 
}
#cadastroFunc{
    background-color: rgb(217, 217, 217);
    border-radius: 5%;

}

#titulo{
    text-align: center;
    font-family: Bebas Neue;
}

#botao{
   padding-bottom: 2%;
   border-radius: 10%;
   padding-top: 2%;
   width: 50%;
   font-size: 70%;
   background-color: rgb(5, 50, 112);
   color: white;
}

#login{
    text-align: center;
    font-size: 200%;
    margin-left: 35%;
    margin-right: 35%;
    margin-top: 1%;
    padding-bottom: 2%;
    padding-top: 1%;
}
