<template>
    <div class="img-update">
        <img :src="img.src" class="image" height="200px">
        <form @submit.prevent class="form">
            <input type="text" v-model="image.alt">
            <input type="checkbox" v-model="image.nsfw">
            <input type="text" v-model="image.category">
            <button @click="update()">Submit</button>
        </form>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'adminImgUpdates',
    props: ['img'],
    data() {
        return {
            image: {
                nsfw: false,
                alt: ''
            }
        }
    },
    mounted() {
        this.image = this.img;
    },
    methods: {
        update() {
            axios.patch(`${process.env.VUE_APP_URI}/admin/images/${this.image._id}`,this.image, {
                headers: {
                    'authorization': localStorage.getItem('token')
                },
            })
                .then(res => {
                    console.log(res.data)
                    this.image = res.data;
                })
                .catch(err => {
                    console.log(err)
                })
        }
    }
}
</script>

<style scoped>
/* form next to the image */
.img-update {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    margin: 10px;
}

</style>