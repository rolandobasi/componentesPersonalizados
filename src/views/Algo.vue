<template>
  <v-container fluid>
    <v-card color="v-card-color">
      <v-card-title class="text-center justify-center py-6">
        <h1 class="font-weight-bold text-h2 basil--text">BASiL</h1>
      </v-card-title>

      <v-tabs v-model="tabb" background-color="transparent" color="basil" grow>
        <v-tab v-for="item in items" :key="item">
          {{ item }}
        </v-tab>
      </v-tabs>

      <v-tabs-items v-model="tabb">
        <v-tab-item v-for="item in tabs" :key="item.key">
          <component :is="item.content" />
        </v-tab-item>
      </v-tabs-items>
    </v-card>
  </v-container>
</template>

<script>
import AppTabsVue from "@/components/AppTabs.vue";
import AppDataTable from "@/components/AppDataTable.vue";

export default {
  name: "PruebasVue",
  components: {
    AppDataTable,
    AppTabsVue,
  },
  data: () => ({
    tabb: null,
    tabs: [
      {
        tab: "v-data-table",
        content: AppDataTable,
        key: Date.now() + 3,
      },
      {
        tab: "v-dialog",
        content: AppTabsVue,
        key: Date.now() + 4,
      },
    ],
    items: ["v-data-table", "v-dialog", "Tab 3"],
    text: `Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.`,
  }),
};
</script>
<style scoped>
.v-card-color {
  background: rgba(228, 225, 225, 0.3);
}
</style>
