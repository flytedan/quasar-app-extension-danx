<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          to="/"
          icon="home"
        />

        <q-toolbar-title>
          quasar-ui-danx v{{ version }}
        </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <div class="flex flex-nowrap">
        <CollapsableSidebar v-model:collapse="isCollapsed">
          <NavigationMenu :items="menu" :hide-label="isCollapsed" />
        </CollapsableSidebar>
        <router-view />
      </div>
    </q-page-container>
  </q-layout>
</template>

<script setup>
import NavigationMenu from '@/components/NavigationMenu';
import { CollapsableSidebar, DragHandleDotsIcon as DragIcon, FilterIcon, version } from 'ui';
import { ref, shallowRef } from 'vue';

const isCollapsed = ref(false);
const menu = shallowRef([
  {
    label: 'List Item Draggable',
    icon: DragIcon,
    path: 'demo-list-item-draggable-page'
  },
  {
    label: 'Action Table',
    icon: FilterIcon,
    path: 'demo-action-table-page'
  }
]);
</script>
