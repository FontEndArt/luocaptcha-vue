# [*Luosimao*](https://luosimao.com/service/captcha "Luosimao") 人机验证 在VUE中的应用

- ###演示
1. 请自行clone到本地vue项目中

2. 添加指向到Login.vue的路由

3. 打开你的vue项目对应的路由查看演示

- ###说明
Login.vue中有效代码如下  其他请自行替换为自己的逻辑代码


    <template>
      <div>
        <validate @success="SetToken"></validate>
        <button type="submit" @click="SubmitLogin">登录</button>
      <div>
    </template>
    
    <script>
    import Validate from "./Nc.vue";
    
    export default {
      data() {
        return {
          form: {
            token: ""
          }
        };
      },
      components: {
        Validate
      },
      methods: {
        SetToken(resp) {
          this.form.token = resp;
        }
      }
    };
    </script>
    

------------

### 其他细节以及服务端验证请参考：

# [*luosimao* 官方使用文档](https://luosimao.com/docs/api/56 "luosimao官方使用文档")
