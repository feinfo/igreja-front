<template>
  <div>
    <Header />
    <SideBar @collapsed="retorno"/>
    <div class="container-fluid">
      <div class="row">
        <div v-bind:class="styleObject.colunaCard" v-bind:style="styleObject.marginLeft">
          <div class="card text-center mt-4">
            <div class="card-header">
              Dados Usúario
            </div>
            <div class="card-body">
              <form>
                <div class="form-row">
                  <div class="form-group col-md-4">
                    <label for="inputEmail4">Nome:</label>
                    <input type="text" class="form-control col-10 col-sm-8" id="inputEmail4" placeholder="Email" v-model="dadosUsuario.name">
                  </div>
                  <div class="form-group col-lt-6">
                    <label for="inputPassword4">Sobrenome:</label>
                    <input type="password" class="form-control" id="inputPassword4" placeholder="Password">
                  </div>
                </div>
                <div class="form-group">
                  <label for="inputAddress">CPF</label>
                  <input type="text" class="form-control" id="inputAddress" placeholder="1234 Main St">
                </div>
                <div class="form-group">
                  <label for="inputAddress2">E-mail</label>
                  <input type="email" class="form-control" id="email" placeholder="email@email.com" v-model="dadosUsuario.email">
                </div>
                <div class="form-row">
                  <div class="form-group col-md-6">
                    <label for="inputCity">Senha</label>
                    <input type="text" class="form-control" id="inputCity">
                  </div>
                  <div class="form-group col-md-4">
                    <label for="inputState">State</label>
                    <select id="inputState" class="form-control">
                      <option selected>Choose...</option>
                      <option>...</option>
                    </select>
                  </div>
                  <div class="form-group col-md-2">
                    <label for="inputZip">Zip</label>
                    <input type="text" class="form-control" id="inputZip">
                  </div>
                </div>
                <div class="form-group">
                  <div class="form-check">
                    <input class="form-check-input" type="checkbox" id="gridCheck">
                    <label class="form-check-label" for="gridCheck">
                      Check me out
                    </label>
                  </div>
                </div>
                <button type="submit" class="btn btn-primary">Sign in</button>
              </form>
            </div>
            <div class="card-footer text-muted">
              2 days ago
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

import Header from './header';
import SideBar from './template';
import api from '../service/api';
import { stringify } from 'querystring';

export default {
  name: 'Dashboard',
  components: {
   Header,
   SideBar,
  },
  data() {
    return {
      form : [],
      dadosUsuario : [],
      styleObject: {
        colunaCard: 'col-10',
        marginLeft: 'margin-left: 14%'
      }
    }
  },
  created() {
    let token = localStorage.getItem('token');
    let self = this;
    api.post("me", stringify({token})).then(res =>{
      self.dadosUsuario = res.data[0];
    });
  },
  methods:{
    retorno : function(res){
      if(res)
      {
         this.styleObject.colunaCard =  'col-11';
         this.styleObject.marginLeft = 'margin-left: 5%';
      }
      else 
      {
        this.styleObject.colunaCard =  'col-10';
        this.styleObject.marginLeft = 'margin-left: 14%';
      }
    },
    onSubmit : function(){

    },
    onReset: function(){

    }
  }
}

</script>
<style scoped>
  .espaco{
    margin-left: 10%;
  }

</style>