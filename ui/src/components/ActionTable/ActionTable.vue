<template>
  <q-table
      ref="actionTable"
      :selected="selectedRows"
      :pagination="quasarPagination"
      :columns="columns"
      :loading="isLoadingList"
      :rows="pagedItems?.data || []"
      selection="multiple"
      :rows-per-page-options="rowsPerPageOptions"
      class="sticky-column sticky-header w-full !border-0"
      color="blue-base"
      @update:selected="$emit('update:selected-rows', $event)"
      @update:pagination="() => {}"
      @request="$emit('update:quasar-pagination', $event.pagination)"
  >
    <template #no-data>
      <slot name="empty">
        <EmptyTableState :text="`There are no ${label.toLowerCase()} matching the applied filter`" />
      </slot>
    </template>
    <template #top-row>
      <TableSummaryRow
          :label="label"
          :item-count="summary?.count || 0"
          :selected-count="selectedRows.length"
          :loading="isLoadingSummary"
          :summary="summary"
          :columns="columns"
          @clear="$emit('update:selected-rows',  [])"
      />
    </template>
    <template #header-cell="rowProps">
      <q-th
          :key="rowProps.key"
          :props="rowProps"
          :data-drop-zone="`resize-column-` + rowProps.col.name"
      >
        {{ rowProps.col.label }}
        <HandleDraggable
            v-if="rowProps.col.resizeable"
            :drop-zone="`resize-column-` + rowProps.col.name"
            class="resize-handle"
            @resize="rowProps.col.onResize"
        >
          <RowResizeIcon class="w-4 text-neutral-base" />
        </HandleDraggable>
      </q-th>
    </template>
    <template #body-cell="rowProps">
      <q-td :key="rowProps.key" :props="rowProps">
        <template v-if="rowProps.col.component">
          <RenderComponentColumn
              :row-props="rowProps"
              @action="$emit('action', $event)"
          />
        </template>
        <template v-else-if="rowProps.col.fieldList">
          <div v-for="field in rowProps.col.fieldList" :key="field">
            {{ rowProps.row[field] }}
          </div>
        </template>
        <template v-else-if="rowProps.col.filterOnClick">
          <a @click="$emit('filter', rowProps.col.filterOnClick(rowProps.row))">
            {{ rowProps.value }}
          </a>
        </template>
        <template v-else>
          <slot v-bind="{name: rowProps.col.name, row: rowProps.row, value: rowProps.value}">
            {{ rowProps.value }}
          </slot>
        </template>
      </q-td>
    </template>
  </q-table>
</template>

<script setup>
import { ref } from 'vue';
import { EmptyTableState, registerStickyScrolling, RenderComponentColumn, TableSummaryRow } from '.';
import { DragHandleIcon as RowResizeIcon } from '../../svg';
import { HandleDraggable } from '../DragAndDrop';

defineEmits(['action', 'filter', 'update:quasar-pagination', 'update:selected-rows']);
defineProps({
  label: {
    type: String,
    required: true
  },
  selectedRows: {
    type: Array,
    required: true
  },
  quasarPagination: {
    type: Object,
    required: true
  },
  isLoadingList: Boolean,
  pagedItems: {
    type: Object,
    default: null
  },
  isLoadingSummary: Boolean,
  summary: {
    type: Object,
    default: null
  },
  columns: {
    type: Array,
    required: true
  },
  rowsPerPageOptions: {
    type: Array,
    default: () => [10, 25, 50, 100]
  }
});
const actionTable = ref(null);
registerStickyScrolling(actionTable);
</script>

<style lang="scss" scoped>
[data-drop-zone] {
  .resize-handle {
    position: absolute;
    top: 0;
    right: -.45em;
    width: .9em;
    opacity: 0;
    transition: all .3s;
  }

  &:hover {
    .resize-handle {
      opacity: 1;
    }
  }
}
</style>
