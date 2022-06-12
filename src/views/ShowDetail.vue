<template>
    <div class="container show-details mt-5">
        <div class="panel-body inf-content">
            <div v-for="(uniquedetail, i) in user" :key="i">
                <div v-for="(unique, i) in uniquedetail.results" :key="i">
                    <div class="row">
                        <div class="col-md-4">
                            <img alt="" style="width:600px;" title="" class="img-circle img-thumbnail isTooltip"
                                :src="unique.picture.large">
                        </div>
                        <div class="col-md-6">
                            <div class="table-responsive">
                                <table class="table table-user-information">
                                    <tbody>
                                        <tr>
                                            <td>
                                                <strong>
                                                    <span class="glyphicon glyphicon-user  text-primary"></span>
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
                                                    <span class="glyphicon glyphicon-asterisk text-primary"></span>
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
                                                    <span class="glyphicon glyphicon-envelope text-primary"></span>
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


<!-- <template>
    <div class="container">
        <div class="row">
            <div class="col-4 text-center m-auto pt-5">
                <div v-for="(uniquedetail, i) in user" :key="i">
                    <div v-for="(unique, i) in uniquedetail.results" :key="i">
                        <div class="card" style="width: 18rem;">
                            <img class="card-img-top" :src="unique.picture.medium" alt="Card image cap">
                            <div class="card-body">
                                <h5 class="mt-0">{{ unique.name.first }}</h5>
                                <h6> {{ unique.email }} </h6>
                                <h6> {{ unique.cell }} </h6>
                                <p class="card-text">Some quick example text to build on the card title and make up the
                                    bulk of the card's content.</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template> -->

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
        axios.get('https://randomuser.me/api/?results=25/${id.value}')
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