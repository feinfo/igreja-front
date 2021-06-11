<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark" class="colorDark">
      <b-navbar-brand href="#"></b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-item right>{{tipoPerfil}}</b-nav-item>

          <b-nav-item-dropdown right>
            <!-- Using 'button-content' slot -->
            <template v-slot:button-content>
              <em>{{nomeUsuario}}</em>
            </template>
            <b-dropdown-item href="perfilUsuario">Perfil</b-dropdown-item>
            <b-dropdown-item @click="sair">Sair</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
    name:'header',
    data(){
        return{
          nomeUsuario:null,
          tipoPerfil: null
             
        }
    },
    created(){
      this.nomeUsuario = localStorage.getItem('nomeUsuario');
      this.tipoPerfil = localStorage.getItem('tipoPerfil');
    },
    methods: {
      sair(){
        localStorage.setItem('nomeUsuario','');
        localStorage.setItem('tipoPerfil','');
        localStorage.setItem('token','');
        this.$router.push('/');
      }
    }
}
</script>
<style  scoped>
  .colorDark{
    background-color: rgb(42,42,41) !important;

  }
</style>