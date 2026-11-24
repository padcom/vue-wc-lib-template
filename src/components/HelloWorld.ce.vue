<template>
  <button class="btn-primary" @click="console.log('Hello!')">{{ t('hello-world') }}</button>
</template>

<script lang="ts" setup>
import { provide, watchEffect } from 'vue'
import { I18nInjectionKey } from 'vue-i18n'
import i18n from '../i18n'

const props = defineProps({
  lang: { type: String, default: '' },
})

// synchronize i18n locale with lang prop
watchEffect(() => {
  i18n.global.locale.value = props.lang || i18n.global.locale.value
})

// make i18n available to child components using useI18n()
provide(I18nInjectionKey, i18n)

const { t } = i18n.global
</script>

<style lang="postcss">
@import '@padcom/nano-css-reset';

:host {
  display: block;
}
</style>
