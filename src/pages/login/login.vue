<template>
  <div class="box">
    <div class="con">
      <h3>登录</h3>
      <div class="div1"><input type="text" v-model="user.username" /></div>
      <div class="div1"><input type="text" v-model="user.password" /></div>
      <div class="div1"><button @click="login">登录</button></div>
    </div>
  </div>
</template>
<script>
import { requserLogin } from "../../util/request";
import {mapGetters,mapActions} from 'vuex'
export default {
  components: {},
  data() {
    return {
      user: {
        username: "",
        password: "",
      },
    };
  },
  methods: {
      ...mapActions({
          requestuserList:'user/requestuserList'
      }),
    login() {
      requserLogin(this.user).then((res) => {
        if (res.data.code == 200) {
          this.requestuserList(res.data.list);
          this.$router.push("/index/home");
        } else {
          alert(res.data.msg);
        }
      });
    },
  },
  mounted() {},
};
</script>
<style>
.box {
  width: 100vw;
  height: 100vh;
  background: linear-gradient(to right, #563443, #303d60);
}

.con {
  width: 300px;
  height: 300px;
  background: #fff;
  position: relative;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  border-radius: 10px;
}

.con h3 {
  text-align: center;
}

.con input {
  width: 100%;
  height: 30px;
  border: 1px solid #000;
}
.con button {
  width: 100%;
  height: 40px;
  background: #409eff;
  color: #fff;
  font-size: 16px;
  border-radius: 10px;
}
.div1 {
  width: 70%;
  margin: 20px auto;
  text-align: center;
}
</style>