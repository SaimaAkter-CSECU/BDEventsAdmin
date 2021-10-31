<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Add New Event Organizer
        </div>
        <div>           
            <v-form
                ref="form"
                v-model="valid"
                lazy-validation
            >
                <v-text-field
                    v-model="organizer"
                    :rules="inputRules"
                    label="Organizer"
                    outlined
                    required
                ></v-text-field>

                <v-btn
                    :disabled="!valid"
                    class="btn-style mr-4"
                    large
                    @click="addOrganizer"
                    elevation="0"
                >
                    Add Organizer
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
        name: 'AddNewBlogCategory',
        data: ()=>({
            valid: true,
            organizer: '',
            inputRules: [
                v => !!v || 'This Field is Required',
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
            snackbar: false,
            snackbarText: '' , 
        }),
        methods: {
            addOrganizer() {
                if(this.$refs.form.validate()){
                    let checkOrganizer = this.organizers.find(x=> x.org == this.organizer);
                    if(checkOrganizer){
                        this.snackbarText= 'Organizer Already Exist';
                        this.snackbar= true; 
                    }
                    else{
                        this.snackbarText= 'Organizer Added Successfully';
                        this.snackbar= true; 
                        this.$refs.form.reset(); 
                    }
                }
            },
            reset () {
                this.$refs.form.reset()
            },
        },
    }
</script>