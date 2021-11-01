<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Event Detail <span v-show="statusId == '2' ">(Pending)</span>
        </div>
        <v-card
            elevation="3"
        >
            <v-card-title>
                <v-spacer></v-spacer>
                <div
                    v-show="viewMode"
                >
                    <v-btn
                        class="ml-3"
                        color="primary"
                        v-show="statusId == '1' "
                        @click="viewMode = false"
                    >
                        Edit
                    </v-btn>
                    
                    <div v-show ="statusId == 2">
                        <v-dialog
                            v-model="dialog"
                            persistent
                            max-width="320"
                        >
                            <template v-slot:activator="{ on, attrs }">
                                <v-btn
                                    color="primary"
                                    dark
                                    v-bind="attrs"
                                    v-on="on"
                                >
                                    Approve Event
                                </v-btn>
                            </template>
                            <v-card class="pa-7">
                                <v-card-title class="text-h6 mb-5 ">
                                    Are You Sure You Want to Approve This Event?
                                </v-card-title>
                                <v-card-actions>
                                    <v-spacer></v-spacer>
                                    <v-btn
                                        color="btn-style"
                                        @click="dialog = false,approveEvent(),statusId = 1"
                                        elevation="0"
                                    >
                                        Approve
                                    </v-btn>
                                    <v-btn
                                        color="error darken-1"
                                        text
                                        @click="dialog = false"
                                        elevation="0"
                                    >
                                        Cancel
                                    </v-btn>
                                
                                </v-card-actions>
                            </v-card>
                        </v-dialog>
                    </div>
                </div>
                
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
                <v-card
                    elevation="0"
                >
                    <v-row
                    >
                        <v-col
                            col="12"
                            md="12"
                            sm="12"
                            xs="12"
                        >
                            <v-card-title class="text-h4 font-weight-medium pt-0 pb-4">{{viewTitle}}</v-card-title>
                            <v-card-subtitle class="py-1 subtitle-1">
                                {{viewShortDescription}}
                            </v-card-subtitle>
                            <v-card-subtitle class="py-1 subtitle-1">Category: {{viewCategory}}</v-card-subtitle>
                            <v-card-subtitle class="py-1 subtitle-1">Event Status: {{viewEventStatus}}</v-card-subtitle>
                            <v-card-subtitle class="py-1 subtitle-1">Location: {{viewLocation}}</v-card-subtitle>
                            <v-card-subtitle class="py-1 subtitle-1">Venue: {{viewVenue}}</v-card-subtitle>
                            <v-card-subtitle class="py-1 subtitle-1">Address: {{viewAddress}}</v-card-subtitle>
                            <v-card-subtitle class="py-1 subtitle-1">Start Date: {{viewStartDateTime}}</v-card-subtitle>
                            <v-card-subtitle class="py-1 subtitle-1">End Date: {{viewEndDateTime}}</v-card-subtitle> 

                            <v-card-subtitle class="py-1 mt-4 subtitle-1">Phone: {{viewPhone}}</v-card-subtitle>   
                            <v-card-subtitle class="py-1 subtitle-1">Email: {{viewEmail}}</v-card-subtitle> 
                            <v-card-subtitle class="py-1 subtitle-1">Website: {{viewWebsiteLink}}</v-card-subtitle>
                            <v-card-subtitle class="py-1 subtitle-1">Facebook: {{viewFacebookLink}}</v-card-subtitle>
                            <v-card-subtitle class="py-1 subtitle-1">Twitter: {{viewTwitterLink}}</v-card-subtitle>
                            <v-card-subtitle class="py-1 subtitle-1">Instagram: {{viewInstagramLink}}</v-card-subtitle>
                            <v-card-subtitle class="py-1 subtitle-1">YouTube: {{viewYoutubeLink}}</v-card-subtitle> 
                        </v-col>
                    </v-row>

                    <v-row
                        class="mb-5 mt-5"
                    >
                        <v-col
                            col="12"
                            md="12"
                            sm="12"
                            xs="12"
                            style="border-bottom: 1px solid #eaeaea"
                            class="text-h5"
                        >
                            Description
                        </v-col>
                        <v-col
                            col="12"
                            xs="12"
                        >
                            <v-img
                                :src="viewBannerImage"
                                max-height="800px"
                                class="mb-5"
                            ></v-img>
                            <div v-html="viewDescription"></div>
                        </v-col>
                    </v-row>

                    <v-row
                        class="mb-5"
                    >
                        <v-col
                            col="12"
                            md="12"
                            sm="12"
                            xs="12"
                            style="border-bottom: 1px solid #eaeaea"
                            class="text-h5 d-flex align-center flex-wrap"
                        >
                            <span>Speakers</span>
                        </v-col>
                        <v-col
                            col="12"
                            md="6"
                            sm="12"
                            xs="12"
                            v-for="speaker in viewSpeakers"
                            :key="speaker.id"
                        >
                            <v-row
                                class="d-flex flex-wrap"
                            >
                                <v-col
                                    col="12"
                                    md="3"
                                    sm="4"
                                    xs="12"
                                >
                                    <v-img
                                        :src="speaker.url"
                                    ></v-img>
                                </v-col>
                                <v-col
                                    col="12"
                                    md="9"
                                    sm="8"
                                    xs="12"
                                >
                                    <div class="text-h5 pl-4 pt-0">{{speaker.name}}</div>
                                    <div class="pt-1 pl-4 pb-3 subtitle-1">
                                        {{speaker.category}}
                                    </div>
                                    <div class="text-p pl-4 black--text">
                                        <div class="pb-2">
                                            Phone: {{speaker.phone}}
                                        </div>
                                        <div class="pb-2">
                                            Email: {{speaker.email}}
                                        </div>
                                        <div class="pb-2">
                                            Location: {{speaker.location}}
                                        </div>
                                    </div>
                                </v-col>
                            </v-row>
                        </v-col>
                    </v-row>

                    <v-row
                        class="mb-5"
                    >
                        <v-col
                            col="12"
                            md="12"
                            sm="12"
                            xs="12"
                            style="border-bottom: 1px solid #eaeaea"
                            class="text-h5 d-flex align-center flex-wrap"
                        >
                            <span>Event Schedule</span>
                        </v-col>
                        <v-col
                            col="12"
                            md="12"
                            sm="12"
                            xs="12"
                            v-for="schedule in viewSchedule"
                            :key="schedule.id"
                            class="my-4"
                        >
                            <v-row
                            >
                                <v-col
                                    col="12"
                                    md="12"
                                    sm="12"
                                    xs="12"
                                >
                                    <div class="text-h5 pl-4 pt-0">{{schedule.title}}</div>
                                    <div class="pt-1 pl-4 pb-3 subtitle-1">
                                        {{schedule.date}}
                                    </div>
                                    <div class="text-p pl-8 my-3 black--text"
                                        v-for="session in schedule.sessions"
                                        :key="session.id"
                                    >
                                        <div class="pb-2">
                                            Title: {{session.title}}
                                        </div>
                                        <div class="pb-2">
                                            Description: {{session.description}}
                                        </div>
                                        <div class="pb-2">
                                            Time: {{session.time}}
                                        </div>
                                        <div 
                                            v-show="session.speakers.length"
                                            class="ml-3"
                                        >
                                            <span class="black--text my-3 pb-3 font-weight-medium">Speakers: </span>
                                            <div
                                                v-for="speaker in session.speakers"
                                                :key="speaker.id"
                                                class="ml-4"
                                            >
                                                <div class="pb-1">
                                                    Name: {{speaker.name}}
                                                </div>
                                                <div class="pb-2">
                                                    Category: {{speaker.category}}
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </v-col>
                            </v-row>
                        </v-col>
                    </v-row>
                    
                    <v-row
                        class="mb-5"
                    >
                        <v-col
                            col="12"
                            md="12"
                            sm="12"
                            xs="12"
                            style="border-bottom: 1px solid #eaeaea"
                            class="text-h5 "
                        >
                            Organizers
                        </v-col>
                        <v-col
                            col="12"
                            xs="12"
                        >
                            <v-row>
                                <v-col
                                    col="12"
                                    md="12"
                                    sm="12"
                                    xs="12"
                                    class="d-flex align-center flex-wrap"
                                >
                                    <div
                                        v-for="organizer in viewOrganizers"
                                        :key="organizer.id"
                                        
                                    >
                                        <v-btn
                                            elevation="2"
                                            color="grey darken-1"
                                            class="white--text mr-3 my-2"
                                            style="cursor: default"
                                        >
                                            {{organizer.org}}
                                        </v-btn>
                                    </div>
                                </v-col>
                            </v-row>
                        </v-col>
                    </v-row>
                    
                    <v-row
                        class="mb-5"
                    >
                        <v-col
                            col="12"
                            md="12"
                            sm="12"
                            xs="12"
                            style="border-bottom: 1px solid #eaeaea"
                            class="text-h5 "
                        >
                            Tags
                        </v-col>
                        <v-col
                            col="12"
                            xs="12"
                        >
                            <v-row>
                                <v-col
                                    col="12"
                                    md="12"
                                    sm="12"
                                    xs="12"
                                    class="d-flex align-center flex-wrap"
                                >
                                    <div
                                        v-for="tag in viewTags"
                                        :key="tag.id"
                                        
                                    >
                                        <v-btn
                                            elevation="2"
                                            color="grey darken-1"
                                            class="white--text mr-3 my-2"
                                            style="cursor: default"
                                        >
                                            {{tag.tag}}
                                        </v-btn>
                                    </div>
                                </v-col>
                            </v-row>
                        </v-col>
                    </v-row>

                    <v-row
                        class="mb-5"
                    >
                        <v-col
                            col="12"
                            md="12"
                            sm="12"
                            xs="12"
                            style="border-bottom: 1px solid #eaeaea"
                            class="text-h5 mb-5"
                        >
                            Photos
                        </v-col>
                        <v-col
                            col="12"
                            xs="12"
                        >
                            <v-row>
                                <v-col
                                    col="12"
                                    md="4"
                                    sm="6"
                                    xs="12"
                                    class="pa-0"
                                    v-for="viewPhoto in viewPhotos"
                                    :key="viewPhoto.id"
                                >
                                    <v-img
                                        :src="viewPhoto.url"
                                    ></v-img>
                                </v-col>
                            </v-row>
                        </v-col>
                    </v-row>

                    <v-row
                        class="mb-5"
                    >
                        <v-col
                            col="12"
                            md="12"
                            sm="12"
                            xs="12"
                            style="border-bottom: 1px solid #eaeaea"
                            class="text-h5 mb-5"
                        >
                            Sponsors
                        </v-col>
                        <v-col
                            col="12"
                            xs="12"
                        >
                            <v-row>
                                <v-col
                                    col="12"
                                    md="3"
                                    sm="4"
                                    xs="12"
                                    class="pa-0"
                                    v-for="sponsor in viewSponsors"
                                    :key="sponsor.id"
                                >
                                    <v-img
                                        :src="sponsor.img"
                                    ></v-img>
                                </v-col>
                            </v-row>
                        </v-col>
                    </v-row>

                    
                </v-card>
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
                        label="Event Id"
                        outlined
                        required
                        readonly
                    ></v-text-field>

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
                        outlined
                        required
                    ></v-textarea>

                    <v-select
                        v-model="eventStatus"
                        :items="alleventstatus"
                        item-value="id"
                        item-text="eventStatus"
                        :rules="inputRules"
                        label="Event Status"
                        outlined
                        required
                    ></v-select>

                    <v-select
                        v-model="category"
                        :items="allcategories"
                        item-value="catId"
                        item-text="category"
                        :rules="inputRules"
                        label="Category"
                        outlined
                        required
                    ></v-select>

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
                            class="mb-4"
                        ></v-datetime-picker>
                    </client-only>

                    <v-select
                        v-model="location"
                        :items="alllocations"
                        item-value="id"
                        item-text="location"
                        :rules="inputRules"
                        label="Location"
                        outlined
                        required
                    ></v-select>

                    <v-select
                        v-model="venue"
                        :items="allvenues"
                        item-value="id"
                        item-text="venue"
                        :rules="inputRules"
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
                        v-model="websiteLink"
                        label="Website Link"
                        outlined
                    ></v-text-field>

                    <v-text-field
                        v-model="facebookLink"
                        label="Facebook Link"
                        outlined
                    ></v-text-field>

                    <v-text-field
                        v-model="instagramLink"
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
                        v-model="tags"
                        :items="alltags"
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
                        :items="allorganizers"
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
                        v-model="speakers"
                        :items="allspeakers"
                        item-text="name"
                        item-value="id"
                        chips
                        label="Speakers"
                        multiple
                        outlined
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
                        @click="UpdateEventInfo"
                        elevation="0"
                    >
                        Update Event Info
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

    let VueEditor;
    if (process.browser) {
        VueEditor = require('vue2-editor').VueEditor
    }

    export default {
        name: 'EventDetail', 
        data:()=>({
            viewMode: true,
            events:[
                {
                    id: '1',
                    title: 'Wedding of James & Helen',
                    shortDescription: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has. Sed ad dicam platonem, mea eros illum elitr id, ei has similique constituto. ',
                    description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has. Sed ad dicam platonem, mea eros illum elitr id, ei has similique constituto. Ea movet saperet rationibus sit, pri autem aliquip invidunt an. Consetetur omittantur consequuntur eos et. <strong> Eleifend praesent iudicabit no mea, tollit persequeris ex pri, tota splendide voluptaria in pri.</strong> Ad per tale aliquip, ei sit viris commune albucius. Eos aliquip scaevola ut, eum alii mentitum prodesset no, his ne suas atomorum. Et numquam deleniti ponderum vis, quod error at mei. Novum blandit adolescens sea te. Ea eum cetero scaevola.<br /><br />In his meis porro viris, illud imperdiet reprimique et vim. Feugiat atomorum reprehendunt vix ei, ei facete regione pri. Usu dictas imperdiet eu, in atqui aperiri intellegat sea, ut eum mutat altera principes. Te sit quaeque oportere, has modus inani ceteros ad. Impedit blandit deseruisse duo ea, ne graecis deleniti incorrupte usu. Ut mei splendide accommodare. An pri iisque meliore, eam ei splendide eloquentiam philosophia. <u>Ne per meis eleifend electram.</u> Ne eam porro aliquam invidunt. Minim docendi eloquentiam cum ad. Quo ea mazim ubique, ex est fuisset blandit scaevola. Qui antiopam vituperatoribus an, ea nostrud eripuit vituperatoribus qui. In eam diam nominati, per ea alia luptatum. <span class="yellowish--text">Nam habemus electram democritum ut.</span> Mei ea omnium admodum intellegat. Habeo atqui molestiae at mei, an nec ridens consequuntur. Quem nulla cum ei, his ipsum apeirian no, per at eius iriure aperiri. Sed dicam interesset ei. Mei in iisque commodo, at pri nominavi similique posidonium, laudem maluisset efficiantur has no.<br/><br /><br />His verterem consectetuer consequuntur ne, no virtute atomorum usu. <b> Eu quo nemore causae tacimates, eos viderer persequeris an.</b> Cu molestie consulatu qui. Natum labores perfecto no ius, pri dico mundi inciderint id. Ei usu dico libris postea. Cu graeco doctus splendide qui, ei eum probo regione.', 

                    statusId: 2, 
                    status: 'Pending',
                    catId: 9,
                    category: 'Beach',
                    locId: 2,
                    location: 'Callifornia', 
                    address: 'Harbiye Mahallesi, Darülbedai Caddesi No:3, 34367 Şişli/Aunstralia',
                    venueId: 6, 
                    venue: 'Oxnard Beach', 
                    startDateTime: 'November 23, 2021', 
                    endDateTime: 'November 29, 2021', 
                    eventStatusId: 1, 
                    eventStatus: 'Upcomming', 
                    cost: '259', 
                                      
                    phone: '0674 987 665',
                    email: 'event@gloriathemes.com', 
                    websiteLink: 'www.website.com',
                    facebookLink: 'http://www.facebook.com',
                    instagramLink: 'http://www.instagram.com', 
                    youtubeLink: 'http://www.youtube.com', 
                    twitterLink: 'http://www.facebook.com', 
                    whishCount: 7, 

                    url: require('../assets/Images/LatestPost/LatestPost1.png'),
                    photos: [
                        {
                            id: 1, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        },
                        {
                            id: 2, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        },
                        {
                            id: 3, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        },
                        {
                            id: 4, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        },
                        {
                            id: 5, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        },
                        {
                            id: 6, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        },
                        {
                            id: 7, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        },
                        {
                            id: 8, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        },
                        {
                            id: 9, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        }
                    ],
                    sponsors: [
                        {
                            id: 1,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                        {
                            id: 2,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                        {
                            id: 3,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                        {
                            id: 4,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                        {
                            id: 5,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                        {
                            id: 6,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                    ],
                    tags:[
                        {
                            id: 1, 
                            tag: 'Speaker', 
                        },
                        {
                            id: 2, 
                            tag: 'Conferrence', 
                        },
                        {
                            id: 3, 
                            tag: 'Meeting', 
                        },
                        {
                            id: 4, 
                            tag: 'Culture', 
                        },
                        {
                            id: 5, 
                            tag: 'Art', 
                        },
                        {
                            id: 6, 
                            tag: 'Event', 
                        }
                    ],
                    speakers: [
                        {
                            id: 1, 
                            name: 'Speaker 1', 
                            email: 'speaker1@gmail.com', 
                            phone: '01234567891',
                            category: 'CEO',
                            location: 'Istambul',
                            url: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-4-350x350.jpg',
                        },
                        {
                            id: 2, 
                            name: 'Speaker 2', 
                            email: 'speaker2@gmail.com', 
                            phone: '01234567892',
                            category: 'Designer',
                            location: 'France',
                            url: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-4-350x350.jpg',
                        },
                        {
                            id: 3, 
                            name: 'Speaker 3', 
                            email: 'speaker3@gmail.com', 
                            phone: '01234567893',
                            category: 'Founder',
                            location: 'USA',
                            url: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-4-350x350.jpg',
                        },
                        {
                            id: 4, 
                            name: 'Speaker 4', 
                            email: 'speaker4@gmail.com', 
                            phone: '01234567894',
                            category: 'CEO',
                            location: 'Istambul',
                            url: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-4-350x350.jpg',
                        },
                        {
                            id: 5, 
                            name: 'Speaker 5', 
                            email: 'speaker5@gmail.com', 
                            phone: '01234567895',
                            category: 'Designer',
                            location: 'England',
                            url: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-4-350x350.jpg',
                        },
                        {
                            id: 6, 
                            name: 'Speaker 6', 
                            email: 'speaker6@gmail.com', 
                            phone: '01234567896',
                            category: 'Model',
                            location: 'Paris',
                            url: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-4-350x350.jpg',
                        },
                    ],
                    organizers: [
                        {
                            id: 1,
                            org: 'BCC',
                        },
                        {
                            id: 2,
                            org: 'ICT Ministry', 
                        }
                    ], 
                    sponsors: [
                        {
                            id: 1,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                        {
                            id: 2,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                        {
                            id: 3,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                        {
                            id: 4,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                        {
                            id: 5,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                        {
                            id: 6,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                    ],
                    schedule:[
                        {
                            id: 1,
                            title: 'Day 1',
                            date: 'November 17 2021',
                            sessions: [
                                {
                                    id: 1, 
                                    time: '10:30',
                                    title: 'Nunc non ligula eu massa venenatis',
                                    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse non posuere dolor, ut fermentum enim. Nullam quis molestie purus. Nam leo turpis, scelerisque in convallis ac, accumsan a lacus. Sed laoreet arcu in odio auctor commodo qisque et mi lacinia.',
                                    speakers: [
                                        {
                                            id: 2, 
                                            name: 'Speaker 2', 
                                            category: 'Designer',
                                        },
                                        {
                                            id: 3, 
                                            name: 'Speaker 3', 
                                            category: 'Model',
                                        },
                                    ],                                    

                                },
                                {
                                    id: 2, 
                                    time: '12:30',
                                    title: 'Nunc non ligula eu massa venenatis',
                                    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse non posuere dolor, ut fermentum enim. Nullam quis molestie purus. Nam leo turpis, scelerisque in convallis ac, accumsan a lacus. Sed laoreet arcu in odio auctor commodo qisque et mi lacinia.',
                                    speakers: [
                                        {
                                            id: 2, 
                                            name: 'Speaker 2', 
                                            category: 'Designer',
                                        },
                                        {
                                            id: 3, 
                                            name: 'Speaker 3', 
                                            category: 'Model',
                                        },
                                    ],                                    

                                },
                                {
                                    id: 3, 
                                    time: '13:30',
                                    title: 'Nunc non ligula eu massa venenatis',
                                    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse non posuere dolor, ut fermentum enim. Nullam quis molestie purus. Nam leo turpis, scelerisque in convallis ac, accumsan a lacus. Sed laoreet arcu in odio auctor commodo qisque et mi lacinia.',
                                    speakers: [
                                        {
                                            id: 2, 
                                            name: 'Speaker 2', 
                                            category: 'Designer',
                                        },
                                        {
                                            id: 3, 
                                            name: 'Speaker 3', 
                                            category: 'Model',
                                        },
                                    ],  
                                },
                                {
                                    id: 4, 
                                    time: '14:00',
                                    title: 'Nunc non ligula eu massa venenatis',
                                    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse non posuere dolor, ut fermentum enim. Nullam quis molestie purus. Nam leo turpis, scelerisque in convallis ac, accumsan a lacus. Sed laoreet arcu in odio auctor commodo qisque et mi lacinia.',
                                    speakers: [
                                        {
                                            id: 2, 
                                            name: 'Speaker 2', 
                                            category: 'Designer',
                                        },
                                    ],                                    

                                }
                            ],
                        },
                        {
                            id: 2,
                            title: 'Day 2',
                            date: 'November 18 2021',
                            sessions: [
                                {
                                    id: 1, 
                                    time: '10:30',
                                    title: 'Nunc non ligula eu massa venenatis',
                                    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse non posuere dolor, ut fermentum enim. Nullam quis molestie purus. Nam leo turpis, scelerisque in convallis ac, accumsan a lacus. Sed laoreet arcu in odio auctor commodo qisque et mi lacinia.',
                                    speakers: [
                                        {
                                            id: 2, 
                                            name: 'Speaker 2', 
                                            category: 'Designer',
                                        },
                                        {
                                            id: 3, 
                                            name: 'Speaker 3', 
                                            category: 'Model',
                                        },
                                    ],                                    

                                },
                                {
                                    id: 2, 
                                    time: '12:30',
                                    title: 'Nunc non ligula eu massa venenatis',
                                    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse non posuere dolor, ut fermentum enim. Nullam quis molestie purus. Nam leo turpis, scelerisque in convallis ac, accumsan a lacus. Sed laoreet arcu in odio auctor commodo qisque et mi lacinia.',
                                    speakers: [
                                        {
                                            id: 2, 
                                            name: 'Speaker 2', 
                                            category: 'Designer',
                                        },
                                        {
                                            id: 3, 
                                            name: 'Speaker 3', 
                                            category: 'Model',
                                        },
                                    ],                                    

                                },
                                {
                                    id: 3, 
                                    time: '13:30',
                                    title: 'Nunc non ligula eu massa venenatis',
                                    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse non posuere dolor, ut fermentum enim. Nullam quis molestie purus. Nam leo turpis, scelerisque in convallis ac, accumsan a lacus. Sed laoreet arcu in odio auctor commodo qisque et mi lacinia.',
                                    speakers: [
                                        {
                                            id: 2, 
                                            name: 'Speaker 2', 
                                            category: 'Designer',
                                        },
                                        {
                                            id: 3, 
                                            name: 'Speaker 3', 
                                            category: 'Model',
                                        },
                                    ],  
                                },
                                {
                                    id: 4, 
                                    time: '14:00',
                                    title: 'Nunc non ligula eu massa venenatis',
                                    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse non posuere dolor, ut fermentum enim. Nullam quis molestie purus. Nam leo turpis, scelerisque in convallis ac, accumsan a lacus. Sed laoreet arcu in odio auctor commodo qisque et mi lacinia.',
                                    speakers: [
                                        {
                                            id: 2, 
                                            name: 'Speaker 2', 
                                            category: 'Designer',
                                        },
                                    ],                                    

                                }
                            ],
                        },
                        {
                            id: 3,
                            title: 'Day 3',
                            date: 'November 19 2021',
                            sessions: [
                                {
                                    id: 1, 
                                    time: '10:30',
                                    title: 'Nunc non ligula eu massa venenatis',
                                    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse non posuere dolor, ut fermentum enim. Nullam quis molestie purus. Nam leo turpis, scelerisque in convallis ac, accumsan a lacus. Sed laoreet arcu in odio auctor commodo qisque et mi lacinia.',
                                    speakers: [
                                        {
                                            id: 2, 
                                            name: 'Speaker 2', 
                                            category: 'Designer',
                                        },
                                        {
                                            id: 3, 
                                            name: 'Speaker 3', 
                                            category: 'Model',
                                        },
                                    ],                                    

                                },
                                {
                                    id: 2, 
                                    time: '12:30',
                                    title: 'Nunc non ligula eu massa venenatis',
                                    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse non posuere dolor, ut fermentum enim. Nullam quis molestie purus. Nam leo turpis, scelerisque in convallis ac, accumsan a lacus. Sed laoreet arcu in odio auctor commodo qisque et mi lacinia.',
                                    speakers: [
                                        {
                                            id: 2, 
                                            name: 'Speaker 2', 
                                            category: 'Designer',
                                        },
                                        {
                                            id: 3, 
                                            name: 'Speaker 3', 
                                            category: 'Model',
                                        },
                                    ],                                    

                                },
                                {
                                    id: 3, 
                                    time: '13:30',
                                    title: 'Nunc non ligula eu massa venenatis',
                                    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse non posuere dolor, ut fermentum enim. Nullam quis molestie purus. Nam leo turpis, scelerisque in convallis ac, accumsan a lacus. Sed laoreet arcu in odio auctor commodo qisque et mi lacinia.',
                                    speakers: [
                                        {
                                            id: 2, 
                                            name: 'Speaker 2', 
                                            category: 'Designer',
                                        },
                                        {
                                            id: 3, 
                                            name: 'Speaker 3', 
                                            category: 'Model',
                                        },
                                    ],  
                                },
                                {
                                    id: 4, 
                                    time: '14:00',
                                    title: 'Nunc non ligula eu massa venenatis',
                                    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse non posuere dolor, ut fermentum enim. Nullam quis molestie purus. Nam leo turpis, scelerisque in convallis ac, accumsan a lacus. Sed laoreet arcu in odio auctor commodo qisque et mi lacinia.',
                                    speakers: [
                                        {
                                            id: 2, 
                                            name: 'Speaker 2', 
                                            category: 'Designer',
                                        },
                                    ],                                    

                                }
                            ],
                        },
                    ],
                }
            ],
            
            alleventstatus:[
                {
                    id: 1, 
                    eventStatus: 'Upcomming',
                },
                {
                    id: 2, 
                    eventStatus: 'Showing',
                },
                {
                    id: 3, 
                    eventStatus: 'Expired',
                }
            ],
            allorganizers: [
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
            allspeakers: [
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

            allcategories: [
                {
                    id: 1,
                    category: 'CEO',
                },
                {
                    id: 2,
                    category: 'Founder',
                },
                {
                    id: 3,
                    category: 'Model',
                },
                {
                    id: 4,
                    category: 'Motivational Speaker',
                },
                {
                    id: 5,
                    category: 'Designer',
                },
            ],
            alllocations:[
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
            allvenues: [
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
            alltags:[
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
            // authors: [
            //     {
            //         id: 1, 
            //         name: 'Author 1', 
            //         description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
            //         facebookLink: 'www.facebook.com',
            //         twitterLink: 'www.twitter.com',
            //         instagramLink: 'www.instagram.com',
            //         youtubeLink: 'www.youtube.com',
            //         count: 1,
            //     },
            //     {
            //         id: 2, 
            //         name: 'Author 2', 
            //         description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
            //         facebookLink: 'www.facebook.com',
            //         twitterLink: 'www.twitter.com',
            //         instagramLink: 'www.instagram.com',
            //         youtubeLink: 'www.youtube.com',
            //         count: 1,
            //     },
            //     {
            //         id: 3, 
            //         name: 'Author 3', 
            //         description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
            //         facebookLink: 'www.facebook.com',
            //         twitterLink: 'www.twitter.com',
            //         instagramLink: 'www.instagram.com',
            //         youtubeLink: 'www.youtube.com',
            //         count: 2,
            //     },
            //     {
            //         id: 4, 
            //         name: 'Author 4', 
            //         description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
            //         facebookLink: 'www.facebook.com',
            //         twitterLink: 'www.twitter.com',
            //         instagramLink: 'www.instagram.com',
            //         youtubeLink: 'www.youtube.com',
            //         count: 1,
            //     },
            //     {
            //         id: 5, 
            //         name: 'Author 5', 
            //         description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
            //         facebookLink: 'www.facebook.com',
            //         twitterLink: 'www.twitter.com',
            //         instagramLink: 'www.instagram.com',
            //         youtubeLink: 'www.youtube.com',
            //         count: 2,
            //     },
            //     {
            //         id: 6, 
            //         name: 'Author 6', 
            //         description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
            //         facebookLink: 'www.facebook.com',
            //         twitterLink: 'www.twitter.com',
            //         instagramLink: 'www.instagram.com',
            //         youtubeLink: 'www.youtube.com',
            //         count: 1,
            //     },
            //     {
            //         id: 7, 
            //         name: 'Author 7', 
            //         description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
            //         facebookLink: 'www.facebook.com',
            //         twitterLink: 'www.twitter.com',
            //         instagramLink: 'www.instagram.com',
            //         youtubeLink: 'www.youtube.com',
            //         count: 4,
            //     },
            //     {
            //         id: 8, 
            //         name: 'Author 8', 
            //         description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
            //         facebookLink: 'www.facebook.com',
            //         twitterLink: 'www.twitter.com',
            //         instagramLink: 'www.instagram.com',
            //         youtubeLink: 'www.youtube.com',
            //         count: 1,
            //     },
            //     {
            //         id: 9, 
            //         name: 'Author 9',
            //         description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
            //         facebookLink: 'www.facebook.com',
            //         twitterLink: 'www.twitter.com',
            //         instagramLink: 'www.instagram.com',
            //         youtubeLink: 'www.youtube.com',
            //         count: 1,
            //     },
            //     {
            //         id: 10, 
            //         name: 'Author 10', 
            //         description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
            //         facebookLink: 'www.facebook.com',
            //         twitterLink: 'www.twitter.com',
            //         instagramLink: 'www.instagram.com',
            //         youtubeLink: 'www.youtube.com',
            //         count: 3,
            //     },
            // ],

            viewTitle: '',
            viewCategory: '',
            viewEventStatus: '',
            viewVenue: '', 
            viewLocation: '',
            viewAddress: '',
            viewDescription: '',
            viewShortDescription: '',
            viewBannerImage: null,
            viewStartDateTime: '' ,
            viewEndDateTime: '',

            viewPhone: '',
            viewEmail: '', 
            viewWebsiteLink: '',
            viewFacebookLink: '',
            viewInstagramLink: '', 
            viewYoutubeLink: '', 
            viewTwitterLink: '', 

            viewTags:[],
            viewPhotos: [],
            viewSponsors: [],
            viewSpeakers: [],
            viewOrganizers: [],
            viewSchedule: [],
            viewPricing: [],


            id: '',
            title: '',
            category: {},
            location: {},
            venue: {},
            address: '',
            organizer: {}, 
            eventStatus: {},
            description: '',
            shortDescription: '',
            startDatetime: '',
            endDatetime: '', 
            bannerImage: null,
            
            phone: '',
            email: '', 
            websiteLink: '',
            facebookLink: '',
            instagramLink: '', 
            youtubeLink: '', 
            twitterLink: '', 
            whishCount: 7, 

            tags: [],
            organizers: [],
            photos: [],
            sponsors: [],
            speakers: [],
            schedule: [],
            // pricing: [],

            noOfDays: 1, 
            noOfSession: 1,
            noOfSponsors: '',
            pricing: null, 
            noOfTicketType: 1,

            date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
            menu: false,
            dialog: false,

            
            statusId: '', 
            snackbar: false,
            snackbarText: '' ,
            valid: true,
            
            inputRules: [
                v => !!v || 'This Field is Required',
            ],
            emailRules: [
                v => !!v || 'E-mail is required',
                v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
            ],
            
        }),
        methods: {
            async UpdateEventInfo(){
                if(this.$refs.form.validate()){
                    this.snackbarText= 'Event Info Updated Successfully';
                    this.snackbar= true; 
                    this.viewMode= true; 
                }
            },
            async reset(){
                this.$nuxt.$router.push({path: '/Dashboard/Events/All-Events'})
            },
            async approveEvent(){
                this.snackbarText= 'Event Approved Successfully';
                this.snackbar= true; 
                this.statusID = '1' ; 
                this.viewMode= true; 
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
        mounted() { 
            this.id = this.events[0].id; 

            this.viewTitle = this.events[0].title;
            this.viewCategory = this.events[0].category;
            this.viewEventStatus = this.events[0].eventStatus;
            this.viewAddress = this.events[0].address;
            this.viewLocation = this.events[0].location;
            this.viewVenue = this.events[0].venue;
            this.viewDescription = this.events[0].description;
            this.viewShortDescription = this.events[0].shortDescription;
            this.viewBannerImage =  this.events[0].url;
            this.viewStartDateTime = this.events[0].startDateTime;
            this.viewEndDateTime = this.events[0].endDateTime;

            this.viewPhone = this.events[0].phone;
            this.viewEmail = this.events[0].email;
            this.viewWebsiteLink = this.events[0].websiteLink;
            this.viewFacebookLink = this.events[0].facebookLink;
            this.viewInstagramLink = this.events[0].instagramLink;
            this.viewYoutubeLink = this.events[0].youtubeLink;
            this.viewTwitterLink = this.events[0].twitterLink;


            this.viewTags = this.events[0].tags;
            this.viewOrganizers= this.events[0].organizers;
            this.viewPhotos = this.events[0].photos;
            this.viewSponsors = this.events[0].sponsors;
            this.viewSpeakers = this.events[0].speakers;
            this.viewSchedule = this.events[0].schedule;
            this.viewPricing = this.events[0].pricing; 

            this.title = this.events[0].title;
            this.category = { id: this.events[0].catId, category: this.events[0].category };
            this.location = { id: this.events[0].locId, location: this.events[0].location };
            this.venue = { id: this.events[0].venueId, venue: this.events[0].venue };
            this.eventStatus = { id: this.events[0].eventStatusId, eventStatus: this.events[0].eventStatus };
            this.description = this.events[0].description;
            this.shortDescription = this.events[0].shortDescription;
            this.address = this.events[0].address;
            this.startDateTime = this.events[0].startDateTime;
            this.endDateTime = this.events[0].endDateTime;

            this.phone = this.events[0].phone;
            this.email = this.events[0].email;
            this.websiteLink= this.events[0].websiteLink;
            this.facebookLink= this.events[0].facebookLink;
            this.twitterLink= this.events[0].twitterLink;
            this.instagramLink= this.events[0].instagramLink;
            this.youtubeLink= this.events[0].youtubeLink;

            this.tags = this.events[0].tags;
            this.organizers= this.events[0].organizers;
            this.photos = this.events[0].photos;
            this.sponsor = this.events[0].sponsors;
            this.speakers = this.events[0].speakers;
            this.schedule = this.events[0].schedule;
            this.pricing = this.events[0].pricing;
            
            // console.log(tags);
            this.statusId = this.events[0].statusId;
        }
    }
</script>