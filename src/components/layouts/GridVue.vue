<template>
<div :class="'col s'+ tamanho">
<slot/>
</div>
</template>

<script>
export default {
  name: "GridVue",
  props: ["tamanho"],
  data() {
    return {};
  },
};
</script>

<style scoped>
</style>