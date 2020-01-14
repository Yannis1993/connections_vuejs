<template>
  <div>
    <div>
      <span>Create a new person</span>
      <b-form inline style="margin-left: auto;margin-right: auto;width: 50%;">
        <label class="sr-only" for="inline-form-input-name">Last Name</label>
        <b-input
          id="inline-form-input-name"
          class="mb-2 mr-sm-2 mb-sm-0"
          placeholder="Last Name"
          v-model="person.last_name"
        ></b-input>

        <label class="sr-only" for="inline-form-input-name" >First Name</label>
        <b-input
          id="inline-form-input-name"
          class="mb-2 mr-sm-2 mb-sm-0"
          placeholder="First Name"
          v-model="person.first_name"
        ></b-input>

        <label class="sr-only" for="inline-form-input-email">Email</label>
        <b-input-group prepend="@" class="mb-2 mr-sm-2 mb-sm-0">
          <b-input id="inline-form-input-email" v-model="person.email" placeholder="Email"></b-input>
        </b-input-group>

        <b-button variant="primary" @click="addPerson">Create</b-button>
      </b-form>
    </div>

    <div>
      <span>List of people</span>
      <b-table striped hover :items="people" :fields="people_fields"></b-table>
    </div>

    <div>
      <span>List of connections</span>
      <b-table striped hover :items="connections" :fields="connections_fields"></b-table>
    </div>
  </div>
</template>

<script>
const BASE_URL = process.env.VUE_APP_BASE_URL;
const CONNECTIONS_END_POINT = '/connections';
const PEOPLE_END_POINT = '/people';
import axios from 'axios';
  export default {
    data() {
      return {
        // Note `isActive` is left out and will not appear in the rendered table
        connections_fields: ['id', 'connection_type', 'from_person_id', 'to_person_id'],
        people_fields: ['id', 'email', 'first_name', 'last_name'],
        connections: [],
        people: [],
        person: {
          first_name: '',
          email: '',
          last_name: '',
        },
        error: ''
      }
    },
    mounted() {
      axios.get(BASE_URL + CONNECTIONS_END_POINT).then(response => (
        this.connections = response.data
      )).catch(error => {
        this.errorMsg = 'No user or no location!'
        this.error = error
        this.data = []
      })
      axios.get(BASE_URL + PEOPLE_END_POINT).then(response => (
        this.people = response.data
      )).catch(error => {
        this.errorMsg = 'No user or no location!'
        this.error = error
        this.data = []
      })
    },
    methods: {
      addPerson() {
        return new Promise((resolve, reject) => {
          axios.post(BASE_URL + PEOPLE_END_POINT, {
            first_name: this.person.first_name,
            last_name: this.person.last_name,
            email: this.person.email,
          })
          .then(response => {
            resolve(response)
          })
          .catch(error => {
            reject(error.response.data)
          })
        })
      }
    },
}
  
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h3 {
    margin: 40px 0 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }
</style>
