<template>
  <div>
    <validate @success="SetToken"></validate>
    <button type="submit" @click="SubmitLogin">登录</button>
  <div>
</template>

<script>
import { Message } from "element-ui";
import Validate from "./Nc.vue";

export default {
  data() {
    return {
      form: {
        token: ""
      },
      submit: false
    };
  },
  components: {
    Validate
  },
  methods: {
    SubmitLogin() {
      if (!this.submit) {
        return;
      }

      if (!this.ncVerify()) {
        Message.error({ message: "请重新验证" });
        return;
      }

      let PostData = this.form;
      let url = "http://127.0.0.1:8001/login/login";

      this.$ajax
        .post(url, this.qs.stringify(PostData))
        .then(res => {
          // console.log(res);
          if (res.code === 200) {
            Message({
              type: "success",
              message: "登录成功",
              center: true,
              duration: 1000
            });
          } else {
            Message.error({ message: res.description });
            this.ResetValidate();
          }
        })
        .catch(() => {
          this.ResetValidate();
        });
    },
    ncVerify() {
      if (!this.form.token) {
        this.ResetValidate();
        return false;
      }
      return true;
    },
    ResetValidate() {
      this.form.token = "";
      // eslint-disable-next-line
      LUOCAPTCHA && LUOCAPTCHA.reset();
    },
    SetToken(resp) {
      this.submit = true;
      this.form.token = resp;
    }
  }
};
</script>