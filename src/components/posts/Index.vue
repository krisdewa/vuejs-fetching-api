<template>
    <div class="container mt-custom">
        <div class="row">
            <div class="col-md-12">
                <div class="card border-0 rounded shadow">
                    <div class="card-body">
                        <h4>DATA POST</h4>
                        <hr>
                        <router-link :to="{ name: 'posts.create' }" class="btn btn-md btn-success">TAMBAH POST
                        </router-link>

                        <table class="table table-striped table-bordered mt-4">
                            <thead class="thead-dark">
                                <tr>
                                    <th scope="col">TITLE</th>
                                    <th scope="col">CONTENT</th>
                                    <th scope="col">OPTIONS</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(post, index) in posts" :key="index">
                                    <td>{{ post.title }}</td>
                                    <td>{{ post.content }}</td>
                                    <td class="text-center">
                                        <router-link :to="{ name: 'posts.edit', params: { id: post.id } }"
                                            class="btn btn-sm btn-primary me-2">EDIT</router-link>
                                        <button @click.prevent="postDelete(post.id)"
                                            class="btn btn-sm btn-danger ml-1">DELETE</button>
                                    </td>
                                </tr>
                            </tbody>
                        </table>

                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import { onMounted, ref } from 'vue'

export default {
    name: 'IndexPosts',
    setup() {

        //reactive state
        let posts = ref([])

        //mounted
        onMounted(() => {

            //panggil function "getDataPosts" 
            getDataPosts()

        })

        //function "getDataPosts"
        function getDataPosts() {

            //get API from Express Backend
            axios.get('http://localhost:3000/api/posts')
                .then(response => {

                    //assign state posts with response data
                    posts.value = response.data.data

                }).catch(error => {
                    console.log(error.response.data)
                })
        }

        // function "postDelete"
        function postDelete(id) {

            //delete data post by ID
            axios.delete(`http://localhost:3000/api/posts/delete/${id}`)
                .then(() => {

                    //panggil function "getDataPosts"  
                    getDataPosts()

                }).catch(error => {
                    console.log(error.response.data)
                })
        }

        //return
        return {
            posts,
            getDataPosts,
            postDelete
        }

    }

}
</script>