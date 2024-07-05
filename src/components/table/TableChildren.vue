<template>
  <div class="children">
    <div class="table-cell">
      {{ item.name }}
    </div>
    <div class="table-cell">
      {{ item.number }}
    </div>
    <ul v-if="item.children && item.children.length" class="table-children">
      <TableChildren v-for="child in item.children" :key="child.id" :item="child" />
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TableChildren',
  props: {
    item: {
      type: Object,
    },
  },
};
</script>

<style scoped>
.table-cell {
  padding: 16px; /* Добавляет отступы вокруг текста внутри ячейки */
}
.children {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}

.table-children {
  padding-left: 16px;
  display: block;
  width: 100%;
  background-color: #f3f4f6;
}
</style>
