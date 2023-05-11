<template lang="">
  <div class="form-control">
    <label for="value">Значение</label>
    <textarea
      id="value"
      rows="3"
      :value="inputModel"
      @input="change"
    ></textarea>
  </div>
</template>
<script>
export default {
  props: ["inputModel"],
  emits: ["update:inputModel"],
  data() {
    return {};
  },
  methods: {
    change(event) {
      this.$emit("update:inputModel", event.target.value);
    },
  },
};
</script>
<style lang=""></style>
