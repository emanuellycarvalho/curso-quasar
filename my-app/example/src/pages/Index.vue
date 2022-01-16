<template>
  <q-page class="row">
      <div class="col q-pa-md">
          <q-table
          title="Users"
          :columns="columns"
          :data="users"
          row-key="Name"
          dark
          bordered
          class="my-sticky-header-table"
          color="amber" />
      </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'
import axios from 'axios';

export default defineComponent({
  name: 'PageIndex',
  data(){
    return {
      columns: [
        {
          name: 'Name',
          label: 'Name',
          field: 'Name',
          align: 'left',
          sortable: true
        },
        {
          name: 'Username',
          label: 'Username',
          field: 'Username',
          align: 'left',
          sortable: true
        },
        {
          name: 'Email',
          label: 'Email',
          field: 'Email',
          align: 'left',
        },
        {
          name: 'Website',
          label: 'Website',
          field: 'Website',
          align: 'left',
        },
      ],
      users: ''
    }
  },

  mounted(){
    this.$axios = axios;
    this.getPosts();
  },

  methods: {
    getPosts(){
      this.$axios.get('https://jsonplaceholder.typicode.com/users')
      .then((response) => {
        this.users = response.data;
        console.clear();
        console.log(response.data);
        console.log(this.users);
      })
      .catch((error) => {
        console.log(error);
      })
      .finally(() => {

      });
    }
  }
})
</script>
