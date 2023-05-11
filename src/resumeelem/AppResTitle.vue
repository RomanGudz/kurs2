<template lang="">
  <h1>{{ resumeTitle }}</h1>
</template>
<script>
export default {
  props: ["res"],
  data() {
    return {
      resumeTitle: this.res.resumeTitle,
    };
  },
};
</script>
<style lang=""></style>
