<template>
  <div class="row">
        <GridVue class="input-field" tamanho="12">
          <textarea v-model="conteudo" id="conteudoID" class="materialize-textarea"></textarea>
          <label class="active" for="conteudoID">O que está acontecendo?</label>
        </GridVue>
        <p>
          <GridVue v-if="conteudo" class="btn waves-effect waves-light" tamanho="2 offset-s10">Publicar</GridVue>
        </p>
      </div>
</template>

<script>
import GridVue from "@/components/layouts/GridVue";
export default {
  name: "PublicarConteudoVue",
  props: [
   
  ],
  data() {
    return {
      conteudo: ''
    };
  },
  components: {
    GridVue,
  },
};
</script>

<style scoped>
</style>