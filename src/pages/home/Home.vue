<template>
  <SiteTemplate>
    <span slot="menuesquerdo">
      <div class="row valign-wrapper">
        <GridVue tamanho="4">
          <img
            src="https://materializecss.com/images/yuna.jpg"
            alt=""
            class="circle responsive-img"
          />
          <!-- notice the "circle" class -->
        </GridVue>
        <GridVue tamanho="8">
          <span class="black-text">
            <h5>Maria</h5>
            Add the "circle" class to it to make it appear circular.
          </span>
        </GridVue>
      </div>
    </span>

    <span slot="principal">
      <PublicarConteudoVue />
      <CardConteudoVue
        perfil="https://materializecss.com/images/sample-1.jpg"
        nome="Maria"
        data="13/01/2018 13:30"
      >
        <CardDetalheVue
          img="https://materializecss.com/images/sample-1.jpg"
          titulo=""
          txt="I am a very simple card. I am good at containing small bits of information.
          I am convenient because I require little markup to use effectively."
        />
      </CardConteudoVue>
    </span>

  </SiteTemplate>
</template>

<script>
import SiteTemplate from "@/templates/SiteTemplate";
import CardConteudoVue from "@/components/social/CardConteudoVue";
import CardDetalheVue from "@/components/social/CardDetalheVue";
import PublicarConteudoVue from "@/components/social/PublicarConteudoVue";

export default {
  name: "Home",
  data() {
    return {};
  },
  components: {
    SiteTemplate,
    CardConteudoVue,
    CardDetalheVue,
    PublicarConteudoVue,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
