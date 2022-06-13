<template>
  <div class="home">
    <div class="container users-page">
      <form class="row" @submit.prevent="searchData">
        <div class="col mt-3">
          <div class="form-group">
            <label for="GenderSelect"><strong>Select Gender</strong></label>
            <select class="form-control" id="GenderSelect" v-model="gender">
              <option value="">All</option>
              <option value="male">Male</option>
              <option value="female">Female</option>
            </select>
          </div>
        </div>
        <div class="col mt-5">
          <div class="input-group mb-3">
            <input type="text" class="form-control" v-model="keyword" placeholder="SearchName" />
          </div>
        </div>
        <div class="col mt-5">
          <div class="input-group mb-3">
            <button class="btn btn-primary" :class="loading ? 'btn-disabled' : ''" :disabled="loading ? true : false"
              type="submit">
              Search
            </button>
            <button class="btn btn-secondary ml-2" :class="loading ? 'btn-disabled' : ''"
              :disabled="loading ? true : false" @click="reset" type="button">
              Reset
            </button>
          </div>
        </div>
      </form>
    </div>
    <div class="container users-list">
      <div class="row">
        <div class="col-12 users-data text-left">
          <div class="row" v-if="!this.fullLoading">
            <div class="col-12 col-md-4" v-for="(detail, index) in users" :key="index">
              <div class="card mb-3 text-left pointer" @click="openModel(index)">
                <div class="card-body">
                  <div class="media pt-2 pb-3">
                    <a>
                      <img class="align-self-center mr-3" :src="detail.picture.thumbnail" />
                    </a>
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
      <div class="load-more pt-2 pb-5 text-center">
        <button class="btn btn-primary" :class="loading ? 'btn-disabled' : ''" :disabled="loading ? true : false"
          @click="loadmore" type="button">
          More Results
        </button>
      </div>
    </div>

    <div class="modal" tabindex="-1" data-target="#myModal" id="myModal">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">User Information</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="row" v-if="openItem >= 0 && users[openItem]">
              <div class="col-md-4">
                <img style="width:600px; border-radius: 50%;" class="img-circle img-thumbnail"
                  :src="users[openItem].picture.medium">
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
                          {{ users[openItem].name.first }}
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
                          {{ users[openItem].cell }}
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
                          {{ users[openItem].email }}
                        </td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
          </div>
        </div>
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
      page: 1,
      loading: false,
      keyword:'',
      gender: '',
      fullLoading: false,
      openItem: null,
    };
  },
  mounted() {
    this.loading = true;
    axios.get(`https://randomuser.me/api/?results=25&page=${this.page}`)
      .then(response => response.data.results)
      .then((records) => {
        this.users = records
      })
      .finally(() => this.loading = false);
  },

  methods: {
    loadmore() {
      this.page = this.page+1;
      this.loading = true;

      axios.get(`https://randomuser.me/api/?results=25&page=${this.page}&name=${this.keyword}&gender=${this.gender}`)
        .then(response => response.data.results)
        .then((records) => {
          records.map(record => this.users.push(record));
        })
        .finally(() => this.loading = false);
    },
    reset() {
      this.page = 1;
      this.loading = true;
      this.keyword = '';
      this.gender = '';
      this.fullLoading = true;

      axios.get(`https://randomuser.me/api/?results=25&page=${this.page}&name=${this.keyword}&gender=${this.gender}`)
        .then(response => response.data.results)
        .then((records) => {
          this.users = records;
        })
        .finally(() => {
          this.loading = false;
          this.fullLoading = false;
        });
    },
    searchData() {
      this.page = 1;
      this.loading = true;
      this.fullLoading = true;

      axios.get(`https://randomuser.me/api/?results=25&page=${this.page}&first_name=${this.keyword}&gender=${this.gender}`)
        .then(response => response.data.results)
        .then((records) => {
          this.users = records;
        })
        .finally(() => {
          this.loading = false;
          this.fullLoading = false;
        });
    },

    openModel(i) {
      this.openItem = i;
      window.$('#myModal').modal('show')
    }
  },
};
</script>
<style scoped>
.users-list .users-data ul {
  list-style-type: none;
}
.pointer {
  cursor: pointer;
}
</style>
