<template>
  <q-page class="container">

      <div id="header">
          <h4>Register</h4>
          <hr>
      </div>

      

  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'PageForm',
  data(){
      return {
          form:{
              name: '',
          }
      }
  },
})
</script>

<style scoped>
    h4{
        font-weight: 500;
        margin-bottom: 5px;
    }

    .container{
        margin: 30px;
    }
</style>
