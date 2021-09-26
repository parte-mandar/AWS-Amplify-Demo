<template>
  <h3>Hello world</h3>
  <button @click="createAuthor">Create Author</button>
  <button @click="queryAuthors">Query Authors</button>
  <div v-for="author in authors" :key="author.id">
    <h1>
      {{author.first_name}}
    </h1>
    <h5>
      {{author.last_name}}
    </h5>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import { DataStore } from '@aws-amplify/datastore';
// import { Posts } from './models';
import { Authors } from './models';


export default {
  name: 'App',
  data:(()=>({
    authors: []
  })),
  components: {
  },
  methods:{
    async createAuthor(){
      await DataStore.save(
        new Authors({
          "first_name": "Rajendra",
          "last_name": "Parte"
        })
      );
    },
    async queryAuthors() {
      const models = await DataStore.query(Authors);
      this.authors = models
      console.log(models);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
