<template>
  <div>
    <div>
      <span>List of connections</span>
      <b-table striped hover :items="connections" :fields="connections_fields"></b-table>
    </div>
    <div>
      <span>List of connections</span>
      <b-table striped hover :items="people" :fields="people_fields"></b-table>
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
    }
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
