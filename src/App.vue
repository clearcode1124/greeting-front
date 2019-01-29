<template>
  <div id="app">
    <div class="gen">
      <Input class="gen-param" v-model="name" placeholder="请输入对方的称呼"/>
      <Input class="gen-param" v-model="message" type="textarea" placeholder="请输入祝福语"/>
      <Button type="primary" @click="gen">生成</Button>
    </div>
    <div class="gen-image">
      <img v-if="imageShow" :src="imageSrc" style="width:100%;height:100%;">
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      name: "",
      message: "",
      imageShow: false,
      imageSrc: ""
    };
  },
  methods: {
    gen() {
      let genParam = new Object();
      genParam.name = this.name;
      genParam.message = this.message;
      let name = this.name;
      let that = this;
      this.$http
        .post(this.HOST + "/cards/gen-single", JSON.stringify(genParam), {
          headers: {
            "content-type": "application/json"
          }
        })
        .then(function(res) {
          console.log(res);
          that.imageShow = true;
          that.imageSrc = "http://hk.clearcode.top/hk1-" + name + ".png";
        });
    }
  }
};
</script>

<style>
html,body{
  width: 100%;
  overflow-x: hidden;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.gen {
  height: 20%;
}
.gen-param {
  width: 80%;
  margin: 10px;
}
.gen-image {
  width: 90%;
  height: 80%;
  margin-top: 20px;
}
</style>
