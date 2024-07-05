<template>
  <div class="table">
    <div class="table-header">
      <div @click="sortByName" class="table-cell">Имя</div>
      <div @click="sortByNumber" class="table-cell">Телефон</div>
    </div>
    <div class="table-body">
      <ul>
        <li v-for="item in items" :key="item.id" class="table-row">
          <div class="table-cell">{{ item.name }}</div>
          <div class="table-cell">{{ item.number }}</div>
          <ul
            v-if="item.children && item.children.length"
            class="table-children"
          >
           <li v-for="child in item.children" :key="child.id">
            <TableChildren :item="child"/>
           </li>
        </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import TableChildren from './TableChildren';

export default {
  name: 'TableMain',
  data() {
    return {
      sortName: 'asc',
      sortNumber: 'asc',
    };
  },
  components: {
    TableChildren,
  },
  props: {
    items: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    sortByName() {
      if (this.sortName === 'asc') {
        this.items.sort((a, b) => a.name.localeCompare(b.name));
      }
      if (this.sortName === 'desc') {
        this.items.sort((a, b) => b.name.localeCompare(a.name));
      }
      this.sortName = this.sortName === 'asc' ? 'desc' : 'asc';
    },
    sortByNumber() {
      if (this.sortNumber === 'asc') {
        this.items.sort((a, b) => b.number.localeCompare(a.number));
      }
      if (this.sortNumber === 'desc') {
        this.items.sort((a, b) => a.number.localeCompare(b.number));
      }
      this.sortNumber = this.sortNumber === 'asc' ? 'desc' : 'asc';
    },
  },
};
</script>

<style scoped>
.table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px; /* Добавляет небольшой отступ сверху */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Добавляет легкую тень для визуального выделения */
  border-radius: 8px; /* Скругление углов таблицы */
  max-width: 300px;
}

.table-header {
  display: flex;
  justify-content: space-between;
  background-color: #f3f4f6; /* Светлый фон для заголовка таблицы */
  color: #111827; /* Цвет текста заголовков */
  font-weight: 500; /* Немного увеличиваем жирность текста */
  border-bottom: 2px solid #e5e7eb;
}

.table-header .table-cell {
  cursor: pointer;
}

.table-cell {
  padding: 16px; /* Добавляет отступы вокруг текста внутри ячейки */
}

.table-row {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  /* border-bottom: 1px solid #E5E7EB; */
}

.table-row:last-child .table-cell {
  border-bottom: none; /* Убирает границу у последней строки */
}

.table-children {
  padding-left: 16px;
  display: block;
  width: 100%;
  background-color: #f3f4f6;
}
</style>
