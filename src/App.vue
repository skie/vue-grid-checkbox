<template>
  <div id="app">
    <ejs-grid
      ref="gridObj"
      height="250px"
      :enableInfiniteScrolling="true"
      :pageSettings="pageSettings"
      :dataSource="records"
      :dataStateChange="dataStateChange"
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
      recs: {
          result: [],
          count: 0,
      },
      pageSettings: {
        pageSize: 8,
      },
    };
  },
  computed: {
    records: {
      get() {
        return this.recs;
      },
	}
  },
  methods: {
    load: function () {
      axios.get('data.json').then(({data}) => {
        window.console.log(data);
        this.recs = data;
      });
    },
    loadData() {
      // debugger;
      this.$refs.gridObj.dataSource = this.data;
    },
    dataStateChange() { //state
      // this.$store.dispatch(FETCH_ORDERS, state);
      axios.get('data.json').then(({data}) => {
        window.console.log(data);
        this.recs = data;
      });
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
