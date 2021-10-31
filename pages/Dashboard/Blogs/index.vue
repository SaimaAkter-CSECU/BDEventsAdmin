<template>
    <div>
        <Header />
        <v-main>
            <v-container>
                <nuxt />
            </v-container>
        </v-main>
        <Footer />
    </div>
</template>

<script>
export default {
    mounted() {
        this.$nuxt.$router.push({path:'/Dashboard/Blogs/All-Blogs'}); 
    },
}
</script>