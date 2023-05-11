<template lang="">
  <p>
    {{ resumeText }}
  </p>
</template>
<script>
export default {
  props: ["res"],
  data() {
    return {
      resumeText: this.res.resumeText,
    };
  },
};
</script>
<style lang=""></style>
