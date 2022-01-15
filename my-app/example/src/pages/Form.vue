<template>
  <q-page class="container">

      <div id="header">
          <h4>Register</h4>
          <hr>
      </div>

      <div id="form" class="col-lg-8">
          <q-form @submit.prevent.stop="onSubmit()">
              <div class="row w-space q-gutter-md">
                <div class="col">
                    <q-input 
                    v-model="form.name" 
                    type="text" 
                    label="Full Name" 
                    outlined color="secondary"
                    :rules="[
                        val => val && val.length > 0 || 'The name is required.'
                    ]">
                        <template v-slot:prepend>
                            <q-icon name="person"/>
                        </template>
                    </q-input>
                </div>

                <div class="col">
                    <q-input 
                    v-model="form.age" 
                    type="number" 
                    label="Birth Date" 
                    outlined color="secondary"
                    :rules="[
                        val => val && val != null && val != '' || 'The name is required.',
                        val => val && val > 0 && val < 100 || 'Insert a valid age.',
                        val => val && val < 18 || 'Only 18+ can sign in.',
                    ]">
                        <template v-slot:prepend>
                            <q-icon name="person"/>
                        </template>
                    </q-input>
                </div>
            </div>

            <div class="row w-space q-gutter-md">
                <div class="col">
                    <q-input 
                    v-model="form.email" 
                    type="email" 
                    label="E-mail" 
                    outlined color="secondary"
                    :rules="[
                        val => val && val.length > 0 || 'The email is required.'
                    ]">
                        <template v-slot:prepend>
                            <q-icon name="email"/>
                        </template>
                    </q-input>
                </div>

                <div class="col">
                    <q-input 
                    v-model="form.celphone" 
                    type="tel" 
                    label="Celphone" 
                    outlined color="secondary"
                    mask="(##) #####-####"
                    unmasked-value
                    :rules="[
                        val => val && val.length < 0 || 'The celphone is required.',
                        val => val && val.length === 11 || 'Insert a valid celphone number.',
                    ]">
                        <template v-slot:prepend>
                            <q-icon name="telphone"/>
                        </template>
                    </q-input>
                </div>
            </div>

            <div class="col">
                <q-btn
                type="submit"
                label="Submit"
                color="primary"
                class="float-right"/>
            </div>
          </q-form>
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
                age: '',
                email: '',
                celphone: ''
          }
      }
  },

  methods:{
      onSubmit(){
          console.log('submeteu');
      }
  }
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

    .w-space{
        margin-bottom: 15px;
    }
</style>
