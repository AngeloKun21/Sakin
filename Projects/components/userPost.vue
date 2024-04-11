<template>
    <div class="bg-gradient-to-r from-gray-600 to-blue-400">
        <a-row class="justify-center">
            <a-col :span="12" class="m-3 rounded-2xl" v-for="(data, index) in userDetails" :key="index">
                <a-flex class="items-center justify-center rounded-2xl justify-items-stretch h-full justify-items-center">
                    <a-card  hoverable class="border border-gray-400" style="background-color: #E1ECF7; max-width: 1000px; max-height: 300px;">
                        <a-row type="flex" justify="center">
                            <a-col :span="5" class="flex flex-col items-center self-center">
                                <img class="rounded-xl border-gray-800 border-2 bg-white h-28" alt="example" :src="data.image" /><br>
                                <p class="font-mono text-center text-sm font-bold">{{ data.firstName }} {{ data.lastName }}</p>
                            </a-col>
                            <a-col :span="19" >
                                <template v-for="(posts, postIndex) in postDetails">
                                    <p v-if="postIndex === index" :key="postIndex" class="font-mono font-bold text-base uppercase text-center"> {{ posts.title }} <br> <br></p>
                                    <p v-if="postIndex === index" :key="postIndex" class="font-mono text-justify px-2">{{ posts.body }}</p>
                                </template>
                            </a-col>
                        </a-row>
                    </a-card>
                </a-flex>
            </a-col>
        </a-row>
    </div>
</template>


<script lang='ts' setup>
import {ref} from 'vue'

interface Data{
    firstName: string,
    lastName: string,
    image: string
}
interface Post{
    title: string,
    body: string,
    tags: string
}

let postDetails = ref<Post[]>([]);
let userDetails = ref<Data[]>([]);
async function userData(){
    //USER DATA
    const data = await fetch('https://dummyjson.com/users')
        .then(res => res.json())
        .then(data => {return data.users});
    userDetails.value = data
    console.log("USERS :>>",data)
    //USER POST
    const posts= await fetch(`https://dummyjson.com/posts`)
        .then(res => res.json())
        .then(posts => {return posts.posts});
        postDetails.value = posts
        console.log("POSTS :>>",postDetails)
}
userData()



function data() {
    throw new Error('Function not implemented.');
}
</script>