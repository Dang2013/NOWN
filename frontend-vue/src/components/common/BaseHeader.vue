<template>
  <header >
    <HeaderMenu></HeaderMenu>
  </header>
</template>

<script>
import HeaderMenu from './HeaderMenu.vue'
export default {
  components: { HeaderMenu }
}
</script>

<style scope>

header.header-base{
  padding: 1rem;
  height: 1rem;
  width: calc(100vw - 128px);
  background-color: #6DCEF5;
  justify-content: space-between;
  align-items: center;
  padding: 32px 64px;
}
.header-base{
  position: absolute;
  padding: 1rem;
  height: 1rem;
  width: calc(100vw - 128px);
  background-color: #6DCEF5;
  justify-content: space-between;
  align-items: center;
  padding: 32px 64px;
}
</style>
