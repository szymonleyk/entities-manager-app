<template>
    <v-row justify="center">
        <v-dialog v-model="dialog" persistent width="1024">
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
                            <!-- <v-col cols="12">
                                <v-text-field label="Email*" required></v-text-field>
                            </v-col>
                            <v-col cols="12">
                                <v-text-field label="Password*" type="password" required></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="6">
                                <v-select :items="['0-17', '18-29', '30-54', '54+']" label="Age*" required></v-select>
                            </v-col>
                            <v-col cols="12" sm="6">
                                <v-autocomplete
                                    :items="['Skiing', 'Ice hockey', 'Soccer', 'Basketball', 'Hockey', 'Reading', 'Writing', 'Coding', 'Basejump']"
                                    label="Interests" multiple></v-autocomplete>
                            </v-col> -->
                        </v-row>
                    </v-container>
                    <small>*indicates required field</small>
                </v-card-text>
                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="blue-darken-1" variant="text" @click="dialog = false">
                        Close
                    </v-btn>
                    <v-btn color="blue-darken-1" variant="text" @click="addItem(item)">
                        Save
                    </v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </v-row>
</template>
<script>
import axios from 'axios';
export default {
    data: () => ({
        dialog: false,
        name: '',
        email: '',
        vat: ''
    }),

    methods: {
        addItem() {
            const item = {
                name: this.name,
                email: this.email,
                vat: this.vat,
            };

            axios.post('http://localhost:3333/api/v1/customers', item)
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
    }
}
</script>