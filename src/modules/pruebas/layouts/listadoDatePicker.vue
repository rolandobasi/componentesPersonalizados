<template>
  <div>
    <AppTitle :titulo="'Demostración de DatePicker Genérico'" />
    <v-spacer />
    <v-row>
      <v-col cols="6">
        <AppDatePicker v-model="fecha" :max="max" :min="min" />
        <v-text-field v-model="fecha" label="Fecha" disabled></v-text-field>
      </v-col>
      <v-col cols="6">
        <AppDatePicker
          v-model="fechaRange"
          :max="max"
          :min="min"
          :range="true"
        />
        <v-text-field
          v-model="fechaRange"
          label="Fecha"
          disabled
        ></v-text-field>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import moment from "moment";

import { defineAsyncComponent } from "vue";
export default {
  components: {
    AppTitle: defineAsyncComponent(() => import("@/components/AppTitle.vue")),
    AppDatePicker: defineAsyncComponent(() =>
      import("@/components/AppDatePicker.vue")
    ),
  },
  name: "listadoDatePicker",
  data: () => ({
    fecha: "",
    fechaRange: "",
    min: moment().subtract(5, "years").format("YYYY-MM-DD"),
    max: moment().format("YYYY-MM-DD"),
  }),
};
</script>
