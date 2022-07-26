<template>

    <siteTemplate>

      <span slot="menuesquerdo">
        <img src="https://www.mazag.com.br/wp-content/uploads/2020/09/gerenciamento-de-redes-sociais-1024x663.jpg" class="responsive-img">
      </span>
      

          <span slot="principal">
     
          <h2>Perfil</h2>  

          <input type="text" placeholder="Nome" v-model="name">
          <input type="text" placeholder="E-mail" v-model="email">

          <div class="file-field input-field">
            <div class="btn">
             <span>File</span>
              <input type="file">
         </div>
         <div class="file-path-wrapper">
           <input class="file-path validate" type="text">
         </div>
         </div>

          <input type="password" placeholder="Senha" v-model="password">
          <input type="password" placeholder="Confirme sua senha" v-model="password_confirmation">
          <button class="btn" v-on:click="perfil()">Atualizar</button>
 
    
        </span>

    </SiteTemplate>

</template>

<script>
import SiteTemplate from "@/templates/SiteTemplate";
import axios from "axios";
export default {
  name: "Perfil",
  data() {
    return {
    usuario: false,
    name:'',  
    email:'',
    password:'',
    password_confirmation:''
    }
  },
  created() {
    let usuarioAux = sessionStorage.getItem('usuario');
    if(usuarioAux){
      this.usuario = JSON.parse(usuarioAux);
      /* pegando os dados que vem de usuário */
      this.name = this.usuario.name;
      this.email = this.usuario.email;
    }
  },
  components: {
    SiteTemplate
  },
  methods: {
    /* envia para o back-end via put */
    perfil(){
      axios.put('http://127.0.0.1:8000/api/perfil', {
				name: this.name,
				email: this.email,
        password: this.password,
        password_confirmation: this.password_confirmation,
			},{"headers":{"authorization":"Bearer "+this.usuario.token}})
				.then(response => {
          console.log(response);
    
         
            console.log(response.data);

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
