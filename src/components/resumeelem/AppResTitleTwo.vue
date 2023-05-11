<template lang="">
  <h2>{{ resumeTitleTwo }}</h2>
</template>
<script>
export default {
  props: ["res"],
  data() {
    return {
      resumeTitleTwo: this.res.resumeTitleTwo,
    };
  },
};
</script>
<style lang=""></style>
