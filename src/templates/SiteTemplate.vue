<template>
  <span>
    <header>
      <NavBar cor="green darken-1" logo="Social" url="/">
        <li><router-link to="/">Home</router-link></li> 
        <li v-if="!usuario"><router-link to="/login">Entrar</router-link></li>
        <li v-if="!usuario"><router-link to="/cadastro">Cadastre-se</router-link></li>
        <li v-if="usuario"><router-link to="/perfil">{{usuario.name}}</router-link></li>
        <li v-if="usuario"><a v-on:click="sair()">Sair</a></li>
      </NavBar>
    </header>

    <main>
      <div class="container">
        <div class="row">
          <GridVue tamanho="4">
            <CardMenuVue>
              <slot name="menuesquerdo" />
            </CardMenuVue>
          </GridVue>
          <GridVue tamanho="8">
            <slot name="principal" />
          </GridVue>
        </div>
      </div>
    </main>

    <footer>
      <FooterVue
        cor="green darken-1"
        logo="Social"
        descricao="Teste de descrição"
        ano="2018"
      >
        <li><a class="grey-text text-lighten-3" href="#!">Link 1</a></li>
        <li><a class="grey-text text-lighten-3" href="#!">Link 2</a></li>
        <li><a class="grey-text text-lighten-3" href="#!">Link 3</a></li>
        <li><a class="grey-text text-lighten-3" href="#!">Link 4</a></li>
      </FooterVue>
    </footer>
  </span>
</template>

<script>
import NavBar from "@/components/layouts/NavBar";
import FooterVue from "@/components/layouts/FooterVue";
import GridVue from "@/components/layouts/GridVue";
import CardMenuVue from "@/components/layouts/CardMenuVue";
import CardConteudoVue from "@/components/social/CardConteudoVue";

export default {
  name: "SiteTemplate",
  data(){
    return {
      usuario: false
    }
  },
  components: {
    NavBar,
    FooterVue,
    GridVue,
    CardMenuVue,
    CardConteudoVue,
  },
  created() {
    console.log('created()');
    let usuarioAux = sessionStorage.getItem('usuario');
    if(usuarioAux){
      this.usuario = JSON.parse(usuarioAux);
    }else{
      /* usuario não acessa a home, caso não esteja logado */
      this.$router.push('/login');
    }
  },
  /* limpa a sessão do storage e desloga o usuário */
  methods: {
    sair(){
      sessionStorage.clear();
      this.usuario = false;
      /* ao clicar em sair, usuário é direcionado para tela de login */
      this.$router.push('/login');
    }
  },
};
</script>

<style>
</style>
