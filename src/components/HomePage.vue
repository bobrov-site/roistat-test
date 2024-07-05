<template>
  <div class="container">
    <div class="row">
      <PrimaryButton @click.native="toggleModal" type="button">Добавить</PrimaryButton>
    </div>
    <div class="row">
      <Table :items="items" />
      <Modal @addUser="addUser" @closeModal="toggleModal" :items="items" :showModal="showModal" />
    </div>
  </div>
</template>

<script>
import TableMain from './table/App';
import ModalMain from './modal/App';
import PrimaryButton from './ui/PrimaryButton';

export default {
  name: 'HelloWorld',
  components: {
    Table: TableMain,
    Modal: ModalMain,
    PrimaryButton,
  },
  mounted() {
    if (localStorage.getItem('items')) {
      this.items = JSON.parse(localStorage.getItem('items'));
    }
  },
  data() {
    return {
      items: [
        {
          id: 1,
          name: 'Марина',
          number: '+79624256601',
          children: [
            {
              id: 2,
              name: 'Марина2',
              number: '+79624256601123',
            },
            {
              id: 6,
              name: 'Марина4',
              number: '+79624256601123',
              children: [
                {
                  id: 8,
                  name: 'Марина2',
                  number: '+79624256601123',
                },
                {
                  id: 10,
                  name: 'Марина2',
                  number: '+79624256601123',
                },
              ],
            },
          ],
        },
        {
          id: 3,
          name: 'Евгений',
          number: '+7962425661234',
          children: [
            {
              id: 4,
              name: 'Евгений 2',
              number: '+796242566011234',
            },
          ],
        },
        {
          id: 33,
          name: 'Вася',
          number: '+796242566121234',
        },
      ],
      showModal: false,
    };
  },
  methods: {
    toggleModal() {
      this.showModal = !this.showModal;
    },
    addUser(user) {
      this.items.forEach((item) => {
        if (item.id === user.bossId) {
          item.children = [...item.children, user];
          localStorage.setItem('items', JSON.stringify(this.items));
        }
      });
    },
  },
};
</script>

<style scoped>
.container {
  margin: 0 auto;
  max-width: 1720px;
  margin-bottom: 36px;
  @media screen and (max-width: 1920px) {
    margin: unset;
    margin-left: 100px;
    margin-right: 100px;
  }
  @media screen and (max-width: 1139px) {
    margin-left: 16px;
    margin-right: 16px;
  }
}
.row {
  display: flex;
  justify-content: space-between;
  margin-top: 42px;
}
</style>
