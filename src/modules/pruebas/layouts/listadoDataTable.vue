<template>
  <div class="mt-4">
    <AppTitle :titulo="'Demostración de DataTable Genérica'" />
    <br />
    <div class="d-flex justify-end align-center mb-5">
      <v-btn color="blue" outlined @click="value = true">
        Nuevo Registro <v-icon> mdi-plus-box-outline</v-icon></v-btn
      >
    </div>
    <v-container style="height: 70vh">
      <DataTable
        :headers="headers"
        @paginate="getSolicitud"
        :response="response"
        :actions="actions"
      >
      </DataTable>
    </v-container>

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
    // AppDataTable: defineAsyncComponent(() =>
    //   import("@/components/AppDataTable.vue")
    // ),
    AppDialog: defineAsyncComponent(() => import("@/components/AppDialog.vue")),
    DataTable: defineAsyncComponent(() => import("@/components/DataTable.vue")),
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
        text: "ID",
        align: "start",
        sortable: false,
        value: "id",
      },
      { text: "Estado Solicitud", value: "estado_solicitud.nombre" },
      { text: "Fecha Creacion", value: "fecha_creacion" },
      { text: "Actions", value: "actions", sortable: false },
    ],
    items: [
      {
        name: "Frozen Yogurt",
        calories: 159,
        fat: 6.0,
        carbs: 24,
        protein: 4.0,
        class: "bluePatologia white--text",
      },
      {
        name: "Ice cream sandwich",
        calories: 237,
        fat: 9.0,
        carbs: 37,
        protein: 4.3,
        class: "bluePatologia white--text",
      },
      {
        name: "Eclair",
        calories: 262,
        fat: 16.0,
        carbs: 23,
        protein: 6.0,
        class: "bluePatologia white--text",
      },
      {
        name: "Cupcake",
        calories: 305,
        fat: 3.7,
        carbs: 67,
        protein: 4.3,
        class: "bluePatologia white--text",
      },
      {
        name: "Gingerbread",
        calories: 356,
        fat: 16.0,
        carbs: 49,
        protein: 3.9,
        class: "bluePatologia white--text",
      },
    ],
    response: [],
    actions: [
      {
        tooltip: {
          text: "Enviar Notificación",
          color: "gtPrimary",
        },
        icon: {
          color: "gtPrimary",
          name: "mdi-send-check",
        },
        eventName: "send",
      },
      {
        tooltip: {
          text: "Ver",
          color: "gtPrimary",
        },
        icon: {
          color: "gtPrimary",
          name: "mdi-eye",
        },
        eventName: "show1",
      },
      {
        tooltip: {
          text: "Imprimir",
          color: "red",
        },
        icon: {
          color: "red",
          name: "mdi-printer",
        },
        eventName: "show",
      },
    ],
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
    async getSolicitud(pagination = { per_page: 10, pagina: 1 }) {
      const response1 = { ...pagination };
      const response = await axios.get(
        "http://10.168.241.215:8010/api/v1/solicitudes",
        { params: response1 }
      );
      console.log(response.data);
      this.response = response.data;
    },
  },
  created() {
    this.getSolicitud();
  },
};
</script>
