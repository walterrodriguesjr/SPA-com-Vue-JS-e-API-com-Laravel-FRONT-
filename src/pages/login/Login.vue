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
import axios from 'axios';

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
      axios.post('http://127.0.0.1:8000/api/login', {
				email: this.email,
        password: this.password
			})
				.then(response => {
          console.log(response);
          if (response.data.token) {
            /* login com sucesso */
            console.log('Login com sucesso!');
            /* converte os dados retornados do usuário para texto */
            sessionStorage.setItem('usuario', JSON.stringify(response.data));
            /* direciona o usuário para a Home */
            this.$router.push('/');
          }else if(response.data.status == false){
            /* login não existe */
            console.log('Login não existe');
            alert('Login inválido!');

          }else{
            /* erros de validação */
            console.log('Erros de validação');
            let erros = '';
            /* cria um loop que lista os erros de validação */
            for(let erro of Object.values(response.data)) {
              erros += erro +" ";
            }
            alert(erros);
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
