<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Event Organizer Detail
        </div>
        <v-card
            elevation="3"
        >
            <v-card-title>
                <v-spacer></v-spacer>
                <v-btn
                    class="ml-3"
                    color="primary"
                    v-show="viewMode"
                    @click="viewMode = false"
                >
                    Edit
                </v-btn>
                <v-btn
                    class="ml-3"
                    color="grey darken-2"
                    v-show="!viewMode"
                    @click="viewMode = true"
                >
                    Cancel
                </v-btn>
            </v-card-title>
            <div
                v-if="viewMode"
                class="pa-7"
            >
                <v-row>
                    <v-col
                        col="12"
                        md="4"
                        sm="6"
                        xs="12"
                    >
                        <v-list-item two-line>
                            <v-list-item-content>
                                <v-list-item-title class="text-h6 font-weight-regular">id</v-list-item-title>
                                <v-list-item-subtitle class="subtitle-1 mt-2">{{viewOrganizerId}}</v-list-item-subtitle>
                            </v-list-item-content>
                        </v-list-item>
                    </v-col>
                    <v-col
                        col="12"
                        md="4"
                        sm="6"
                        xs="12"
                    >
                        <v-list-item two-line>
                            <v-list-item-content>
                                <v-list-item-title class="text-h6 font-weight-regular">Organizer</v-list-item-title>
                                <v-list-item-subtitle class="subtitle-1 mt-2">{{viewName}}</v-list-item-subtitle>
                            </v-list-item-content>
                        </v-list-item>
                    </v-col>
                </v-row>
            </div>
            <div
                v-else
                class="pa-7"
            >
                <v-form
                    ref="form"
                    v-model="valid"
                    lazy-validation
                >
                    <v-text-field
                        v-model="id"
                        :rules="inputRules"
                        label="Organizer Id"
                        outlined
                        required
                        readonly
                    ></v-text-field>

                    <v-text-field
                        v-model="organizer"
                        :rules="inputRules"
                        label="Organization Name"
                        outlined
                        required
                    ></v-text-field>

                    <v-btn
                        :disabled="!valid"
                        class="btn-style mr-4"
                        large
                        @click="UpdateOrganizerInfo"
                        elevation="0"
                    >
                        Update Organizer Info
                    </v-btn>

                    <v-btn
                        color="grey darken-2"
                        class="mr-4"
                        @click="reset"
                        large
                        elevation="0"
                    >
                        Cancel
                    </v-btn>
                </v-form>
            </div>
        </v-card>

        <v-snackbar
            v-model="snackbar"
            timeout="2000"
            color="secondary"
        >
            {{snackbarText}}

            <template v-slot:action="{ attrs }">
                <v-btn
                    color="white"
                    text
                    v-bind="attrs"
                    @click="snackbar = false" 
                >
                Close
                </v-btn>
            </template>
        </v-snackbar>
    </div>
</template>

<script>
    export default {
        name: 'BlogCategoryDetail',
        data:()=>({
            viewMode: true,
            organizerInfo:[
                {
                    id: 2,
                    org: 'BCC AP',
                }
            ],
            
            snackbar: false,
            snackbarText: '' ,
            valid: true,
            id: '',
            organizer: '',
            inputRules: [
                v => !!v || 'Organizer Name is required',
            ],
            viewOrganizerId: '',
            viewName: '',
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

        }),
        methods: {
            async UpdateOrganizerInfo(){
                if(this.$refs.form.validate()){
                    let checkOrganizer = this.organizers.find(x=> x.org == this.organizer);
                    if(checkOrganizer){
                        this.snackbarText= 'Organizer Already Exist';
                        this.snackbar= true; 
                    }
                    else{
                        this.snackbarText= 'Organizer Info Updated Successfully';
                        this.snackbar= true;  
                    }
                }
            },
            async reset(){
                this.$nuxt.$router.push({path: '/Dashboard/Events/All-Organizers'})
            }
        },
        mounted() {
            this.id = this.organizerInfo[0].id; 
            this.organizer = this.organizerInfo[0].org;
            this.vieworganizerId = this.organizerInfo[0].id; 
            this.viewName = this.organizerInfo[0].org;
        }
    }
</script>