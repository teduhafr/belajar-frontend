<template>
  <div class="home">
      <div class="container container-md">
        <form class="form" @submit.prevent="LoginUser" >
          <div class="mb-3">
            <label for="User" class="form-label">User Name </label>
            <input type="text" class="form-control" id="username" v-model="state.user"
            :class="UserNameCount.length < 6 ? 'btn btn-danger' : ''" aria-describedby="userHelp">
            <div id="userHelp" class="form-text">Nama minimal 6 karakter dan hanya huruf dan angka!</div>
          </div>
          <div class="mb-3">
            <label for="exampleInputPassword1" class="form-label"> Password</label>
            <input type="password" class="form-control" id="password" v-model="state.password"
            :class="PasswordCount.length < 8 ? 'btn btn-danger' : ''">
            <div id="userhelp" class="form-text">Password minimal 8 karakter.</div>
          </div>
          <button v-if="state.canSumbit" type="submit" class="btn btn-primary">Login</button>
        </form>
</div>
  </div>
</template>

<script>
// @ is an alias to /src

import { reactive, watch, computed } from "vue";

export default {
  name: 'Login',
  components: {
  },
  setup(){
      const state = reactive({
          user : "isi nama Anda",
          password : "default",
          canSumbit: false
      });
    const UserNameCount = computed(() => state.user);
    const PasswordCount = computed(() => state.password);
    watch(UserNameCount, (a, b)=> {
        cansubmit1( a, b );
         
})

    watch(PasswordCount, (a, b)=> {
         if ( b.length >= 8) {
          state.canSumbit = true
        }
              if (b.length < 7) {
                state.canSumbit = false
        }
         
})
function cansubmit1 ( a,b ) {

         if ( /^[A-Za-z0-9]+$/.test(b) && b.length > 5) {
          state.canSumbit = true
        }
              if (b.length <= 5 || !(/^[A-Za-z0-9]+$/.test(b))) {
                state.canSumbit = false
        }
}
     function LoginUser() {
          console.log(state.user+"   "+state.password)      
      }
      
return {
      state,
      LoginUser,
      UserNameCount,
      PasswordCount,
      cansubmit1
  };
  }
  };
</script>
