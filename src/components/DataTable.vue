<template>
  <v-table density="compact">
    <thead>
      <tr>
        <th class="text-left" v-for="item in headers">
          {{ item }}
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in customers" :key="item.name">
        <td>{{ item.name }}</td>
        <td>{{ item.email }}</td>
        <td>{{ item.vat }}</td>
        <td>
          <v-icon size="small" class="me-2" @click="editItem(item.id)">
            mdi-pencil
          </v-icon>
          <v-icon size="small" @click="deleteItem(item.id)">
            mdi-delete
          </v-icon>
        </td>
      </tr>
    </tbody>
  </v-table>
</template>

<script>
import axios from 'axios';
export default {

  data() {
    return {
      headers: ['Name', 'E-mail', 'Vat', 'Actions'],
      customers: [],
    }
  },

  created() {
    axios.get(`http://localhost:3333/api/v1/customers`)
      .then(response => {
        console.log(response.data);
        this.customers = response.data
      })
      .catch(e => {
        this.errors.push(e)
      })
  },

  methods: {
    editItem(id) {
      this.editedIndex = this.desserts.indexOf(item)
      this.editedItem = Object.assign({}, item)
      this.dialog = true
    },

    deleteItem(id) {
      console.log(id)
      axios.delete(`http://localhost:3333/api/v1/customers/${id}`)
        .then((response) => {
          console.log(`Customer with ID ${id} deleted successfully`);
          console.log(response.data);
        })
        .catch((error) => {
          console.error(`Error deleting customer with ID ${id}`);
          console.error(error);
        });
    },
  }


}
</script>