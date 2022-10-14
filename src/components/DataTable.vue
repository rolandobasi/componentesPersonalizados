<template>
  <div>
    <v-data-table
      :headers="headers"
      :items="response.rows"
      :page.sync="paginator.page"
      :items-per-page="paginator.per_page"
      class="elevation-1"
      locale="es"
      hide-default-footer
      id="mytable"
      :single-select="false"
      :show-select="selectable"
      v-model="selecteds"
      :item-key="itemKey"
    >
      <template v-for="(index, name) in $scopedSlots" v-slot:[name]="data">
        <slot :name="name" v-bind="data"></slot>
      </template>
      <template v-slot:[`item.actions`]="{ item }">
        <slot :name="ac.eventName" v-for="ac in actions" v-bind="{ ac, item }">
          <DataTableButton
            :key="ac.eventName"
            :icon="ac.icon.name"
            :icon-color="ac.icon.color"
            :tooltipText="ac.tooltip.text"
            :tooltipColor="ac.tooltip.color"
            @click="$emit(ac.eventName, item)"
          />
        </slot>
      </template>
      <template #no-data> Sin Datos que Mostrar </template>
    </v-data-table>

    <v-pagination
      v-if="pagination"
      v-model="paginator.page"
      @input="setPage($event)"
      :length="totalPage"
      color="blueGrayMinsal"
    ></v-pagination>
  </div>
</template>

<script>
import DataTableButton from "@/components/DataTableButton";

export default {
  name: "DataTable",
  components: {
    DataTableButton,
  },
  props: {
    headers: {
      type: Array,
      required: true,
      default() {
        return [];
      },
    },
    response: {
      type: [Object, Array],
      required: true,
    },
    selectable: {
      type: Boolean,
      required: false,
      default: false,
    },
    actions: {
      type: Array,
      required: false,
      default() {
        return [
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
            eventName: "show",
          },
        ];
      },
    },
    pagination: {
      type: Boolean,
      default: true,
    },
    itemKey: {
      type: String,
      default: "id",
    },
  },
  data() {
    return {
      items: [],
      totalPage: 1,
      pagina: 1,
      paginator: {
        pagina: 1,
        per_page: 1,
      },
      selecteds: [],
    };
  },
  watch: {
    selecteds: {
      handler() {
        this.$emit("input", this.selecteds);
      },
    },
  },
  created() {
    this.items = this.response.rows;
    this.paginator.page = this.response.page;
    this.totalPage = this.response.totalPages;
    this.paginator.per_page = this.response.perPage;
  },
  updated() {
    this.items = this.response.rows;
    this.paginator.page = this.response.page;
    this.totalPage = this.response.totalPages;
    this.paginator.per_page = this.response.perPage;
  },
  methods: {
    print(slots) {
      console.log(slots);
    },
    setPage(e) {
      this.paginator.page = e;
      this.$emit("paginate", { pagina: e, per_page: this.response.perPage });
    },
    paginate() {
      this.$emit("paginate", this.paginator);
    },
  },
};
</script>

<style></style>
