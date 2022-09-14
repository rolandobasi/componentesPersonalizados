<!-- eslint-disable vue/no-unused-components -->
<template>
  <v-container fluid>
    <AppTabs
      :contenido="contenido"
      :items="items"
      :titulo="'Pruebas Frontend'"
    />
  </v-container>
</template>

<script>
import listadoDataTable from "../layouts/listadoDataTable.vue";
import listadoDatePicker from "../layouts/listadoDatePicker.vue";
import AppTabs from "@/components/AppTabs.vue";
import AppDataTable from "@/components/AppDataTable.vue";
import AppDialog from "@/components/AppDialog.vue";
export default {
  components: {
    AppTabs,
    // eslint-disable-next-line vue/no-unused-components
    AppDataTable,
    // eslint-disable-next-line vue/no-unused-components
    AppDialog,
    // eslint-disable-next-line vue/no-unused-components
    listadoDataTable,
    // eslint-disable-next-line vue/no-unused-components
    listadoDatePicker,
  },
  name: "listadoPruebas",
  data: () => ({
    contenido: [
      {
        tab: "v-data-table",
        content: listadoDataTable,
        key: Date.now() + 3,
      },
      {
        tab: "v-date-picker",
        content: listadoDatePicker,
        key: Date.now() + 4,
      },
    ],
    items: ["v-data-table", "v-date-picker"],
  }),
};
</script>
