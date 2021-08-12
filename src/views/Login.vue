<template>
    <b-container>
        <div class="d-flex justify-content-center centro">
            <b-card  :img-src="require('@/assets/560px-Logoccb.png')" title="CCB ÁREA RESTRITA" border-variant="primary">
                <b-card-text>
                    <b-form @submit="onSubmit" @reset="onReset">
                        <b-row>
                            <b-col>
                                <b-form-group label="Login:" label-for="login" label-cols-sm="3" class="mt-2">
                                    <div class="text-center">
                                        <b-form-input type="email" required placeholder="Digite seu usuário" v-model="usuario.login" class="col-12" :state="erroAutenticado"/>
                                    </div>
                                </b-form-group>
                            </b-col>
                        </b-row>
                        <b-row>
                            <b-col> 
                                <b-form-group label="Senha:" label-for="senha" label-cols-sm="3" class="mt-2">
                                    <b-form-input type="password" required placeholder="Digite sua senha" class="col-12" v-model="usuario.senha" :state="erroAutenticado"/>
                                </b-form-group>
                            </b-col>
                        </b-row>
                        <b-row>
                            <b-col> 
                                <b-form-invalid-feedback :state="erroAutenticado">
                                    Usuário ou senha incorreta!
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
.centro{
    margin-top: 10%;
}
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
        erroAutenticado: null,
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
                this.erroAutenticado = null;
                this.erroDesc = true;
            }
            else{
                let token = response.data.access_token;
                api.post("me",  stringify({token})).then(responsed => {
                    localStorage.setItem('nomeUsuario', responsed.data['0'].name);
                    localStorage.setItem('tipoPerfil',  responsed.data['0'].perfil.ds_descricao);
                    //console.log(response);
                    this.erroAutenticado = null;
                    this.erroDesc = null;
                    localStorage.setItem('token', token);
                    localStorage.setItem('usuario',response.data.usuario.name);
                    //localStorage.setItem('cd_usuario',response.data.usuario.cd_usuario);
                    //localStorage.setItem('email',response.data.usuario.email);
                    this.$router.push('dashboard');
                });
               
                //redirecionar para o dashboard
            }
        }).catch(erro => {
            if(erro.response && erro.response.status == 401)
            {
                this.erroAutenticado = false;
                this.erroDesc = null
                
            }
            else 
            {
                this.erroAutenticado = null;
                this.erroDesc = true;
                
            }
        }).finally(() => this.loading = false);
        
    },
    onReset: function(){
        this.erroAutenticado = null;
        this.usuario.login = "";
        this.usuario.senha = "";
    }
}
}
</script>