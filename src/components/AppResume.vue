<template lang="">
  <div class="card card-w70" v-if="resume.length !== 0">
    <div v-for="res in resume" :key="res">
      <app-res-title :res="res"></app-res-title>
      <app-res-avatar :res="res"></app-res-avatar>
      <app-res-title-two :res="res"></app-res-title-two>
      <app-res-text :res="res"></app-res-text>
    </div>
  </div>
  <div class="card card-w70" v-else>
    <h3>Добавить первый блок</h3>
  </div>
</template>
<script>
import AppResTitle from "./resumeelem/AppResTitle.vue";
import AppResAvatar from "./resumeelem/AppResAvatar.vue";
import AppResTitleTwo from "./resumeelem/AppResTitleTwo.vue";
import AppResText from "./resumeelem/AppResText.vue";

export default {
  props: {
    resume: Array,
  },
  components: { AppResTitle, AppResAvatar, AppResTitleTwo, AppResText },
};
</script>
<style lang=""></style>
