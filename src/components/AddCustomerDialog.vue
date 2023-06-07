<template>
    <v-row justify="center">
        <v-dialog fullscreen v-model="dialog" persistent>
            <template v-slot:activator="{ props }">
                <v-btn color="primary" v-bind="props">
                    Add customer
                </v-btn>
            </template>
            <v-card>
                <v-card-title>
                    <span class="text-h5">Customer</span>
                </v-card-title>
                <v-card-text>
                    <v-container>
                        <v-row>
                            <v-col cols="12" sm="6" md="4">
                                <v-text-field label="Name*" v-model="name" required></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="6" md="4">
                                <v-text-field label="Email*" v-model="email" required></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="6" md="4">
                                <v-text-field label="Vat*" v-model="vat" required></v-text-field>
                            </v-col>
                        </v-row>
                    </v-container>
                    <small>*indicates required field</small>
                </v-card-text>
                <v-card-title>
                    <span class="text-h5">Site</span>
                </v-card-title>
                <v-card-text>
                    <v-container>
                        <v-row v-for="(site, index) in sites" :key="index">
                            <v-col cols="12" sm="6" md="4">
                                <v-text-field v-model="site.name" label="Name*" required></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="6" md="4">
                                <v-text-field v-model="site.coordinatesLat" label="Coordinates (lat)*"
                                    required></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="6" md="4">
                                <v-text-field v-model="site.coordinatesLon" label="Coordinates (lon)*"
                                    required></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="6" md="4">
                                <v-text-field v-model="site.address" label="Address*" required></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="6" md="4">
                                <v-text-field v-model="site.postCode" label="Post code*" required></v-text-field>
                            </v-col>
                        </v-row>
                    </v-container>
                    <small>*indicates required field</small>
                </v-card-text>
                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="blue-darken-1" variant="text" @click="dialog = false">
                        Close
                    </v-btn>
                    <v-btn color="blue-darken-1" variant="text" @click="addItem()">
                        Save
                    </v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </v-row>
</template>
<script>
import axios from 'axios';
import { useStore } from 'vuex';

export default {
    data: () => ({
        dialog: false,
        name: '',
        email: '',
        vat: '',
        sites: [{
            name: '',
            coordinatesLat: '',
            coordinatesLon: '',
            address: '',
            postCode: ''
        }]
    }),

    methods: {
        addItem() {
            const customer = {
                name: this.name,
                email: this.email,
                vat: this.vat,
            };

            const sites = this.sites.map((site) => ({
                name: site.name,
                coordinates: { latitude: site.coordinatesLat, longitude: site.coordinatesLon },
                address: site.address,
                postCode: site.postCode
            }));

            const payload = {
                customer,
                sites,
            };

            axios
                .post('http://localhost:3333/api/v1/customers', payload)
                .then((response) => {
                    console.log('Customer created successfully');
                    console.log(response.data);
                })
                .catch((error) => {
                    console.error('Error creating customer');
                    console.error(error);
                });

            this.dialog = false;
        },

        openDialog(customerData) {
            this.name = customerData.name;
            this.email = customerData.email;
            this.vat = customerData.vat;
            this.dialog = true;
        }
    },
}


</script>