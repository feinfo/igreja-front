<template>
    <b-container>
        <div class="d-flex justify-content-center">
            <b-card  :img-src="require('@/assets/560px-Logoccb.png')" title="CCB ÁREA RESTRITA" border-variant="primary">
                <b-card-text>
                    <b-form @submit="onSubmit" @reset="onReset">
                        <b-row>
                            <b-col>
                                <b-form-group label="Login:" label-for="login" label-cols-sm="3" class="mt-2">
                                    <div class="text-center">
                                        <b-form-input type="email" required placeholder="Digite seu usuário" v-model="usuario.login" class="col-12" :state="autenticado"/>
                                    </div>
                                </b-form-group>
                            </b-col>
                        </b-row>
                        <b-row>
                            <b-col> 
                                <b-form-group label="Senha:" label-for="senha" label-cols-sm="3" class="mt-2">
                                    <b-form-input type="password" placeholder="Digite sua senha" class="col-12" v-model="usuario.senha" :state="autenticado"/>
                                </b-form-group>
                            </b-col>
                        </b-row>
                        <b-row>
                            <b-col> 
                                <b-form-invalid-feedback :state="autenticado">
                                    Usuário ou senha incorreto !
                                </b-form-invalid-feedback>
                                <b-form-invalid-feedback :state="!erroDesc">
                                    Erro desconhecido, entrar em contato com o desenvolvedor!
                                </b-form-invalid-feedback>
                            </b-col>
                        </b-row>
                        <b-row>
                            <b-col>
                                <b-form-group class="mt-2">
                                    <b-button type="submit" pill variant="primary" :disabled="loading">
                                        <b-spinner small v-if="loading"></b-spinner>
                                          Entrar
                                        </b-button>
                                </b-form-group>
                            </b-col>
                            <b-col>
                                <b-form-group class="mt-2">
                                    <b-button type="reset" pill variant="light" :disabled="loading">Limpar</b-button>
                                </b-form-group>
                            </b-col>
                        </b-row>
                    </b-form>
                </b-card-text>
            </b-card>
        </div>
    </b-container>
</template>
<style>
</style>
<script>
//import sideBar from '@/views/template/index.vue';
import api from '../service/api';
import { stringify } from 'querystring';

export default {
  name: "login",
  components:{
  //sideBar
  },
  data() {
    return{
        usuario:{
            login:null,
            senha:null
        },
        autenticado: null,
        erroDesc: null,
        loading: null,
    };
  },
methods: {
     async onSubmit(evt){
        evt.preventDefault();
        this.loading = true;
        let dadosLogin = stringify({email: this.usuario.login, password:this.usuario.senha});
        api.post("login", dadosLogin
        ).then(response => {
            if(response.status == undefined)
            {
                this.autenticado = null;
                this.erroDesc = true;
            }
            else{
                this.autenticado = null;
                this.erroDesc = null;
                //redirecionar para o dashboard
            }
        }).catch(erro => {
            if(erro.response && erro.response.status == 401)
            {
                this.erroDesc = null
                this.autenticado = false;
            }
            else 
            {
                this.erroDesc = true;
                this.autenticado = null;
            }
        }).finally(() => this.loading = false);
        
    },
    onReset: function(){
        this.autenticado = null;
        this.usuario.login = "";
        this.usuario.senha = "";
    }
}
}
</script>