<template>
  <data-table />
</template>

<script lang="ts">
import { defineComponent } from 'vue';

// Components
import DataTable from '../components/DataTable.vue';

export default defineComponent({
  name: 'DashboardView',

  components: {
    DataTable,
  },
});
</script>
