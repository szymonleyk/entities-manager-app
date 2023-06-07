<template>
  <add-customer-dialog/>
  <data-table />
</template>

<script lang="ts">
import { defineComponent } from 'vue';

// Components
import DataTable from '../components/DataTable.vue';
import AddCustomerDialog from '../components/AddCustomerDialog.vue'

export default defineComponent({
  name: 'DashboardView',

  components: {
    DataTable,
    AddCustomerDialog
  },
});
</script>
