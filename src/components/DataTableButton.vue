<template>
  <v-tooltip top :color="tooltipColor">
    <template v-slot:activator="{ on }">
      <v-icon v-on="on" :color="iconColor" class="mr-2" @click="$emit('click')">
        {{ icon }}
      </v-icon>
    </template>
    <span>{{ tooltipText }}</span>
  </v-tooltip>
</template>

<script>
export default {
  name: "DataTableButton",
  props: {
    tooltipText: String,
    tooltipColor: String,
    icon: String,
    iconColor: String,
  },
};
</script>

<style></style>
