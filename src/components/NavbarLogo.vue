<template>
  <div id="header">
    <a href="#">
      <img id="logo" src="../assets/logo.png" />
    </a>
  </div>
</template>

<style scoped>
#header {
  height: 53px;
  padding-bottom: 1px;
  padding-top: 2px;
  border-bottom: solid 1px;
  border-color: #979797;
}
#header #logo {
  margin-left: 131px;
  margin-top: 4px;
}
@media (max-width: 1170px) {
  #header #logo {
    margin-left: 0px;
    margin-bottom: 5px;
  }

  #header {
    display: flex;
    align-items: center;
    justify-content: center;
  }
}
</style>
