<template>
  <div class="warning-box">
    <p style="color: #fff">You haven't write down anything!</p>
  </div>
</template>

<script>
export default {
  name: "NullInputWarning",
  props: {
    setOpacity: Number,
  },
  data() {
    return {
      nowOpacity: 0,
    };
  },
  mounted() {
    setInterval(() => {
      if (this.setOpacity == 0 && this.nowOpacity < 0.01) this.nowOpacity = 0;
      if (this.setOpacity == 1 && 1 - this.nowOpacity < 0.01)
        this.nowOpacity = 1;
      if (Math.abs(this.setOpacity - this.nowOpacity) >= 0.01)
        this.nowOpacity = this.nowOpacity * 0.9 + this.setOpacity * 0.1;
      document.querySelector(".warning-box").style.opacity = this.nowOpacity;
    }, 10);
  },
};
</script>

<style scoped>
.warning-box {
  width: 400px;
  height: 50px;
  background-color: #f56c6c;
  border: 1px solid #e05151;
  display: flex;
  align-items: center;
}

p {
  width: 400px;
  font-size: 20px;
  text-align: center;
}
</style>
