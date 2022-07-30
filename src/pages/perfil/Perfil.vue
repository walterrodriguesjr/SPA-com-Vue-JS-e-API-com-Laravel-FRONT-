<template>

    <siteTemplate>

      <span slot="menuesquerdo">
        <img :src="usuario.imagem" class="responsive-img">
      </span>
      

          <span slot="principal">
     
          <h2>Perfil</h2>  

          <input type="text" placeholder="Nome" v-model="name">
          <input type="text" placeholder="E-mail" v-model="email">

          <div class="file-field input-field">
            <div class="btn">
             <span>Imagem</span>
              <input type="file" v-on:change="salvaImagem">
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
export default {
  name: "Perfil",
  data() {
    return {
    usuario: false,
    name:'',  
    email:'',
    password:'',
    password_confirmation:'',
    imagem:''
    }
  },
  created() {
    /* método que verifica se ousuário está logado, e pega os dados deste usuário */
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
    /* método de capturar imagem */
    salvaImagem(e){
      let arquivo = e.target.files || e.dataTransfer.files;
      if(!arquivo.length){
        return;
      }
      let reader = new FileReader();
      reader.onloadend = (e) => {
      this.imagem = e.target.result;
      };
      reader.readAsDataURL(arquivo[0]);
    },
    /* envia dados do usuário para o back-end via put */
    perfil(){
      this.$http.put(this.$urlAPI+`perfil`, {
				name: this.name,
				email: this.email,
        imagem:this.imagem,
        password: this.password,
        password_confirmation: this.password_confirmation,
			},{"headers":{"authorization":"Bearer "+this.usuario.token}})
				.then(response => {
          if(response.data.status){
            /* console.log(response.data); */
            this.usuario = response.data.usuario;
            sessionStorage.setItem('usuario', JSON.stringify(this.usuario));
            alert("Perfil atualizado com sucesso!")
          }else if (response.data.status == false && response.data.validacao){
              /* console.log("Erro de validação"); */
              let erros = '';
              for(let erro of Object.values(response.data.erros)){
                erros += erro +"";
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
