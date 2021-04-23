<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h1>Home</h1>
    <p>Click on "About" to trigger a navigation and be able to see the issue.
      Or use this button:</p>
    <button @click="$router.push({ name: 'About' })">Go to About</button>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: 'Home',
};
</script>
