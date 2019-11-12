<template>
  <div class="nav-menu">
    <span v-for="c in categories" v-bind:key="c">
      <a>{{ c }}</a>
    </span>
    <span class="login">
      <a>LOGIN</a>
    </span>
  </div>
</template>

<script>
export default {
  props: ["categories"]
};
</script>

<style scoped>
.nav-menu {
  max-width: 900px;
  position: absolute;
  text-align: center;
  margin-bottom: 1em;
  top: 1em;
  right: 130px;
}
@media (max-width: 1170px) {
  .nav-menu {
    display: none;
  }
}
.nav-menu span {
  margin-right: 29px;
  size: 14px;
  color: #3e433e;
  line-height: 17px;
}
.nav-menu span.login {
  margin-right: 0px;
  margin-left: 25px;
  color: #4990e2;
}
.nav-menu span a {
  cursor: pointer;
  white-space: nowrap;
}
</style>
