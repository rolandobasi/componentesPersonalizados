<template>
  <div>
    <v-data-table
      :headers="headers"
      :items="items"
      no-data-text="Sin datos"
      sort-by="calories"
      class="elevation-1"
    >
      <template v-for="(index, name) in $scopedSlots" v-slot:[name]="data">
        <slot :name="name" v-bind="data"></slot>
      </template>

      <template v-slot:activator="{ on }">
        <v-tooltip top color="blue">
          <v-icon
            v-if="item.id_estado_solicitud != 2"
            v-on="on"
            color="bluePatologia"
            size="20"
            @click="$emit('mostrarModalPlane')"
          >
            fa-solid fa-paper-plane
          </v-icon>
          <span>Agregar referencia</span>
        </v-tooltip>
      </template>

      <template v-slot:[`item.actions`]="{ item }">
        <v-tooltip
          :top="acciones.tooltip.top"
          :left="acciones.tooltip.left"
          :right="acciones.tooltip.right"
          :bottom="acciones.tooltip.bottom"
          :color="acciones.tooltip.color"
          v-for="(acciones, index) in tablaAcciones"
          :key="index"
        >
          <template v-slot:activator="{ on }">
            <v-icon
              v-on="on"
              :color="acciones.icono.color"
              :disabled="acciones.icono.disabled"
              :large="acciones.icono.large"
              :left="acciones.icono.left"
              :right="acciones.icono.right"
              :size="acciones.icono.size"
              :small="acciones.icono.small"
              :class="acciones.icono.class"
              :key="index"
              class="ml-2"
              @click="$emit(acciones.icono.funcion, item)"
            >
              {{ acciones.icono.figura }}
            </v-icon>
          </template>
          <span :class="acciones.tooltip.class">{{
            acciones.tooltip.name
          }}</span>
        </v-tooltip>
      </template>
    </v-data-table>
    <br />
  </div>
</template>
<script>
export default {
  name: "AppDataTable",
  props: {
    headers: {
      type: Array,
      default: () => {
        return [
          {
            text: "Dessert (100g serving)",
            align: "start",
            sortable: false,
            value: "name",
          },
          { text: "Calories", value: "calories" },
          { text: "Fat (g)", value: "fat" },
          { text: "Carbs (g)", value: "carbs" },
          { text: "Protein (g)", value: "protein" },
          { text: "Actions", value: "actions", sortable: false },
        ];
      },
    },
    items: {
      type: [Array, Object],
      default: () => {
        return [
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
        ];
      },
    },
    // tablaAcciones: {
    //   type: [Array, Object],
    //   default: () => {
    //     return [];
    //   },
    // },
    // EJEMPLO DE COMO ENVIAR LA DATA AL COMPONENTE
    tablaAcciones: {
      type: Array,
      default: () => {
        return [
          {
            id: 1,
            icono: {
              funcion: "editItem",
              figura: "mdi-pencil",
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
              name: "Editar Registro",
              top: true,
              left: false,
              right: false,
              bottom: false,
              class: "whiteMinsal--text font-weight-bold",
            },
          },
          {
            id: 2,
            icono: {
              funcion: "showItem",
              figura: "mdi-eye",
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
              name: "Mostrar Registro",
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
              funcion: "deleteItem",
              figura: "mdi-delete",
              color: "red",
              disabled: false,
              large: false,
              left: false,
              right: false,
              size: "",
              small: false,
              class: "",
            },
            tooltip: {
              color: "red",
              name: "Eliminar Registro",
              top: true,
              left: false,
              right: false,
              bottom: false,
              class: "whiteMinsal--text font-weight-bold",
            },
          },
        ];
      },
    },
  },
};
</script>
