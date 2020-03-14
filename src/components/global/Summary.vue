<template>
    <div>
        <img v-show="isImageLoaded" class="img-fluid" alt="Corona logo" :src="urlImageSummary" @load="onImgLoad">
        <h1 v-if="!isImageLoaded"><strong>{{ title }}</strong></h1>
        <p>
          Serving data from John Hopkins University CSSE as a JSON API via <a href="https://covid19.mathdro.id/api">mMathdroid API</a>
        </p>
    </div>
</template>

<script>
    import {
        APIServiceCovid
    } from '../../services/APIServiceCovid';

    const apiService = new APIServiceCovid();

    export default {
        name: "HeaderSummary",
        data() {
            return {
                title: "COVID-19",
                urlImageSummary: String,
                isImageLoaded: false
            };
        },
        methods: {
            getUrlImageSummary() {
                apiService.getDataGlobal().then((data) => {
                    this.urlImageSummary = data.image;
                });
            },
            onImgLoad () {
                this.isImageLoaded = true;
            }
        },
        mounted() {
            this.getUrlImageSummary();
        },
    }
</script>

<style scoped>

</style>
