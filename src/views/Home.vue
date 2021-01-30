<template>
  <div id="app">
    <UserDetails/>
  </div>
</template>

<script>
import UserDetails from "../components/UserDetails";

export default {
  name: 'Home',
  components: {
    UserDetails
  }
}
</script>

<style>
* {box-sizing: border-box; margin: 0; padding: 0;}

body {font-family: Arial, Helvetica, sans-serif; line-height: 1.4;}

.clearfix::after {content: "";clear: both;display: table;}
</style>
