<template>

    <LoginTemplate>

      <span slot="menuesquerdo">
        <img src="https://www.mazag.com.br/wp-content/uploads/2020/09/gerenciamento-de-redes-sociais-1024x663.jpg" class="responsive-img">
      </span>
      
      <span slot="principal">

        
        <h2>Login</h2>  

          <input type="text" placeholder="E-mail" v-model="email">
          <input type="password" placeholder="Senha" v-model="password">
          <button class="btn" type="button" v-on:click="login()">Entrar</button>
          <router-link class="btn orange" to="/cadastro">Cadastre-se</router-link>

          

      </span>

    </LoginTemplate>

</template>

<script>
import LoginTemplate from "@/templates/LoginTemplate";

export default {
  name: "Login",
  data() {
    return {
        email:'',
        password:'',
    }
  },
  components: {
    LoginTemplate
  },
  methods: {
    login(){
      this.$http.post(this.$urlAPI+`login`, {
				email: this.email,
        password: this.password
			})
				.then(response => {
          console.log(response);
          if (response.data.status) {
            /* login com sucesso */
            console.log('Login com sucesso!');
            /* converte os dados retornados do usuário para texto */
            sessionStorage.setItem('usuario', JSON.stringify(response.data.usuario));
            /* direciona o usuário para a Home */
            this.$router.push('/');
          }else if(response.data.status == false && response.data.validacao){
            console.log('Erros de validação');
            let erros = '';
            /* cria um loop que lista os erros de validação */
            for(let erro of Object.values(response.data.erros)) {
              erros += erro +" ";
            }
            alert(erros);
          }else{
            /* login não existe */
            console.log('Login não existe');
            alert('Login inválido!');
            
          }
        })
        /* erro caso o servidor esteja fora do ar */
				.catch(e => {
				console.log(e)
        alert("Erro! Tente novamente mais tarde!");
			})
    }
  },
};

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
