<template>
  <div>
    <div class="mx-5 mt-4"> Welcome, {{ username }}</div>
    <div class="mx-5">
      <div class="row mt-2">
        <div class="col-sm-2">
          <h4>Posts for July</h4>
        </div>
        <div class="col-sm-1">
          <button type="button" class="bgColor btn btn-sm">List</button>
        </div>
        <div class="col-sm-1">
          calender
        </div>
        <div class="col-8">
          <div class="float-end">
            <div v-if="authLoader">Loading...</div>
            <button class="btn" @click="logout">Logout</button>
          </div>
        </div>
      </div>
    </div>
    <div class="ms-5 mt-5">
      <h5>July 5 - 10</h5>
    </div>
    <div class="row mt-2 px-2 mx-5 mb-5">
      <div class="col-sm-2">
        <div class="card mt-4">
          <div style="border-style: dotted; height:255px; border-radius: 16px;">
            <div class="p-2">
              <small> July 8, 8:00</small>
            </div>
            <div class="text-center" style="margin-top:40%">
              <button type="button" class="bgColor btn rounded-lg">Select</button>
            </div>
          </div>
        </div>
      </div>
      <div class="col-sm-2" v-for="(item, i) in cardText" :key="i">
        <div class="card scduledbg mt-4" id="centerbox1" v-if="item.status == 'Scheduled'">
          <div class="mt-2 mx-2">
            <small> {{ item.datetime }}</small>
          </div>
          <div class="form-check" style="position:relative; top:30px; left:7px;">
            <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault">
          </div>
          <img :src="item.keyword" alt="">
          <div class="row align-items-center p-2">
            <div class="col-1">
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                class="bi bi-clock-fill" viewBox="0 0 16 16">
                <path
                  d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zM8 3.5a.5.5 0 0 0-1 0V9a.5.5 0 0 0 .252.434l3.5 2a.5.5 0 0 0 .496-.868L8 8.71V3.5z" />
              </svg>
            </div>
            <div class="col-6">
              <small>{{ item.status }}</small>
            </div>
          </div>
        </div>
        <div class="card approvalbg mt-4" id="centerbox1" v-if="item.status == 'Needs approval'">
          <div class="mx-2 mt-2">
            <small> {{ item.datetime }}</small>
          </div>
          <div class="form-check" style="position:relative; top:30px; left:7px;">
            <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault">
          </div>
          <img :src="item.keyword" alt="">
          <div class="row align-items-center p-2">
            <div class="col-1">
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                class="bi bi-hourglass-split" viewBox="0 0 16 16">
                <path
                  d="M2.5 15a.5.5 0 1 1 0-1h1v-1a4.5 4.5 0 0 1 2.557-4.06c.29-.139.443-.377.443-.59v-.7c0-.213-.154-.451-.443-.59A4.5 4.5 0 0 1 3.5 3V2h-1a.5.5 0 0 1 0-1h11a.5.5 0 0 1 0 1h-1v1a4.5 4.5 0 0 1-2.557 4.06c-.29.139-.443.377-.443.59v.7c0 .213.154.451.443.59A4.5 4.5 0 0 1 12.5 13v1h1a.5.5 0 0 1 0 1h-11zm2-13v1c0 .537.12 1.045.337 1.5h6.326c.216-.455.337-.963.337-1.5V2h-7zm3 6.35c0 .701-.478 1.236-1.011 1.492A3.5 3.5 0 0 0 4.5 13s.866-1.299 3-1.48V8.35zm1 0v3.17c2.134.181 3 1.48 3 1.48a3.5 3.5 0 0 0-1.989-3.158C8.978 9.586 8.5 9.052 8.5 8.351z" />
              </svg>
            </div>
            <div class="col-9">
              <small>{{ item.status }}</small>
            </div>
          </div>
        </div>
        <div class="card publishedbg mt-4" id="centerbox1" v-if="item.status == 'Published'">
          <div class="mx-2 mt-2">
            <small> {{ item.datetime }}</small>
          </div>
          <div class="form-check" style="position:relative; top:30px; left:7px;">
            <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault">
          </div>
          <img :src="item.keyword" alt="">
          <div class="row align-items-center p-2">
            <div class="col-1">
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-check-lg"
                viewBox="0 0 16 16">
                <path
                  d="M12.736 3.97a.733.733 0 0 1 1.047 0c.286.289.29.756.01 1.05L7.88 12.01a.733.733 0 0 1-1.065.02L3.217 8.384a.757.757 0 0 1 0-1.06.733.733 0 0 1 1.047 0l3.052 3.093 5.4-6.425a.247.247 0 0 1 .02-.022Z" />
              </svg>
            </div>
            <div class="col-9">
              <small>{{ item.status }}</small>
            </div>
          </div>
        </div>
        <div class="card failedbg mt-4" id="centerbox1" v-if="item.status == 'Failed to post'">
          <div class="mx-2 mt-2">
            <small> {{ item.datetime }}</small>
          </div>
          <div class="form-check" style="position:relative; top:30px; left:7px;">
            <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault">
          </div>
          <img :src="item.keyword" alt="">
          <div class="row align-items-center p-2">
            <div class="col-1">
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                class="bi bi-exclamation-circle" viewBox="0 0 16 16">
                <path d="M8 15A7 7 0 1 1 8 1a7 7 0 0 1 0 14zm0 1A8 8 0 1 0 8 0a8 8 0 0 0 0 16z" />
                <path
                  d="M7.002 11a1 1 0 1 1 2 0 1 1 0 0 1-2 0zM7.1 4.995a.905.905 0 1 1 1.8 0l-.35 3.507a.552.552 0 0 1-1.1 0L7.1 4.995z" />
              </svg>
            </div>
            <div class="col-9">
              <small>{{ item.status }}</small>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import carddata from '@/static/carddata'
export default {
  auth: true,
  data: () => ({
    authLoader: false
  }),
  computed: {
    cardText() {
      return carddata
    },
    username() {
      return this.$auth.user.name
    },
  },
  methods: {
    async logout() {
      try {
        this.authLoader = true
        let response = await this.$auth.logout(this.username)
        if (response) this.authLoader = false
        this.$router.push('/login')
      } catch (error) {
        console.log(error)
      }
    }
  }
}
</script>

<style>
body {
  overflow-x: hidden;
  /* Hide scrollbars */
}

.bgColor {
  background-image: linear-gradient(98.85deg, #ED3F56 5.31%, #FC6C4D 81.84%);
  width: 88px;
  color: white;
}

.card {
  border-radius: 16px;
}

.scduledbg {
  background-color: #FFE5C7;
  color: #ED8A17;
}

.approvalbg {
  background-color: #EADFF6;
  color: #2A0C4E;
}

.publishedbg {
  background-color: #CFEFE5;
  color: #2F9876;
}

.failedbg {
  background-color: #FFD6D9;
  color: #EF4454;
}
</style>