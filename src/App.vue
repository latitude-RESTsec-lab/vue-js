<template>

 <div id="app" class="container">
   
  <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
  <a class="navbar-brand" href="#">CEPESC</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarColor01" aria-controls="navbarColor01" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="navbarColor01">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
        <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Pessoas</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">SIAPE</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Manual</a>
      </li>
    </ul>
    <form class="form-inline my-2 my-lg-0">
      <input class="form-control mr-sm-2" placeholder="Search" type="text">
      <button class="btn btn-secondary my-2 my-sm-0" type="submit">Search</button>
    </form>
  </div>
</nav>
 
    

    <div class="panel panel-default">
      <div class="panel-heading" style="padding-top: 50px">
        <h3>Cadastro de Pessoa</h3>
      </div>

      <div class="panel-body" style="padding-top: 10px">
        <form id="form" class="form-inline" v-on:submit.prevent="addPessoa">
          <div class="form-row">
            <div class="form-group col-md-4">
              <label for="pessoaNome">Nome</label>
              <input type="text" class="form-control" id="pessoaNome" placeholder="Digite o nome" v-model="novaPessoa.nome">
            </div>
            <div class="form-group col-md-4">
              <label for="pessoaSiape">SIAPE</label>
              <input type="text" class="form-control" id="pessoaSiape" placeholder="Digite o SIAPE" v-model="novaPessoa.siape">
            </div>
            <div class="form-group col-md-4">
              <label for="pessoaDataNasc">Data de Nascimento</label>
              <input type="date" class="form-control" id="pessoaDataNasc" v-model="novaPessoa.dataNasc">
            </div>
          </div>
          
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </form>
      </div>
    </div>

    <div class="panel panel-default">
      <div class="panel-heading" style="padding-top: 50px">
        <h3> Lista de Pessoas</h3>
      </div>
      <div class="panel-body" style="padding-top: 10px">
        <table class="table table-striped">
          <thead>
            <tr>
              <th>
                Nome
              </th>
              <th>
                SIAPE
              </th>
              <th>
                Delete
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for-key="pessoa in pessoas">
              <td>
                {{pessoa.nome}}
              </td>
              <td>
                {{pessoa.siape}}
              </td>
              <td>
                <input type="submit" class="btn btn-danger" value="Remover" v-on:click="removePessoa(pessoa)">
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld";

import Firebase from "firebase";

let config = {
  apiKey: "AIzaSyAL57gpCzJaBvP1F-ZyQyHHl2RA4QCR044",
  authDomain: "vuejs-firebase-02-aadfe.firebaseapp.com",
  databaseURL: "https://vuejs-firebase-02-aadfe.firebaseio.com",
  projectId: "vuejs-firebase-02-aadfe",
  storageBucket: "vuejs-firebase-02-aadfe.appspot.com",
  messagingSenderId: "724764517877"
};

let app = Firebase.initializeApp(config);
let db = app.database();

let pessoasRef = db.ref("pessoas");

export default {
  name: "App",
  firebase: {
    pessoas: pessoasRef
  },
  data() {
    return {
      novaPessoa: {
        nome: "",
        siape: "",
        dataNasc: ""
      }
    };
  },
  methods: {
    addPessoa: function() {
      pessoasRef.push(this.novaPessoa);
      this.novaPessoa.nome = "";
      this.novaPessoa.siape = "";
      this.novaPessoa.dataNasc = "";
    },
    removePessoa: function(pessoa) {
      pessoasRef.child(pessoa[".key"]).remove();
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
