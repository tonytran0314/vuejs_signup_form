<script setup>
  import SignupForm from './components/SignupForm.vue';
</script>

<template>
  <div class="container">
    <SignupForm />
  </div>
</template>

<style lang="scss">
  @import './assets/variables';
  .container {
    @include horizontalCenter();
    background-color: $formContainerBackgroundColor;
    padding: $baseDistance * 7;
    border-radius: $baseDistance * 2;
  }
</style>