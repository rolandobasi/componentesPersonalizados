<!-- eslint-disable vue/no-mutating-props -->
<template>
  <v-row justify="center">
    <v-dialog
      v-model="value"
      content-class="elevation-0"
      :max-width="max"
      persistent
    >
      <v-card class="rounded-xl" height="auto">
        <v-card-title class="text-h5 primary--text text-center">
          <section class="container">
            <slot name="container-title" />
            <v-icon
              v-if="custom"
              color="gray"
              @click="$emit('input', false)"
              class="btn-close-custom"
            >
              mdi-close-box
            </v-icon>
          </section>
        </v-card-title>
        <v-divider />
        <v-spacer></v-spacer>
        <div class="d-flex align-center justify-center mt-5" v-if="icon">
          <v-icon
            x-large
            class="bluePatologia--text"
            color="primary"
            style="font-size: 100px"
          >
            {{ icon }}
          </v-icon>
        </div>
        <p :class="`${colorText}--text text-center`">
          {{ description }}
        </p>

        <section class="container">
          <slot name="container-main" />
        </section>

        <v-spacer />
        <v-divider />
        <div class="actions-buttons d-flex justify-end pb-4 mt-5 mr-5">
          <slot name="actions" />
        </div>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
export default {
  name: "Global-Modal-Simple",
  props: {
    description: String,
    custom: Boolean,
    icon: String,
    colorText: String,
    value: Boolean,
    max: {
      type: Number,
      default: 600,
    },
  },
};
</script>

<style scoped>
.description {
  padding: 0 50px 0 50px;
  font-size: 18px;
}

.actions-buttons button {
  margin-right: 30px;
}
.btn-close-custom {
  position: absolute;
  top: 10px;
  right: 15px;
}
.centrat-icono {
  position: fixed;
  top: 30%;
  right: 25%;
}
</style>
