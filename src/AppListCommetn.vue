<template lang="">
  <h2>Комментарии</h2>
  <ul class="list">
    <li class="list-item" v-for="coment in coments" :key="coment">
      <div>
        <p>
          <strong>{{ coment.email }}</strong>
        </p>
        <small>{{ coment.body }}</small>
      </div>
    </li>
  </ul>
</template>
<script>
export default {
  props: ["coments"],
};
</script>
<style lang=""></style>
