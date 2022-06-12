<template>
  <div class="home">
    <div class="container users-page">
      <div class="row">
        <div class="col-6 col-md-3 mt-3">
          <div class="form-group">
            <label for="GenderSelect">Select Gender</label>
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
        <div class="col-12 text-center">
          <div class="users-data text-left" v-for="(user, i) in users" :key="i">

            <div v-for="(detail, index) in user.results" :key="index">
              <div>
                <ul>
                  <li><img :src="detail.picture.thumbnail" /> {{ detail.gender }} {{ detail.email }} {{ detail.name.first }} {{
                      detail.name.last
                  }}</li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="load-more" @click="loadmore" >
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
      search:'',
    };
  },
  mounted() {
    axios.get('https://randomuser.me/api/?results=25')
      .then((records) => {
        this.users = records
      });
  },

// methods:{
//   loadmore(){
//     axios.get('randomuser.me/api/?offset=25&results=25')
//     .then((records) => {
//       records.map(record => this.users.push(record));
//     })

//   }
// }

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
</style>
