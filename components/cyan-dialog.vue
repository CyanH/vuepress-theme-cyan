<template>
  <div class="dialog-container">
    <div style="text-align:center">
      <img src="../public/img/love.png">
      <div>这是我跟夫人的私人领域哦~</div>
      <div>
        <el-input
          type="password"
          placeholder="请夫人输入我们爱的代码"
          v-model="password"
        />
      </div>
      <div class="btnGroup">
        <el-button type="primary" @click="handleClose">自觉退散</el-button>
        <el-button type="succeed" @click="entry">夫人快来</el-button>
      </div>
    </div>
  </div>
</template>

<script>
import CryptoJs from 'crypto-js'
export default {
  data() {
    return {
      password: "",
    };
  },
  methods: {
    handleClose() {
      this.$parent.dialogVisible = false;
      this.$router.go(-1)
    },
    entry() {
      let key = CryptoJs.enc.Utf8.parse("慕卿子");
      let srcs = CryptoJs.enc.Utf8.parse(this.password);
      let encrypted = CryptoJs.AES.encrypt(srcs, key, {
        mode: CryptoJs.mode.ECB,
        padding: CryptoJs.pad.Pkcs7
      });

      if (encrypted.toString() === "VRyH3/PBe2IrKU2aGtgpvQ==") {
        this.$parent.dialogVisible = false;
        this.$emit("entry");
      }else{
        this.$message({
          message: '错误暗号',
          type: 'warning'
        });
      }
    },
  },
};
</script>

<style>
.dialog-container {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #fff;
  z-index: 9;
  display: flex;
  align-items: center;
  justify-content: center;
}

.btnGroup{
  display: flex;
  align-items: center;
  justify-content: space-around;
}

.btn{
  background-color: #66ccff;
  padding: 5px 10px;
  border-radius: 8px;
}
</style>