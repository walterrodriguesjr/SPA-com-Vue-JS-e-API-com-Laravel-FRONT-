<template>

    <LoginTemplate>

      <span slot="menuesquerdo">
        <img src="https://www.mazag.com.br/wp-content/uploads/2020/09/gerenciamento-de-redes-sociais-1024x663.jpg" class="responsive-img">
      </span>
      

          <span slot="principal">
     
          <h2>Cadastro</h2>  

          <input type="text" placeholder="Nome" v-model="name">
          <input type="text" placeholder="E-mail" v-model="email">
          <input type="password" placeholder="Senha" v-model="password">
          <input type="password" placeholder="Confirme sua senha" v-model="password_confirmation">
          <button class="btn" v-on:click="cadastro()">Enviar</button>
          <router-link class="btn orange" to="/login">Já tenho conta</router-link>
 
    
        </span>

    </LoginTemplate>

</template>

<script>
import LoginTemplate from "@/templates/LoginTemplate";
export default {
  name: "Cadastro",
  data() {
    return {
    name:'',  
    email:'',
    password:'',
    password_confirmation:''
    }
  },
  components: {
    LoginTemplate
  },
  methods: {
    cadastro(){
      this.$http.post(this.$urlAPI+`cadastro`, {
				name: this.name,
				email: this.email,
        password: this.password,
        password_confirmation: this.password_confirmation,
			})
				.then(response => {
          console.log(response);
          if (response.data.status) {
            /* cadastro realizado com sucesso */
            console.log('Cadastro realizado com sucesso!');
            /* converte os dados retornados do usuário para texto */
            sessionStorage.setItem('usuario', JSON.stringify(response.data.usuario));
            /* direciona o usuário para a Home */
            this.$router.push('/');
          }else if(response.data.status == false && response.data.validacao){
             /* erros de validação */
            console.log('Erros de validação');
            let erros = '';
            /* cria um loop que lista os erros de validação */
            for(let erro of Object.values(response.data.erros)) {
              erros += erro +" ";
            }
            alert(erros);
          }else{
            /* Erro no cadastro! Tente novamente mais tarde! */
            console.log('Erro no cadastro. Tente novamente mais tarde!');
            alert('Erro no cadastro! Tente novamente mais tarde!');
           
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
