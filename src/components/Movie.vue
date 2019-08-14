<template>
    <div class="movie">
        <a @click="openDetail(movie.id)"><img :src="movie.image"/></a>
    </div>
    
</template>

<script>

export default {
    props: {
        movie: {
            type: Object,
            required: true,
            default: () => ({image: "https://scontent.fmcz3-1.fna.fbcdn.net/v/t1.0-9/1013705_464554786963390_1840760218_n.jpg?_nc_cat=100&_nc_oc=AQmdbFdcEexHbdZ7a74xGgUzIx3U-7cGPEovOLG2oBJ2cPxQEs8LHcUgI34ugBrPis4&_nc_ht=scontent.fmcz3-1.fna&oh=f39a052bf018aacf3fc2912793a481ea&oe=5DD2C04A"})
        }
    },
    name: 'movie-component',
    methods: {
        openDetail(value) {
            this.$router.push({
                name: 'movie',
                params: {
                    id: value
                }
            })
        }
    }
}
</script>

<style scoped>

.movie img {
    transition: all 0.6s ease;
}

.movie a :hover {
    transform: scale(1.1);
    box-shadow: 1px 1px 15px #000000;
}

.movie img {
    height: 300px;
    width: 200px;
    margin: 20px;
}

</style>