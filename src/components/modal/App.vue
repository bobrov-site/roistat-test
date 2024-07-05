<template>
  <div v-if="showModal" class="modal">
    <div class="modal-body">
      <div class="modal-header">
        <h3 class="modal-title">Добавление пользователя</h3>
        <button @click="closeModal" class="modal-close" type="button">X</button>
      </div>
      <form @submit.prevent="addUser" class="form">
        <div class="form-group">
          <label for="name">Имя</label>
          <input id="name" class="form-input" type="text" />
        </div>
        <div class="form-group">
          <label for="number">Телефон</label>
          <input id="number" class="form-input" type="text" />
        </div>
        <div class="form-group">
          <label for="bossId">Начальник</label>
          <select id="bossId" class="form-input">
            <option v-for="item in optionsList" :key="item.id" :value="item.id">
              {{ item.name }}
            </option>
          </select>
        </div>
        <PrimaryButton type="submit">Сохранить</PrimaryButton>
      </form>
    </div>
  </div>
</template>

<script>
import PrimaryButton from '../ui/PrimaryButton';

export default {
  name: 'ModalMain',
  components: {
    PrimaryButton,
  },
  props: {
    showModal: {
      type: Boolean,
    },
    items: {
      type: Array,
    },
  },
  computed: {
    optionsList() {
      return this.generateOptions(this.items);
    },
  },
  methods: {
    closeModal() {
      this.$emit('closeModal');
    },
    generateOptions(items, depth = 0) {
      debugger;
      let options = [];
      items.forEach((item) => {
        options.push({ name: '-'.repeat(depth) + item.name, id: item.id });
        if (item.children && item.children.length) {
          options = options.concat(this.generateOptions(item.children, depth + 1));
        }
      });
      return options;
    },
    addUser($event) {
      const user = {
        name: $event.target.elements.name.value,
        number: $event.target.elements.number.value,
        id: Date.now(),
        children: [],
        bossId: Number($event.target.elements.bossId.value),
      };
      this.$emit('addUser', user);
      this.closeModal();
    },
  },
};
</script>

<style scoped>
.modal {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 9999;
  overflow: auto;
  padding: 16px;
}
.modal-body {
  background-color: #fff;
  padding: 16px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  max-width: 500px;
  width: 100%;
  max-height: 500px;
  overflow: auto;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;
}

.modal-title {
  margin: 0;
  font-size: 24px;
  font-weight: 500;
  color: #111827;
}
.modal-close {
  background-color: transparent;
  border: none;
  cursor: pointer;
  font-size: 24px;
  color: #111827;
}
.form-input {
  width: 100%;
  max-width: 400px;
  height: 40px;
  border-radius: 8px;
  border: 1px solid #e5e7eb;
  padding: 0 16px;
  font-size: 16px;
  color: #111827;
  outline: none;
}

.form-group {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 16px;
}
</style>
