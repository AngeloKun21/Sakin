<template>
  <WelcomeHeader/>
  <a-layout class="m-48 w-20px bg-transparent">
    <img class="mb-20 w-2/6 my-4 self-center" src="/assets/images/neko.png">
    <h1 class="text-black text-center text-2xl font-mono">
      Welcome to Neko Corp - where talent thrives. <br>Join us in shaping the future with your skills. <br>Explore our opportunities today!</h1>
    <a-button type="button" class="text-white font-mono text-2xl w-30 h-12 self-center mt-12 bg-gray-700" @click="$router.push('/app/applicants')">
      Get Started
    </a-button>
  </a-layout>
  <WelcomeFooter/>
</template>

<script lang="ts" setup>
declare function definePageMeta(meta: any): void;
  definePageMeta({
  layout: "RecruitmentLayout",
});
</script>

<style>

</style>