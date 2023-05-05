<script setup>
import { computed, ref } from 'vue';
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

const posts = ref([]);
const postXpage = 10
const inicio = ref(0)
const fin = ref(postXpage)

const loading = ref(true)

const favorito = ref('');


const cambiarFavorito = (title) =>{
  favorito.value = title
}

const next= ()=>{
  inicio.value += postXpage
  fin.value += postXpage
}
const previus= ()=>{
  inicio.value -= postXpage
  fin.value -= postXpage
}

const fetchData = async()=>{
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json()
  } catch (error) {
    console.log(error)
  }finally{
    loading.value = false
  }
}

fetchData()

// fetch('https://jsonplaceholder.typicode.com/posts')
// .then(res => res.json())
// .then(data => posts.value = data)
// .catch(e=> console.log(e))
// .finally(()=> loading.value = false)

const maxPage = computed(()=> posts.value.length) 
</script>

<template>

  <LoadingSpinner v-if="loading"></LoadingSpinner>
  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mi post Favorito es: {{ favorito }}</h2>

    
    <PaginatePost 
      @previus="previus" 
      @next="next" 
      class="mb-2"
      :inicio="inicio"
      :fin="fin"
      :maxPage="maxPage"></PaginatePost>

    <BlogPost
      v-for="post in posts.slice(inicio, fin)"
      :key="post.id"
      :title="post.title" 
      :id="post.id" 
      :body="post.body"
      @cambiarFavorito="cambiarFavorito"
      class="mb-2"
    ></BlogPost>
  </div>
</template>

