<template>
    <div class="single-Img">
        <p><router-link to="/">&lt;-- Back to all images</router-link></p>
        <img :src="img.src" :alt="img.alt" height="100%">

        <div class="img-info">
            <p>Description: {{ img.alt || "No description added yet" }}</p>
            <p>ID: {{ img._id }}</p>
            <p>Type: {{ img.nsfw == true ? "NSFW" : "Safe" }}</p>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'singleImg',
    data() {
        return {
            img: {}
        }
    },
    mounted() {
        axios.get(`${process.env.VUE_APP_URI}images/${this.$route.params.id}`)
            .then(res => {
                this.img = res.data;
            })

    }
}
</script>

<style scoped>
.single-Img {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100%;
    width: 100%;
}
img { 
    max-width: 100vh;
    max-height: 100vh;
}
</style>