<template>
  <nuxt-layout name="default-layout">
    <n-space vertical>
      <n-card>
        <template #header>
          <h1 style="text-align: center">Teleport</h1>
          <n-divider />
        </template>
        <asset-transfer-component />
      </n-card>
    </n-space>
    <n-space vertical>
      <span class="filler" />
    </n-space>
  </nuxt-layout>
</template>

<script setup lang="ts">
import { NSpace, NCard, NDivider } from 'naive-ui'
import AssetTransferComponent from '~~/components/assets/asset-transfer-component.vue'
definePageMeta({
  layout: false,
})
</script>
