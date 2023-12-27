<template>
  <div class="greeting">
    <p>Hello,</p>
    <input type="text" @input="ResetUsername" v-model="username" />
  </div>
</template>

<script>
export default {
  name: "GreetingArea",
  data() {
    return {
      username: "",
    };
  },
  methods: {
    ResetUsername() {
      console.log(this.username);
      localStorage.setItem("username", this.username);
    },
  },
  mounted() {
    if (!localStorage.getItem("username"))
      localStorage.setItem("username", "Write down your name here");
    const u = localStorage.getItem("username");
    var trueName = "";
    var haveSpace = true;
    for (var i = 0; i < u.length; i++) {
      if (haveSpace && u[i] != " ") {
        haveSpace = false;
      }
      if (haveSpace == false) {
        trueName += u[i];
      }
    }
    if (trueName != "") {
      console.log(localStorage.getItem("username"));
      this.username = trueName;
    } else {
      this.username = "Write down your name here";
    }
  },
};
</script>

<style scoped>
* {
  font-size: 30px;
}
.greeting {
  padding-inline: 250px;
  display: flex;
  height: 100px;
  align-items: center;
}

p {
  font-weight: 700;
}

input {
  overflow: hidden;
  width: 500px;
  color: var(--regular-text);
  border: none;
}
input:focus {
  outline: none;
}
</style>
