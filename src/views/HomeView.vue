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
        <div class="col-6 col-md-6 mt-5">
          <div class="input-group mb-3">
            <input
              type="text"
              class="form-control"
              placeholder="SearchName"
              aria-label="Username"
              aria-describedby="basic-addon1"
            />
          </div>
        </div>
      </div>
    </div>
    <div class="container users-list">
      <div class="row">
        <div class="col-12 text-center">
          <div class="users-data text-left" v-for="(user, i) in users" :key="i">
            <!-- <img :src="user.img" /> -->
            <span
              >
              <p>{{ user.gender }}</p></span
            >
          </div>
        </div>
      </div>
      <div class="load-more">
        <button class="btn btn-primary">More Results</button>
      </div>
    </div>
  </div>
</template>

<script>
// import HelloWorld from '@/components/HelloWorld.vue'

import axios from "axios";
export default {
  name: "HomeView",

  data() {
    return {
      users: [],
    };
  },
  mounted() {
    axios.get('https://randomuser.me/api/?results=25')
    .then((records) => {
				this.state.users = records
			});
  },
  // methods: {
	// loadmore() {
	// 	axios.get('randomuser.me/api/?limit=25&offset=25')
	// 		.then((records) => {
	// 			records.map(record => this.state.users.push(record));
	// 		})
	// },
  
  components: {
    // HelloWorld
  },
};
</script>
<style scoped>
img {
  width: 5%;
  border-radius: 50%;
}
</style>
