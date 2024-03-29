<template>
  <q-page class="container">

      <div id="header">
          <h4>Register</h4>
          <hr>
      </div>

      <div id="form" class="col-lg-8">
          <q-form @submit.prevent.stop="onSubmit()" @reset="onReset" ref="myForm">
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
                    v-model="form.cellphone" 
                    type="tel" 
                    label="Cellphone" 
                    outlined color="secondary"
                    mask="(##) #####-####"
                    unmasked-value
                    :rules="[
                        val => val && val.length > 0 || 'The cellphone is required.',
                        val => val && val.length === 11 || 'Insert a valid cellphone number.',
                    ]">
                        <template v-slot:prepend>
                            <q-icon name="telphone"/>
                        </template>
                    </q-input>
                </div>
            </div>

            <div class="row w-space q-gutter-md">
                <div class="col">
                    <div class="w-space">
                        <q-select 
                        v-model="form.gender" 
                        label="Gender" 
                        :options="genderOptions"
                        emit-value
                        map-options
                        option-label="option" 
                        outlined color="secondary"
                        :rules="[
                            val => val && val.length > 0 || 'Gender identity is required.'
                        ]"
                        />
                    </div>

                    <div class="w-space">
                        <q-input 
                        v-model="form.age" 
                        type="number" 
                        label="Age" 
                        outlined color="secondary"
                        :rules="[
                            val => val && val != null && val != '' || 'The age is required.',
                            val => val && val > 0 && val < 100 || 'Insert a valid age.',
                            val => val && val > 17 || 'Only 18+ can sign in.',
                        ]"/>
                    </div>
                </div>

                <div class="col">
                    <div class="bg-grey-2 q-pa-sm rounded-borders">
                        <p class="section-title">You are representing a</p>
                        <q-option-group
                        name="type"
                        v-model="form.type"
                        :options="typeOptions"
                        class="w-space-sm"
                        />
                    </div>
                </div>
            </div>

            <div class="row w-space">
                <div class="col bg-grey-2 q-pa-lg rounded-borders">
                    <p class="section-title">Please, tell us if you have any difficulties that fit in these areas:</p>
                    <p class="section-subtitle">Select as many as you need</p>
                    <q-option-group
                    v-model="form.difficulties"
                    :options="difficultiesOptions"
                    color="cyan"
                    type="toggle"
                    inline
                    />
                </div>
            </div>

            <div class="row w-space">
                <div class="col">
                    <q-checkbox
                    v-model="form.newsletter"
                    color="primary"
                    label="Do you want to recieve our weekly newsletter?"
                    true-value="yes"
                    false-value="no"/>
                </div>
            </div>

            <div class="col q-gutter-xs">
                <q-btn
                type="reset"
                label="Clear"
                color="warning"
                class="float-right"/>

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
                age: null,
                email: '',
                cellphone: '',
                gender: '',
                type: '',
                difficulties: [],
                newsletter: 'yes'
          },

          genderOptions: [
              { option: 'Feminine', value: 'F'},
              { option: 'Masculine', value: 'M'},
              { option: 'Non binary', value: 'NB'},
              { option: 'Other', value: 'Other'},
          ],

          typeOptions: [
              { label: 'Person', value: 'PF', color: 'cyan' },
              { label: 'Company', value: 'PJ', color: 'negative' },
          ],

          difficultiesOptions: [
              { label: 'Manual', value: 'manual' },
              { label: 'Visual', value: 'visual' },
              { label: 'Respiratory', value: 'respiratory' },
              { label: 'Other(s)', value: 'other' },
          ],
      }
  },

  methods:{
      onSubmit(){
          this.$q.notify({
              message: 'Registered successfully',
              color: 'positive',
              icon: 'check_circle_outline'
          });

          this.onReset();
      },

      async onReset(){
          await this.resetForm();
          this.$refs.myForm.resetValidation();
      },

      async resetForm(){
          this.form = { 
                name: '',
                age: null,
                email: '',
                cellphone: ''             
          }
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

    .w-space-sm{
        margin-bottom: 5px;
    }

    p.section-title{
        font-weight: 500;
        font-size: 18px;
    }

    p.section-subtitle{
        font-size: 13px;
        color: grey;
        margin-top: -10px;
    }
</style>
