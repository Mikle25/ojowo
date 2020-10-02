<template>
  <div class="list-elem">
    <input type="checkbox" name="" id=""/>
    <p>{{ user.name }}</p>
    <p>{{ dateShow(user.registration) }}</p>
    <p>{{ dateShow(user.activity) }}</p>
    <p>{{ user.action }}</p>
    <p>{{ user.product }}</p>
    <div class="list-elem__control">
      <input class="list-elem__edit" type="button">
      <input class="list-elem__remov" type="button">
    </div>
  </div>
</template>

<script>
export default {
  props: ['user'],
  data() {
    return {
      monthes: [
        'Январь',
        'Февраль',
        'Март',
        'Апрель',
        'Май',
        'Июнь',
        'Июль',
        'Август',
        'Сентябрь',
        'Октябрь',
        'Ноябрь',
        'Декабрь',
      ],
    };
  },
  methods: {
    dateShow(date) {
      const dateRegistration = new Date(date);
      const year = dateRegistration.getFullYear();
      const month = this.monthes[dateRegistration.getMonth()];
      const day = dateRegistration.getDate();

      return `${month} ${day}, ${year} г.`;
    },
  },
};
</script>

<style lang="scss" scoped>
  .list-elem {
    display: grid;
    grid-template-columns: max-content repeat(6, 1fr);
    grid-auto-rows: 57px;
    align-items: center;
    justify-items: center;
    padding: 0 10px;

    font-style: normal;
    font-weight: 500;
    font-size: 15px;
    line-height: 130%;

    &__control {
      display: grid;
      grid-template-columns: repeat(2, 23px);
      grid-template-rows: 23px;
      grid-column-gap: 20px;
      justify-content: center;
    }

    &__edit {
      background: url('../assets/image/icon/edit.svg') no-repeat 50%;
      background-size: cover;
    }
    &__remov {
      background: url('../assets/image/icon/delete.svg') no-repeat 50%;
      background-size: cover;
    }

  }
</style>
