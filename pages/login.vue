<template>
  <div>
    <div class="cardstyle bg-white overflow-hidden shadow sm:rounded-lg mt-5">
      <h2 class="text-center mt-4">Login</h2>
      <div class="text-center pt-5">
        <img src="https://content.app-sources.com/s/80487845485150444/uploads/fonts/Logo-full-8150045.svg" alt="">
      </div>
      <div class="text-center mt-4">
        <div v-if="authLoader">Loading...</div>
        <button type="button" class="btn bg-primary white--text my-5" data-bs-toggle="modal"
          data-bs-target="#exampleModal" style="width:200px;" @click="loginwithfb">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-facebook"
            viewBox="0 0 16 16">
            <path
              d="M16 8.049c0-4.446-3.582-8.05-8-8.05C3.58 0-.002 3.603-.002 8.05c0 4.017 2.926 7.347 6.75 7.951v-5.625h-2.03V8.05H6.75V6.275c0-2.017 1.195-3.131 3.022-3.131.876 0 1.791.157 1.791.157v1.98h-1.009c-.993 0-1.303.621-1.303 1.258v1.51h2.218l-.354 2.326H9.25V16c3.824-.604 6.75-3.934 6.75-7.951z" />
          </svg>
          <span class="ml-2">Facebook</span>
        </button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  middleware: 'auth',
  data: () => ({
    authLoader: false,
  }),
  methods: {
    async loginwithfb() {
      try {
        this.authLoader = true
        let response = await this.$auth.loginWith('facebook')
        if (response) this.authLoader = false
      } catch (error) {
        console.log(error)
      }

    }
  }

}
</script>

<style>
.cardstyle {
  margin-left: 20%;
  margin-right: 20%;
}
.btn{
  color: white;
}
</style>