<template>
    <div class="admin-home">
        <div class="updateToken">
            Add token
            <form>
            <input type="text" v-model="token">
            <input type="submit" @click="login()">
        </form>
        </div>
        <div class="images">
            <h1>Admin home lol</h1>
        <!-- admin img updates comp -->
        <adminImgUpdates v-for="img in images" :key="img._id" :img="img" />
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import adminImgUpdates from '../../components/admin-img-updates.vue'
export default {
    name:"AdminHome",
    data() {
        return {
            images: [],
            token: null,
        }
    },
    components: {
        adminImgUpdates
    },
    methods: {
        getImages() {
            axios.get(`${process.env.VUE_APP_URI}/images`)
            .then(res => {
                this.images = res.data;
            })
            .catch((err) => {
                return err;
            })
        },
        login() {
            localStorage.setItem('token', this.token)
        }
    },
    mounted() {
        this.getImages()
        if(!this.token) {
            if(!localStorage.getItem('token')) return this.token = null;
                this.token = localStorage.getItem('token')
        }
    }
}
</script>