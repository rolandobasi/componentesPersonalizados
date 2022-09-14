<template>
  <div>
    <h1 class="d-flex justify-center">{{ titulo }}</h1>
    <v-spacer />
    <v-divider />
  </div>
</template>

<script>
export default {
  props: {
    titulo: {
      type: String,
      default: "",
    },
  },
  name: "AppTitle",
};
</script>
<style scoped>
hr {
  border: 1px solid #505458;
}
</style>
