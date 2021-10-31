<template>
    <div>
        <div
            class="title-text mb-5"
        >
            All Event Organizers
        </div>
        <v-card>
            <v-card-title>
                <v-spacer></v-spacer>
                <v-text-field
                    v-model="search"
                    append-icon="mdi-magnify"
                    label="Search"
                    single-line
                    hide-details
                >
                </v-text-field>
            </v-card-title>
            <v-data-table
                :headers="headers"
                :items="organizers"
                :search="search"
                elevation="3"
                @click:row="goToOrganizerDetail()"
                class="dataTable"
            ></v-data-table>
        </v-card>
    </div>
</template>

<script>
    export default {
        name: 'AllEventOrganizers',
        data () {
            return {
                search: '',
                headers:[
                    {
                        text: '#',
                        sortable: true,
                        value: 'id', 
                    },
                    {
                        text: 'Organization Name',
                        sortable: true,
                        value: 'org', 
                    },                   
                ],
                organizers: [
                    {
                        id: 1, 
                        org: 'BCC', 
                    },
                    {
                        id: 2, 
                        org: 'LICT', 
                    },
                    {
                        id: 3, 
                        org: 'BITM', 
                    },
                    {
                        id: 4, 
                        org: 'BUBT', 
                    },
                    {
                        id: 5, 
                        org: 'SUST', 
                    },
                    {
                        id: 6, 
                        org: 'CUET', 
                    },
                    {
                        id: 7, 
                        org: 'BUET', 
                    },
                    {
                        id: 8, 
                        org: 'BCC AP', 
                    },
                ],
            }
        },
        methods: {
            async goToOrganizerDetail(){
                this.$nuxt.$router.push({path:'/Dashboard/Events/Organizer-Detail'});
            }
        }

    }
</script>