<template>
  <div >
    <HeaderComp/>
            <div class="container">

                <ul>
                    <li
                    class="pt-5"
                    v-for="post in posts"
                    :key="post.id"
                    >
                        <h3> Titolo: {{ post.title }}</h3>
                        <p> Contenuto :{{ post.content }}</p>
                        <h4> Categoria :{{ post.category.name }}</h4>
                        <h5 v-if="post.tags.length === 0">nessun tag</h5>
                        <h5 v-else-if="post.tags.length > 0">{{ post.tags.name }}</h5>


                    </li>
                </ul>

            </div>
    <FooterComp/>


  </div>
</template>

<script>
import Axios from 'axios';
import HeaderComp from './components/partials/HeaderComp.vue';
import FooterComp from './components/partials/FooterComp.vue';

export default {
  components: { HeaderComp, FooterComp },
    name: "App",

    data(){
        return{
            apiUrl : "http://127.0.0.1:8000/api/posts",
            posts : [],
        }
    },

    mounted(){
        this.getApi();
    },

    methods:{
        getApi(){
            axios.get(this.apiUrl)
            .then(res =>{
                this.posts = res.data;

            })
        }
    }


}
</script>

<style>

</style>
