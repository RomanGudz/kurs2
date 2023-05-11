<template lang="">
  <div class="avatar">
    <img :src="resumeAvatar" />
  </div>
</template>
<script>
export default {
  props: ["res"],
  data() {
    return {
      resumeAvatar: this.res.resumeAvatar,
    };
  },
};
</script>
<style lang=""></style>
