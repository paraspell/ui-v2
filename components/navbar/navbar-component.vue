<template>
  <n-space justify="space-between">
    <n-space>
      <img
        src="~/assets/images/paraspellLogo.png"
        alt="paraspell"
        width="150"
      />
      <n-menu
        v-model:value="activeKey"
        mode="horizontal"
        :options="menuOptions"
      />
    </n-space>
    <n-space justify="end" align="center">
      <layout-select />
      <client-only>
        <wallet-component />
        <template #fallback>
          <n-button style="margin: 10px" disabled>
            Loading wallets...
          </n-button>
        </template>
      </client-only>
      <client-only>
        <dark-mode
          v-if="mainStore.darkTheme"
          class="themeIcon"
          @click="mainStore.changeTheme()"
        />
        <light-mode v-else class="themeIcon" @click="mainStore.changeTheme()" />
      </client-only>
    </n-space>
  </n-space>
</template>

<script lang="ts" setup>
import {
  AppsFilled as AppsIcon,
  CycloneFilled as CycloneIcon,
  DarkModeFilled as DarkMode,
  DarkModeTwotone as LightMode,
  HomeFilled as HomeIcon,
} from '@vicons/material'
import type { MenuOption } from 'naive-ui'
import { NButton, NIcon, NMenu, NSpace } from 'naive-ui'
import { Component, h, ref } from 'vue'
import WalletComponent from '@/components/wallet/wallet-component.vue'
import LayoutSelect from '@/components/utils/layout-select.vue'

const mainStore = useMainStore()

function renderIcon(icon: Component) {
  return () => h(NIcon, null, { default: () => h(icon) })
}

const menuOptions: MenuOption[] = [
  {
    label: () =>
      h(
        'a',
        {
          href: '/',
        },
        'Home'
      ),
    key: 'home',
    icon: renderIcon(HomeIcon),
  },
  {
    label: 'Channels',
    key: 'channels',
    icon: renderIcon(AppsIcon),
    children: [
      {
        label: () =>
          h(
            'a',
            {
              href: '/channels/open',
            },
            'Open channels'
          ),
        key: 'channels-open',
      },
      {
        label: () =>
          h(
            'a',
            {
              href: '/channels/close',
            },
            'Close channels'
          ),
        key: 'channels-close',
      },
    ],
  },
  {
    label: 'Teleport',
    key: 'teleport',
    icon: renderIcon(CycloneIcon),
    children: [
      {
        label: () =>
          h(
            'a',
            {
              href: '/teleport/relay-para',
            },
            'From relay chain'
          ),
        key: 'teleport-relay-para',
      },
      {
        label: () =>
          h(
            'a',
            {
              href: '/teleport/para-relay',
            },
            'From para-chain'
          ),
        key: 'teleport-para-relay',
      },
      {
        label: () =>
          h(
            'a',
            {
              href: '/teleport/para-para',
            },
            'Para to Para'
          ),
        key: 'teleport-para-para',
      },
    ],
  },
  {
    label: () =>
      h(
        'a',
        {
          href: '/xyk',
        },
        'XYK'
      ),
    key: 'xyk',
  },
]

const activeKey = ref<string | null>(null)
</script>

<style lang="scss" scoped>
.themeIcon {
  width: 30px;
  cursor: pointer;
  margin-right: 5px;
}
</style>