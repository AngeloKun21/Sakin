<template>
    <a-layout-sider style="background-color: #16212c;">
        <AppSidebarHeader></AppSidebarHeader>
        <a-row class="align-start">
            <button class="text-white m-5 pl-5 cursor-pointer" @click="$router.push('/app/applicants')"><UserOutlined class="text-lg"/>APPLICANTS</button>
            <button class="text-white m-5 pl-5 cursor-pointer text-center" @click="$router.push('/app/post')"><AuditOutlined class="text-lg"/>USERPOST</button>
        </a-row>
    </a-layout-sider>
</template>

<script lang="ts" setup>
</script>

<style>
</style>