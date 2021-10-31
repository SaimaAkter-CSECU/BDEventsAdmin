<template>
    <div>
        <!-- <Header />
        <v-main>
            <v-container> -->
                <!-- <AllEvents /> -->
                <!-- <Nuxt /> -->
            <!-- </v-container>
        </v-main>
        <Footer /> -->
    </div>
</template> 

<script>
export default {
    mounted() {
        this.$nuxt.$router.push({path:'/Dashboard/Events/All-Events'})
    },
}
</script>

