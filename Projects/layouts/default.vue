<template>
  <a-layout style="min-height: 100vh;" >
    <AppSidebar/>
    <a-layout>
      <AppMainHeader></AppMainHeader>
      <a-layout-content>
        <slot/>
      </a-layout-content>
    </a-layout>
  </a-layout>
 

</template>

<script lang="ts" setup>
</script>

<style>

</style>