<!-- <template>
<div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        ...
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div>
  </div>
</div>
</template> -->


<template>
<div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">User Information</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="row" v-if="isVisibility">
              <div class="col-md-4">
                <img style="width:600px; border-radius: 50%;" class="img-circle img-thumbnail"
                  :src="filteredResults.picture.medium">
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
                          {{ user }}
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
                          {{ user.phone }}
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
                          {{ filteredResults[openItem].email }}
                        </td>
                        <td class="text-primary">
                          {{ filteredResults[openItem].email }}
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
</template>

<script>

export default {
    props: ['user']
 }

</script>