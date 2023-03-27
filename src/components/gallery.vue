<template>
    <div>
        <div class="blur-toggle">
            <!-- <label class="switch">
                <input type="checkbox" v-model="hideNsfw" @change="blurToggle">
                <span class="slider round"></span>
            </label>
            <span>Hide NSFW</span> <br /> -->
        </div>
        <div class="warning">
            <h4>Carfull Friend! I need to manually add the NSFW tag in the database, so some might not be tagged yet sowwy!</h4>
            <h4>Hovering a blurred image will reveal it.</h4>
        </div>
        <div class="image-array">
            <div class="image-container" v-for="img in imageLinks" :key="img._id">
            <router-link :to="`/i/${img._id}`"><img :src="img.src" :alt="img.alt" :class="img.nsfw == true && hideNsfw == true ? 'blur' : `${img.name}-${img.id}`" height="500px" lazy></router-link>
            <div class="alt-text">{{  img.alt  }}</div>
        </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'gallery-comp',
    data() {
        return {
            hideNsfw: true,
            imageLinks: []
        }
    },
    beforeMount() {
        this.nsfw = localStorage.hideNsfw;
        if(!localStorage.nsfw) localStorage.hideNsfw = true;
    },
    mounted() {
        this.getImages();
        setInterval(this.updateImages, 10000);
    },
    methods: {
        // every few update all images.
        updateImages() {
            axios.get(`${process.env.VUE_APP_URI}/images`)
                .then(res => {
                    if(res.data === this.imageLinks) return;
                    this.imageLinks = res.data;
                })
                .catch((err) => {
                    return err;
                })
        },
        // First load
        getImages() {
            axios.get(`${process.env.VUE_APP_URI}/images`)
            .then(res => {
                this.imageLinks = res.data;
            })
            .catch((err) => {
                return err;
            })
        },
        blurToggle() {
            // If nsfw is false, set it to true
            if(!this.nsfw) {
                this.hideNsfw = true;
                localStorage.hideNsfw = true;
            } else {
                this.hideNsfw = false;
                localStorage.hideNsfw = false;
            }
        }
    },
}
</script>

<style scoped>
.imgs {
    display: flex;
    flex-wrap: wrap;
}
.blur {
    filter: blur(20px);
}
.blur:hover {
    filter: blur(0px);
}
.blur-toggle {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
}
.blur-toggle span {
    margin-left: 10px;
}
.blur-toggle label {
    position: relative;
    display: inline-block;
    width: 60px;
    height: 34px;
}
.blur-toggle input {
    opacity: 0;
    width: 0;
    height: 0;
}
.blur-toggle .slider {
    position: absolute;
    cursor: pointer;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: #ccc;
    -webkit-transition: .4s;
    transition: .4s;
}
.blur-toggle .slider:before {
    position: absolute;
    content: "";
    height: 26px;
    width: 26px;
    left: 4px;
    bottom: 4px;
    background-color: white;
    -webkit-transition: .4s;
    transition: .4s;
}
.blur-toggle input:checked + .slider {
    background-color: #2196F3;
}
.blur-toggle input:focus + .slider {
    box-shadow: 0 0 1px #2196F3;
}
.blur-toggle input:checked + .slider:before {
    -webkit-transform: translateX(26px);
    -ms-transform: translateX(26px);
    transform: translateX(26px);
}
.blur-toggle .slider.round {
    border-radius: 34px;
}
.blur-toggle .slider.round:before {
    border-radius: 50%;
}
.img {
    width: 200px;
    height: 200px;
    margin: 10px;
    margin-right: 5px;
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
}
img:hover {
    cursor: pointer;
    /* highlight the imahe with a blue outline */
    outline: 5px solid rgba(46, 0, 83, 0.568);
}

/* blur hover set blur to 0 */
img:hover.blur {
    filter: blur(0px);
}
/* alt at on the image at the bottom */
img:hover:after {
    content: attr(alt);
    position: absolute;
    bottom: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.5);
    color: #fff;
    padding: 5px;
}
.image-array {
    display: flex;
    flex-wrap: wrap;
}
.image-container {
    position: relative;
    display: inline-block;
}

.alt-text {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    background: rgba(0, 0, 0, 0.7);
    padding: 5%;
    font-size: 12px;
    color: #fff;
    text-align: center;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
</style>