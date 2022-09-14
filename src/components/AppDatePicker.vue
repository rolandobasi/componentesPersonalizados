<template>
  <v-menu
    v-model="menu"
    ref="menu"
    :close-on-content-click="false"
    :nudge-right="40"
    transition="scale-transition"
    offset-y
    min-width="auto"
  >
    <template v-slot:activator="{ on, attrs }">
      <v-text-field
        :dense="dense"
        :outlined="outlined"
        :placeholder="placeholder"
        :filled="filled"
        :rounded="rounded"
        @blur="$emit('blur', $event)"
        prepend-inner-icon="mdi-calendar-month"
        readonly
        v-bind="attrs"
        v-model="fecha"
        v-on="on"
      ></v-text-field>
    </template>
    <v-date-picker
      :range="range"
      :disabled="disabled"
      :max="max"
      :min="min"
      :show-current="current"
      v-model="fecha"
    >
      <v-btn text color="primary" @click="menu = false"> Cancel </v-btn>
      <v-btn text color="primary" @click="saveData(fecha)"> OK </v-btn>
    </v-date-picker>
  </v-menu>
</template>
<script>
export default {
  name: "Date-Picker-Global",
  props: {
    current: null,
    range: {
      type: Boolean,
      default: false,
    },
    outlined: {
      type: Boolean,
      default: () => false,
    },
    min: {
      type: String,
      default: () => "",
    },
    max: {
      type: String,
      default: () => "",
    },
    dense: {
      type: Boolean,
      default: () => false,
    },
    rounded: {
      type: Boolean,
      default: () => false,
    },
    placeholder: {
      type: String,
      default: () => "DD/MM/YYYY",
    },
    filled: {
      type: Boolean,
      default: () => false,
    },
    disabled: {
      type: Boolean,
      default: () => false,
    },
  },
  data: () => ({
    menu: false,
    fecha: null,
  }),
  methods: {
    saveData(fecha) {
      this.$emit("input", fecha);
      this.menu = false;
    },
  },
};
</script>
