<template>
  <div class="mt-4">
    <AppTitle :titulo="'Demostración de DataTable Genérica'" />
    <br />
    <div class="d-flex justify-end align-center mb-5">
      <v-btn color="blue" outlined @click="value = true">
        Nuevo Registro <v-icon> mdi-plus-box-outline</v-icon></v-btn
      >
    </div>
    <AppDataTable
      :headers="headers"
      :items="items"
      :tablaAcciones="tablaAcciones"
    >
      <template v-slot:[`item.direccion`]="{ item }">
        {{ item.direccion }}
      </template>
    </AppDataTable>
    <AppDialog
      v-model="value"
      :custom="true"
      :colorText="'grey'"
      :icon="'fa-solid fa-exclamation-circle'"
      :description="'Ingrese los datos del nuevo registro'"
      :max="1000"
    >
      <template #container-title>
        <span class="font-weight-bold text-wrap"> Nuevo Registro </span>
      </template>
      <template #container-main>
        <div>
          <v-row>
            <v-col cols="6">
              <v-text-field
                v-model="nuevoRegistro.nombre"
                label="Nombre"
                dense
              ></v-text-field>
            </v-col>
            <v-col cols="6">
              <v-text-field
                v-model="nuevoRegistro.apellido"
                label="Apellido"
                dense
              ></v-text-field>
            </v-col>
          </v-row>
        </div>
      </template>
      <template #actions>
        <div>
          <v-btn color="blue" outlined @click="value = false" class="mr-4">
            Guardar <v-icon class="ml-1"> mdi-content-save-plus-outline</v-icon>
          </v-btn>
          <v-btn color="red" outlined @click="value = false">
            Cancelar <v-icon class="ml-1">mdi-close</v-icon></v-btn
          >
        </div>
      </template>
    </AppDialog>
  </div>
</template>

<script>
import { defineAsyncComponent } from "vue";
import axios from "axios";

export default {
  name: "listadoTabla",
  components: {
    AppTitle: defineAsyncComponent(() => import("@/components/AppTitle.vue")),
    AppDataTable: defineAsyncComponent(() =>
      import("@/components/AppDataTable.vue")
    ),
    AppDialog: defineAsyncComponent(() => import("@/components/AppDialog.vue")),
  },
  data: () => ({
    value: false,
    usuarios: null,
    nuevoRegistro: {
      nombre: "",
      apellido: "",
    },
    headers: [
      {
        text: "Nombre",
        align: "center",
        sortable: true,
        value: "nombre",
        class: "primary white--text",
      },
      {
        text: "Dirección",
        align: "center",
        sortable: true,
        value: "direccion",
        class: "primary white--text",
      },
      {
        text: "Fax",
        align: "center",
        sortable: true,
        value: "fax",
        class: "primary white--text",
      },
      {
        text: "Teléfono",
        align: "center",
        sortable: false,
        value: "telefono",
        class: "primary white--text",
      },
      {
        text: "Acciones",
        value: "actions",
        align: "center",
        sortable: false,
        class: "primary white--text text-center",
        width: 200,
      },
    ],
    items: [],
    tablaAcciones: [
      {
        id: 1,
        icono: {
          funcion: "fichasRegistradas",
          figura: "mdi-eye",
          color: "blue",
          disabled: false,
          large: false,
          left: false,
          right: false,
          size: "",
          small: false,
          class: "",
        },
        tooltip: {
          color: "blue",
          name: "Visualizar Ficha",
          top: true,
          left: false,
          right: false,
          bottom: false,
          class: "whiteMinsal--text",
        },
      },
      {
        id: 2,
        icono: {
          funcion: "establecimientosDanados",
          figura: "mdi-map-search-outline",
          color: "blue",
          disabled: false,
          large: false,
          left: false,
          right: false,
          size: "",
          small: false,
          class: "",
        },
        tooltip: {
          color: "blue",
          name: "Establecimientos Dañados",
          top: true,
          left: false,
          right: false,
          bottom: false,
          class: "whiteMinsal--text font-weight-bold",
        },
      },
      {
        id: 3,
        icono: {
          funcion: "reporteFuncionamientoServicio",
          figura: "mdi-file",
          color: "blue",
          disabled: false,
          large: false,
          left: false,
          right: false,
          size: "",
          small: false,
          class: "",
        },
        tooltip: {
          color: "blue",
          name: "Funcionamiento del Servicio de Salud",
          top: true,
          left: false,
          right: false,
          bottom: false,
          class: "whiteMinsal--text font-weight-bold",
        },
      },
      {
        id: 4,
        icono: {
          funcion: "reporteEfectosAdversos",
          figura: "mdi-file",
          color: "gray",
          disabled: false,
          large: false,
          left: false,
          right: false,
          size: "",
          small: false,
          class: "",
        },
        tooltip: {
          color: "gray",
          name: "Tipos de Efectos Adversos",
          top: true,
          left: false,
          right: false,
          bottom: false,
          class: "whiteMinsal--text font-weight-bold",
        },
      },
      {
        id: 5,
        icono: {
          funcion: "cambiarEstado",
          figura: "mdi-check-circle",
          color: "green",
          disabled: false,
          large: false,
          left: false,
          right: false,
          size: "",
          small: false,
          class: "",
        },
        tooltip: {
          color: "green",
          name: "Estado del Establecimiento",
          top: true,
          left: false,
          right: false,
          bottom: false,
          class: "whiteMinsal--text font-weight-bold",
        },
      },
    ],
  }),
  methods: {
    async getUsuarios() {
      const response = await axios.get(
        "http://10.168.241.215:8010/api/v1/establecimientos"
      );
      this.items = response.data.body;
    },
  },
  created() {
    this.getUsuarios();
  },
};
</script>
