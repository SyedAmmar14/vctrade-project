<template>
    <div class="container show-details mt-5">
        <div class="panel-body inf-content">
            <div v-for="(uniquedetail, i) in user" :key="i">
                <div v-for="(unique, i) in uniquedetail.results" :key="i">
                    <div class="row">
                        <div class="col-md-4">
                            <img style="width:600px; border-radius: 50%;" class="img-circle img-thumbnail"
                                :src="unique.picture.medium">
                        </div>
                        <div class="col-md-6 m-auto">
                            <div class="table-responsive">
                                <table class="table table-user-information">
                                    <tbody>
                                        <tr>
                                            <td>
                                                <strong>
                                                    <span class="text-primary"></span>
                                                    Name
                                                </strong>
                                            </td>
                                            <td class="text-primary">
                                                {{ unique.name.first }}
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>
                                                <strong>
                                                    <span class="text-primary"></span>
                                                    Phone Number
                                                </strong>
                                            </td>
                                            <td class="text-primary">
                                                {{ unique.cell }}
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>
                                                <strong>
                                                    <span class="text-primary"></span>
                                                    Email
                                                </strong>
                                            </td>
                                            <td class="text-primary">
                                                {{ unique.email }}
                                            </td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>


<script>

import axios from 'axios';

export default {
    name: "ShowDetail",
    data() {
        return {
            user: [],
        };
    },
    components: {},

    mounted() {
        axios.get(`https://randomuser.me/api?results=25&id=${this.$route.params.id}`)
            .then((records) => {
                this.user = records
            });

    },
};
</script>
<style scoped>
.inf-content {
    border: 1px solid #DDDDDD;
    -webkit-border-radius: 10px;
    -moz-border-radius: 10px;
    border-radius: 10px;
    box-shadow: 7px 7px 7px rgba(0, 0, 0, 0.3);
}
</style>