<template>
    <div class="container mt-custom">
        <div class="row">
            <div class="col-md-12">
                <div class="card border-0 rounded shadow">
                    <div class="card-body">
                        <h4>EDIT POST</h4>
                        <hr>
                        <div v-if="validation.errors" class="mt-2 alert alert-danger">
                            <ul class="mt-0 mb-0">
                                <li v-for="(error, index) in validation.errors" :key="index">{{ `${error.param} :
                                                                    ${error.msg}`
                                }}</li>
                            </ul>
                        </div>
                        <form @submit.prevent="update">
                            <div class="form-group">
                                <label for="title" class="font-weight-bold mb-2">TITLE</label>
                                <input type="text" class="form-control" v-model="post.title"
                                    placeholder="Masukkan Judul Post">
                            </div>
                            <div class="form-group mt-3">
                                <label for="content" class="font-weight-bold mb-2">CONTENT</label>
                                <textarea class="form-control" rows="4" v-model="post.content"
                                    placeholder="Masukkan Konten Post"></textarea>
                            </div>
                            <button type="submit" class="btn btn-primary mt-3">UPDATE</button>
                        </form>

                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { reactive, ref, onMounted } from 'vue'
import { useRouter, useRoute } from 'vue-router'
import axios from 'axios'

export default {
    name: 'EditPosts',
    setup() {

        //state posts
        const post = reactive({
            title: '',
            content: ''
        })

        //state validation
        const validation = ref([])

        //vue router
        const router = useRouter()

        //vue router
        const route = useRoute()

        //mounted
        onMounted(() => {

            //get API from Backend
            axios.get(`http://localhost:3000/api/posts/${route.params.id}`)
                .then(response => {

                    //assign state posts with response data
                    post.title = response.data.data.title
                    post.content = response.data.data.content

                }).catch(error => {
                    console.log(error.response.data)
                })

        })

        //method update
        function update() {

            let title = post.title
            let content = post.content

            axios.patch(`http://localhost:3000/api/posts/update/${route.params.id}`, {
                title: title,
                content: content
            }).then(() => {

                //redirect ke post index
                router.push({
                    name: 'posts.index'
                })

            }).catch(error => {
                //assign state validation with error 
                validation.value = error.response.data
            })

        }

        //return
        return {
            post,
            validation,
            router,
            update
        }

    }

}
</script>