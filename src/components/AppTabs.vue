<template>
  <v-card color="v-card-color">
    <v-card-title class="text-center justify-center py-6">
      <h1 class="font-weight-bold text-h2 blue--text">{{ titulo }}</h1>
    </v-card-title>

    <v-tabs v-model="tab" color="blue" grow>
      <v-tab v-for="item in items" :key="item">
        {{ item }}
      </v-tab>
    </v-tabs>

    <v-tabs-items v-model="tab">
      <v-tab-item v-for="item in contenido" :key="item.key">
        <v-container>
          <component class="mt-3" :is="item.content" />
        </v-container>
      </v-tab-item>
    </v-tabs-items>
  </v-card>
</template>

<script>
export default {
  props: {
    contenido: {
      type: Array,
      default: () => [],
    },
    items: {
      type: Array,
      default: () => [],
    },
    titulo: {
      type: String,
      default: "",
    },
  },
  name: "AppTabs",
  data: () => ({
    tab: null,
  }),
  methods: {
    editItem(item) {
      console.log(item.name, "editItem");
    },
    showItem(item) {
      console.log(item.name, "showItem");
    },
    deleteItem(item) {
      console.log(item.name, "deleteItem");
    },
  },
};
</script>
<style scoped>
.v-card-color {
  background: rgba(226, 221, 221, 0.2);
}
</style>
