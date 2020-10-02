<template>
  <section class="main">
    <Filters @filterList="filterList"/>
    <div class="list">
      <div class="list__header">
        <input type="checkbox" name="" id="select">
        <p v-for="item in headerList" :key="item">{{ item }}</p>
        <div>
          Отобразить
        <select name="show" id="show" >
          <option value="15">15</option>
          <option value="30">30</option>
        </select>
        </div>
      </div>
      <div class="list__item">
        <List v-for="user in list" :key="user.id" :user="user"/>
      </div>
    </div>
  </section>
</template>

<script>
import Filters from '@/components/Filters.vue';
import List from '@/components/List.vue';
import users from '@/api/users.json';

export default {
  data() {
    return {
      users,
      list: [...users],
      headerList: [
        'Пользователь',
        'Дата регистрации',
        'Последняя активность',
        'Последнее действие',
        'Продукт',
      ],
    };
  },
  components: {
    Filters, List,
  },
  methods: {
    filterList(rangeDay) {
      const minDataRegistration = new Date(2000, 0, 1).getTime();
      this.list = this.users.filter((elem) => rangeDay.includes(minDataRegistration)
        || rangeDay.includes(new Date(new Date(elem.registration).toDateString()).getTime()));
    },
  },
};
</script>

<style lang="scss" scoped>
.main {
  display: grid;
  grid-template-rows: max-content 1fr;
  grid-row-gap: 10px;
  max-width: 1269px;

  font-family: Montserrat;
  font-style: normal;
  font-weight: bold;
  font-size: 13px;
  line-height: 130%;
}

.list {
  width: 100%;
  padding: 0 43px 0 32px;

  border-radius: 10px;
  background-color: #fff;

  &__header {
    display: grid;
    grid-template-columns: max-content repeat(6, 1fr);
    grid-template-rows: 62px;
    align-items: center;
    justify-items: center;
    padding: 0 10px;

    border-bottom: 2px solid #E7ECF1;
  }
}
</style>
