<template>
    <v-row justify="center">
        <v-dialog v-model="showDialog" persistent max-width="600px" s>
            <v-card>
                <v-card-title>
                    <span class="headline">New Bookmark</span>
                </v-card-title>
                <v-card-text>
                    <v-container>
                        <v-row>
                            <v-col cols="12">
                                <v-text-field v-model="name" label="Name" required></v-text-field>
                            </v-col>
                            <v-col cols="12">
                                <v-text-field v-model="url" label="URL" required></v-text-field>
                            </v-col>

                        </v-row>
                    </v-container>
                </v-card-text>
                <v-card-actions>
                    <div class="flex-grow-1"></div>
                    <v-btn color="blue darken-1" text @click="closeDialog">Close</v-btn>
                    <v-btn color="blue darken-1" text @click="saveBookmark">Save</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </v-row>
</template>

<script>
    export default {
        name: 'NewBookmark',
        data() {
            return {
                name: "",
                url: "",
            }
        },
        props: {
            show: Boolean,
        },
        computed: {
            showDialog() {
                return this.$store.getters.showNewBookmarkDialog
            }
        },
        methods: {
            closeDialog() {
                this.$store.dispatch('showNewBookmarkDialog', false)
                    .then(() => {
                    })
                    .catch(err => {
                        console.log(err);
                    })
            },
            saveBookmark() {
                const name = this.name
                const url = this.url

                this.$store.dispatch('saveBookmark', {name, url})
                    .then(() => {
                        this.$toast("Bookmark saved successfully")
                        this.closeDialog()
                        this.$router.push('/').catch(err => {})
                    })
                    .catch(err => {
                        console.log(err);
                        this.$toast("Bookmark save failed")
                    })
            }
        }
    }
</script>

<style scoped>
</style>