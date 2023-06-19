<template>
  <div id="app">
    <header>
      <router-link to="/">
        <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />
      </router-link>
    </header>
    <router-view />
  </div>
</template>

<script>

</script>

<style scoped>
header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 15px 0;
  margin-bottom: 20px;
}
.logo {
  width: 60px;
  height: 60px;
}
</style>
