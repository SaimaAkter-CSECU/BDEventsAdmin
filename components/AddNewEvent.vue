<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Add New Event
        </div>
        <div>   
            <v-card class="pa-7">
                <v-form
                    ref="form"
                    v-model="valid"
                    lazy-validation
                >
                    <v-text-field
                        v-model="title"
                        :rules="inputRules"
                        label="Event Title"
                        outlined
                        required
                    ></v-text-field>

                    <v-textarea
                        v-model="shortDescription"
                        :rules="inputRules"
                        label="Short Description"
                        rows="3" 
                        outlined
                        required
                    ></v-textarea>
                    
                    <client-only>
                        <v-datetime-picker
                            v-model="startDatetime" 
                            label="Start Date Time"
                            :rules="[v => !!v || 'Start Date Time is required']"
                            dateIcon="fas fa-calendar"
                            timeIcon="mdi-clock"
                            outlined
                            required 
                        ></v-datetime-picker>
                    </client-only>

                    <client-only>
                        <v-datetime-picker
                            v-model="endDatetime" 
                            label="End Date Time"
                            :rules="[v => !!v || 'End Date Time is required']"
                            outlined
                            required 
                        ></v-datetime-picker>
                    </client-only>

                    <v-select
                        v-model="category"
                        :items="categories"
                        item-text="cat"
                        item-value="id"
                        :rules="[v => !!v || 'Category is required']"
                        label="Category"
                        outlined
                        required
                    ></v-select>

                    <v-select
                        v-model="status"
                        :items="statuses"
                        item-text="stat"
                        item-value="id"
                        :rules="[v => !!v || 'Status is required']"
                        label="Status"
                        outlined
                        required
                    ></v-select>

                    <v-select
                        v-model="location"
                        :items="locations"
                        item-text="location"
                        item-value="id"
                        :rules="[v => !!v || 'Location is required']"
                        label="Location"
                        outlined
                        required
                    ></v-select>

                    <v-select
                        v-model="venue"
                        :items="venues"
                        item-text="venue"
                        item-value="id"
                        :rules="[v => !!v || 'Venue is required']"
                        label="Venue"
                        outlined
                        required
                    ></v-select>

                    <v-text-field
                        v-model="address"
                        :rules="inputRules"
                        label="Address"
                        outlined
                        required
                    ></v-text-field>

                    <v-text-field
                        v-model="email"
                        :rules="emailRules"
                        label="email"
                        outlined
                        required
                    ></v-text-field>

                    <v-text-field
                        v-model="phone"
                        :rules="inputRules"
                        label="Phone"
                        outlined
                        required
                    ></v-text-field>

                    <v-text-field
                        v-model="webLink"
                        label="Website Link"
                        outlined
                    ></v-text-field>

                    <v-text-field
                        v-model="fbLink"
                        label="Facebook Link"
                        outlined
                    ></v-text-field>

                    <v-text-field
                        v-model="instaLink"
                        label="Instagram Link"
                        outlined
                    ></v-text-field>

                    <v-text-field
                        v-model="twitterLink"
                        label="Twitter Link"
                        outlined
                    ></v-text-field>

                    <v-text-field
                        v-model="youtubeLink"
                        label="Youtube Link"
                        outlined
                    ></v-text-field>

                    <v-select
                        v-model="tag"
                        :items="tags"
                        item-text="tag"
                        item-value="id"
                        :rules="[v => !!v || 'Tags are required']"
                        chips
                        label="Tags"
                        multiple
                        outlined
                        required
                    ></v-select>

                    <client-only>
                        <vue-editor 
                            placeholder="Description..." 
                            v-model="description" 
                            required
                            class="mb-5"
                        ></vue-editor>
                    </client-only>

                    <v-file-input
                        v-model="bannerImage"
                        label="Event Banner Image"
                        prepend-icon=""
                        prepend-inner-icon="mdi-camera"
                        outlined
                        required
                    ></v-file-input>

                    <v-file-input
                        label="Event Image Gallery"
                        prepend-icon=""
                        prepend-inner-icon="mdi-camera"
                        outlined
                        chips
                        multiple 
                        required
                    ></v-file-input>

                    <v-select
                        :items="organizers"
                        item-text="org"
                        item-value="id"
                        :rules="[v => !!v || 'Organizers are required']"
                        chips
                        label="Organizers"
                        multiple
                        outlined
                        required
                    ></v-select>

                    <v-select
                        :items="speakers"
                        item-text="name"
                        item-value="id"
                        chips
                        label="Speakers"
                        multiple
                        outlined
                        required
                    ></v-select>

                    <div
                        class="py-5 mt-9 text-h5"
                    >
                        Schedule
                    </div>
                    <hr class="mb-9" />
                    <v-text-field
                        v-model="noOfDays"
                        label="No of Days"
                        :rules="inputRules"
                        outlined
                        required
                        type="number"
                        @change="populateDayField"
                        min="1" 
                    >
                    </v-text-field>
                    <div
                        v-for="i in parseInt(noOfDays)"
                        :key="i"
                    >
                        <v-text-field
                            v-model="noOfSession"
                            label="No of Sessions in the day"
                            :rules="inputRules"
                            outlined
                            required
                            type="number"
                            @change="populateSession"
                            min="1" 
                        >
                        </v-text-field>
                        <div>
                            <div
                                v-for="i in parseInt(noOfSession)"
                                :key="i"
                            >
                                <v-text-field
                                    label="Session Title"
                                    :rules="inputRules"
                                    outlined
                                    required
                                >
                                </v-text-field>
                                <v-textarea
                                    label="Session Description"
                                    :rules="inputRules"
                                    outlined
                                    required
                                >
                                </v-textarea>
                                <v-select
                                    :items="speakers"
                                    item-text="name"
                                    item-value="id"
                                    chips
                                    label="Speakers"
                                    multiple
                                    outlined
                                    required
                                ></v-select>
                            </div>
                        </div>
                    </div>

                    <div
                        class="py-5 mt-9 text-h5"
                    >
                        Ticket Price
                    </div>
                    <hr class="mb-9" />
                    <v-radio-group
                        v-model="pricing"
                        @change="populatePricing"
                        row
                    >
                        <v-radio
                            label="Free"
                            value="free"
                        ></v-radio>
                        <v-radio
                            label="Tickets"
                            value="ticketPricing"
                        ></v-radio>
                    </v-radio-group>
                    <div v-show="pricing == 'ticketPricing'">
                        <v-text-field
                            v-model="noOfTicketType"
                            label="No of Ticket Types"
                            :rules="inputRules"
                            outlined
                            required
                            type="number"
                            @change="populateTicketType"
                            min="1" 
                        >
                        </v-text-field>
                        <div 
                            v-for="i in parseInt(noOfTicketType)"
                            :key="i"
                        >
                            <v-text-field
                                label="Ticket Title"
                                :rules="inputRules"
                                outlined
                                required
                            >
                            </v-text-field>
                            <client-only>
                                <vue-editor 
                                    placeholder="Ticket Description..." 
                                    class="mb-5"
                                ></vue-editor>
                            </client-only>
                            <v-text-field
                                label="No of Tickets"
                                :rules="inputRules"
                                outlined
                                required
                            >
                            </v-text-field>
                            <v-text-field
                                label="Ticket Price"
                                :rules="inputRules"
                                outlined
                                required
                            >
                            </v-text-field>
                        </div>
                    </div>
                    
                    
                    <div
                        class="py-5 mt-9 text-h5"
                    >
                        Sponsor
                    </div>
                    <hr class="mb-9" />
                    <v-text-field
                        v-model="noOfSponsors"
                        label="No of Sponsors"
                        :rules="inputRules"
                        outlined
                        required
                        type="number"
                        @change="populateSponsorField"
                        min="0" 
                    >
                    </v-text-field>
                    <div v-if="noOfSponsors > 0" >
                        <div
                            
                            v-for="i in parseInt(noOfSponsors)"
                            :key="i"
                        >
                            <v-text-field
                                label="Sponsor Title"
                                :rules="inputRules"
                                outlined
                                required
                            >
                            </v-text-field>
                            <v-text-field
                                label="Sponsor Link"
                                :rules="inputRules"
                                outlined
                                required
                            >
                            </v-text-field>
                            <v-text-field
                                label="Sponsor Logo Link"
                                :rules="inputRules"
                                outlined
                                required
                            >
                            </v-text-field>
                        </div>
                    </div>


                    <v-btn
                        :disabled="!valid"
                        class="btn-style mr-4"
                        large
                        @click="addEvent"
                        elevation="0"
                    >
                        Add Event
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
            </v-card>        
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
    // let DatetimePicker;
    // if (process.browser) {
    //     DatetimePicker = require('vuetify-datetime-picker').DatetimePicker
    // }
    export default {
        name: 'AddNewEvent',
        data: ()=>({
            valid: true,
            date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
            menu: false,

            title: '',
            shortDescription: '',
            startDatetime: '',
            endDatetime: '', 
            category: null,
            status: null,
            location: null, 
            venue: null,
            description: '', 
            tag: null,
            bannerImage: null, 
            address: '',
            phone: '',
            email: '',
            webLink: '',
            fbLink: '',
            instaLink: '',
            twitterLink: '',
            youtubeLink: '',
            noOfDays: 1, 
            noOfSession: 1,
            noOfSponsors: '',
            pricing: null, 
            noOfTicketType: 1,
            inputRules: [
                v => !!v || 'This Field is Required',
            ],
            emailRules: [
                v => !!v || 'E-mail is required',
                v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
            ],
            categories: [
                {
                    id: 1,
                    cat: 'CEO',
                },
                {
                    id: 2,
                    cat: 'Founder',
                },
                {
                    id: 3,
                    cat: 'Model',
                },
                {
                    id: 4,
                    cat: 'Motivational Speaker',
                },
                {
                    id: 5,
                    cat: 'Designer',
                },
            ],
            locations:[
                {
                    id: 1,
                    location: 'Romania',
                },
                {
                    id: 2,
                    location: 'Paris',
                },
                {
                    id: 3,
                    location: 'USA',
                },
                {
                    id: 4,
                    location: 'Istambul',
                },
                {
                    id: 5,
                    location: 'Dhaka',
                },
                {
                    id: 6,
                    location: 'Malaysia',
                },
            ],
            statuses:[
                {
                    id: 1,
                    stat: 'Upcomming',
                },
                {
                    id: 2,
                    stat: 'Showing',
                },
                {
                    id: 3,
                    stat: 'Expired',
                },
            ],
            venues: [
                {
                    id: 1,
                    venue: 'Tokyo Meeting Center',
                },
                {
                    id: 2,
                    venue: 'London Arena',
                },
                {
                    id: 3,
                    venue: 'Istanbul Event Arena',
                },
                {
                    id: 4,
                    venue: 'Best Event Ticket Deals',
                },
                {
                    id: 5,
                    venue: 'Love Wedding Hall',
                },
                {
                    id: 6,
                    venue: 'Oxnard Beach',
                }
            ],
            tags:[
                {
                    id: 1,
                    tag: 'Business',
                },
                {
                    id: 2,
                    tag: 'Conferrence',
                },
                {
                    id: 3,
                    tag: 'Speakers',
                },
                {
                    id: 4,
                    tag: 'Event',
                },
                {
                    id: 5,
                    tag: 'Storyteller',
                },
                {
                    id: 6,
                    tag: 'Food',
                },
                {
                    id: 7,
                    tag: 'Meeting',
                }
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
            speakers: [
                {
                    id: 1, 
                    name: 'Speaker 1', 
                    email: 'speaker1@gmail.com', 
                    phone: '01234567891',
                    category: 'CEO',
                    location: 'Istambul'
                },
                {
                    id: 2, 
                    name: 'Speaker 2', 
                    email: 'speaker2@gmail.com', 
                    phone: '01234567892',
                    category: 'Designer',
                    location: 'France'
                },
                {
                    id: 3, 
                    name: 'Speaker 3', 
                    email: 'speaker3@gmail.com', 
                    phone: '01234567893',
                    category: 'Founder',
                    location: 'USA'
                },
                {
                    id: 4, 
                    name: 'Speaker 4', 
                    email: 'speaker4@gmail.com', 
                    phone: '01234567894',
                    category: 'CEO',
                    location: 'Istambul'
                },
                {
                    id: 5, 
                    name: 'Speaker 5', 
                    email: 'speaker5@gmail.com', 
                    phone: '01234567895',
                    category: 'Designer',
                    location: 'England'
                },
                {
                    id: 6, 
                    name: 'Speaker 6', 
                    email: 'speaker6@gmail.com', 
                    phone: '01234567896',
                    category: 'Model',
                    location: 'Paris'
                },
                {
                    id: 7, 
                    name: 'Speaker 7', 
                    email: 'speaker7@gmail.com', 
                    phone: '01234567897',
                    category: 'Model',
                    location: 'USA'
                },
                {
                    id: 8, 
                    name: 'Speaker 8', 
                    email: 'speaker8@gmail.com', 
                    phone: '01234567892',
                    category: 'Motivational Speaker',
                    location: 'USA' 
                },
                {
                    id: 9, 
                    name: 'Speaker 9', 
                    email: 'speaker9@gmail.com', 
                    phone: '01234567899',
                    category: 'CEO',
                    location: 'USA' 
                },
                {
                    id: 10, 
                    name: 'Speaker 10', 
                    email: 'speaker10@gmail.com', 
                    phone: '01234567890',
                    category: 'Model',
                    location: 'Australia' 
                },
            ],
            
            snackbar: false,
            snackbarText: '' , 
        }),
        methods: {
            async addEvent() {
                if(this.$refs.form.validate()){
                    this.snackbarText= 'Event Added Successfully';
                    this.snackbar= true; 
                    this.$refs.form.reset(); 
                }
            },
            async reset () {
                this.$refs.form.reset();
                this.$nuxt.$router.push({path:'/Dashboard/Events/All-Events'})

            },
            async populateDayField(){
                this.noOfDays = this.noOfDays; 
                // console.log(this.noOfDays)
            },
            async populateSession(){
                this.noOfSession = this.noOfSession; 
                // console.log(this.noOfSession)
            },
            async populateSponsorField(){
                this.noOfSponsors = this.noOfSponsors; 
                // console.log(this.noOfSession)
            },
            async populatePricing(){
                console.log(this.pricing)
            },
            async populateTicketType(){
                this.noOfTicketType = this.noOfTicketType;
            }
        },
    }
</script>