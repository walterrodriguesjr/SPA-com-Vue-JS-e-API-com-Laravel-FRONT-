<template>

    <LoginTemplate>

      <span slot="menuesquerdo">
        <img src="https://www.mazag.com.br/wp-content/uploads/2020/09/gerenciamento-de-redes-sociais-1024x663.jpg" class="responsive-img">
      </span>
      
      <span slot="principal">

      <h2>Login</h2>

      <input type="text" placeholder="E-mail" value="">
      <input type="text" placeholder="Senha" value="">
      <button type="button" class="btn">Entrar</button>

      </span>

    
    </LoginTemplate>

</template>

<script>
import LoginTemplate from "@/templates/LoginTemplate";
import CardConteudoVue from "@/components/social/CardConteudoVue";
import CardDetalheVue from "@/components/social/CardDetalheVue";
import PublicarConteudoVue from "@/components/social/PublicarConteudoVue";



export default {
  name: "Login",
  data() {
    
    return {};
  },
  components: {
    LoginTemplate,
    CardConteudoVue,
    CardDetalheVue,
    PublicarConteudoVue

  },
  
};

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
