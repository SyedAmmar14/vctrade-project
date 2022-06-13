<template>
  <div class="home">
    <div class="container users-page">
      <div class="row">
        <div class="col-6 col-md-3 mt-3">
          <div class="form-group">
            <label for="GenderSelect"><strong>Select Gender</strong></label>
            <select class="form-control" id="GenderSelect">
              <option>All</option>
              <option>Male</option>
              <option>Female</option>
            </select>
          </div>
        </div>
        <div class="col-6 col-md-3 mt-5">
          <div class="input-group mb-3">
            <input type="text" class="form-control" v-model="search" placeholder="SearchName" />
          </div>
        </div>
      </div>
    </div>
    <div class="container users-list">
      <div class="row">
        <div class="col-12 users-data text-left">
          <div class="row" v-for="(user, i) in users" :key="i">
            <div class="col-12 col-md-4" v-for="(detail, index) in user.results" :key="index">
              <div class="card mb-3 text-left">
                <div class="card-body">
                  <div class="media pt-2 pb-3">
                    <router-link :to="`/${detail.id.value}`">
                      <img class="align-self-center mr-3" :src="detail.picture.thumbnail" />
                    </router-link>
                    <div class="media-body">
                      <h5 class="mt-0">{{ detail.name.first }} {{ detail.name.last }}</h5>
                      <h6>{{ detail.email }}</h6>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="load-more pt-2 pb-5 text-center" @click="loadmore">
        <button class="btn btn-primary">More Results</button>
      </div>
    </div>
  </div>
</template>
<script>


import axios from "axios";
export default {
  name: "HomeView",

  data() {
    return {
      users: [],
      search: '',
    };
  },
  mounted() {
    axios.get('https://randomuser.me/api/?results=25')
      .then((records) => {
        this.users = records
      });
  },

  methods: {
    loadmore() {
      axios.get('https://randomuser.me/api/?results=25&offset=25')
        .then((records) => {
          records.map(record => this.users.push(record));
        });


    }
  }

  // computed: {

  //   filteredUsers: function() {
  //     return this.users.filter((detail) =>{
  //         return detail.first.match(this.search);
  //     });
  //   }
  // }
};
</script>
<style scoped>
.users-list .users-data ul {
  list-style-type: none;
}
</style>
