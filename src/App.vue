<template>
  <form @submit.prevent="save">
    <input type="text" v-model="form.tittle"><br>
    <textarea v-model="form.content"></textarea><br>
    <button class="btn btn-primary" type="submit">Save</button>
  </form>
  <div>
    <ul>
      <li v-for="article in articles" :key="article.id" >
        {{ article.tittle }} <br>
        {{ article.content }}
      </li>
    </ul>
    <button class="btn btn-warning" @click="load">Load</button>
  </div>
</template>

<script>
import axios from 'axios'
/* eslint-disable */
  export default {
    data(){
      return {
        form:{
          tittle:'',
          content: ''
        },
        articles: []
      }
    },

    async mounted(){
      //this.load()
    },

    methods:{
      async load(){
        const response = await axios.get('http://localhost:3000/articles')
        this.articles = response.data
      },

      async save(){
        try{
          const response = await axios.post('http://localhost:3000/articles', this.form)
          //this.articles = response.data
          this.load()
          this.tittle=''
          this.content=''
        } catch(e){
          console.log(e)
        } 
      }
    }
  }
</script>