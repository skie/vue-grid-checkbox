<template>
  <div id="app">
    <button v-on:click="loadData">LoadData</button>
    <ejs-grid
      ref="gridObj"
      height="150px"
      :enableInfiniteScrolling="true"
      :pageSettings="pageSettings"
      :load="load"
    >
      <e-columns>
        <e-column type="checkbox" width="80"></e-column>
        <e-column
          field="OrderID"
          headerText="ID"
          width="80"
          isPrimaryKey="true"
        ></e-column>
        <e-column
          field="CustomerID"
          headerText="CustomerID"
          width="90"
        ></e-column>
        <e-column field="ShipCity" headerText="ShipCity" width="120"></e-column>
      </e-columns>
    </ejs-grid>
  </div>
</template>
<script>
import Vue from "vue";
import axios from "axios";
import { data } from "./datasource.js";
import {
  GridPlugin,
  Freeze,
  Edit,
  Toolbar,
  Page,
  Filter,
  ColumnChooser,
  InfiniteScroll,
} from "@syncfusion/ej2-vue-grids";
import { ButtonPlugin } from "@syncfusion/ej2-vue-buttons";
Vue.use(ButtonPlugin);
Vue.use(GridPlugin);

export default {
  data() {
    return {
      data: data,
      pageSettings: {
        pageSize: 8,
      },
    };
  },
  methods: {
    load: function () {},
    loadData() {
      debugger;
      this.$refs.gridObj.dataSource = this.data;
    },
  },
  provide: {
    grid: [Freeze, InfiniteScroll, Edit, Toolbar, Page, Filter, ColumnChooser],
  },
};
</script>

<style>
@import "https://cdn.syncfusion.com/ej2/material.css";
</style>
