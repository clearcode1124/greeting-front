<template>
  <div class="img1">
    <div class="gen">
      <Input class="gen-param" v-model="name" placeholder="请输入对方的称呼"/>
      <Input class="gen-param" v-model="message" :rows="4" type="textarea" placeholder="请输入祝福语"/>
      <Button type="primary" @click="gen" long style="width: 30%;">生成</Button>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      name: "",
      message: ""
    };
  },
  methods: {
    gen() {
      let genParam = new Object();
      let name = this.name + new Date().getTime();
      console.log(name + "===" + this.message);
      genParam.name = name;
      genParam.message = this.message;
      let that = this;
      this.$http
        .post(this.HOST + "/cards/gen-single", JSON.stringify(genParam), {
          headers: {
            "content-type": "application/json"
          }
        })
        .then(function(res) {
          console.log(res);
          that.$router.push({
            name: "GenImg",
            params: {
              src: "http://hk.clearcode.top/hk1-" + name + ".png"
            }
          });
          console.log(res);
        });
    }
  }
};
</script>

<style>
.img1 {
  width: 100%;
  height: 100%;
  background-image: url("../assets/bg3.png");
  background-size: cover;
}
.gen {
  height: 30%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.gen-param {
  width: 60%;
  margin: 10px;
  margin-right: 15px;
}
</style>
