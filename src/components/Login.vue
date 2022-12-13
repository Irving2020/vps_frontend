<template>
  <div class="Login-box">
    <div class="Login-container">
      <form class="Login-clock">
      </form>
      <form class="Login-form">

      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LoginPolo',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.Login-box{
  width: 100%;
  height: 100vh;
}
.Login-container{
  width: 100%;
  height: 100%;
  margin: auto;
  /* background: url('@/assets/imgs/preview.jpg') 50% 50% no-repeat;
  background-size: cover; */
  background-color: #a093cd;
}
.Login-clock{
  width: 40%;
  height: 20%;
  margin: auto;
  border-radius: 67px;
  background: #b5abd8;
  box-shadow: 35px 35px 70px #5e5779,
  -35px -35px 70px #e2cfff;
}
.Login-form{
  width: 50%;
  height: 50%;
  margin: 5% auto;
  border-radius: 28px;
  background: linear-gradient(225deg, #3a3256, #312a48);
  box-shadow:  -32px 32px 64px #161320,
  32px -32px 64px #564b80;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
</style>
