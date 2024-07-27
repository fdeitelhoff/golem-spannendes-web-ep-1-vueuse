<script setup lang="ts">
import { ref, watch } from 'vue';
import { useGlobalState } from '../modules/store.ts';

console.log(useGlobalState());

import { useActiveElement } from '@vueuse/core';
import { UseActiveElement } from '@vueuse/components';

const activeElement = useActiveElement();

watch(activeElement, (el) => {
  console.log('focus changed to', el);
});

import { useDocumentVisibility } from '@vueuse/core';

const visibility = useDocumentVisibility();

watch(visibility, (current, previous) => {
  console.log('Visibility', visibility.value);
});

import { useBluetooth } from '@vueuse/core';

const { isSupported, isConnected, device, requestDevice, server } =
  useBluetooth({
    acceptAllDevices: true,
  });

import { useFileDialog } from '@vueuse/core';

const { files, open, reset } = useFileDialog();
</script>

<template>
  <UseActiveElement v-slot="{ element }">
    <input />
    <input />
    Active element is {{ element.dataset.id }}
  </UseActiveElement>
  <button @click="requestDevice()">Bluetooth-Gerät anfragen</button>
  <button type="button" @click="open">Datei auswählen</button>
</template>

<style scoped></style>
