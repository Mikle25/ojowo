<template>
  <div class="popup-box" ref="popup-box">
    <div class="container">
      <div class="filter-days">
      <input
        type="button"
        class="filter-days__btn"
        v-for="(item, index) in filterDays"
        :key="index"
        :class="{active: selectedDay === item}"
        @click="selectRange"
        :value="item"
      >
      </div>
      <div class="calendar">
        <div class="calendar__month">
          <button
            class="calendar__btn-prev btn-calendar"
            @click="decrease"
          />
          <p>{{monthes[month]}}, {{year}}</p>
          <button
            class="calendar__btn-next btn-calendar"
            @click="increase"
          />
        </div>
          <section class="calendar__days">
            <ul class="calendar__day-of-week">
              <li v-for="d in day" :key="d">{{ d }}</li>
            </ul>
            <ul
              class="calendar__week"
              v-for="(week) in calendar()"
              :key="week.index"
            >
              <li
                class="calendar__day"
                v-for="(day, index) in week"
                :key="index"
                :class="{
                  'select-day': showSelectedDay(day.index) ,
                  'select-day__first-last': selectedRangeDay[0] === firstLastDayOfRange(day.index)
                  || selectedRangeDay[selectedRangeDay.length - 1]
                  === firstLastDayOfRange(day.index)
                  || showCustomRange(day.index)
                }"
                @click="castomSelectDay"
                :value="day.index"
              >
                {{ day.index}}
              </li>
            </ul>
          </section>
        <div class="calendar__control">
          <button class="calendar__cancel" @click="cancel">Отмена</button>
          <button
            class="calendar__update"
            :class="{update: isActiveBtn}"
            @click="update"
            :disabled="!isActiveBtn"
          >
            Обновить
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      date: new Date(),
      month: new Date().getMonth(),
      year: new Date().getFullYear(),
      today: new Date().getDate(),
      dFirstMonth: 1,
      day: ['Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб', 'Вс'],
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
      filterDays: [
        'Весь срок',
        'Сегодня',
        'Вчера',
        'Последние 7 дней',
        'Последние 30 дней',
        'В этом месяце',
        'Прошлый месяц',
      ],
      selectedDay: 'Сегодня',
      isActiveBtn: false,
      selectedTextFilter: 'За 1 день',
      selectedRangeDay: [],
      customUserSelectRange: [],
    };
  },
  methods: {
    closeCalendar() {
      this.$emit('closeCalendar');
    },
    calendar() {
      const days = [];
      let week = 0;
      const dlast = new Date(this.year, this.month + 1, 0).getDate();
      days[week] = [];
      let a;

      for (let i = 1; i <= dlast; i += 1) {
        if (new Date(this.year, this.month, i).getDay() !== this.dFirstMonth) {
          a = { index: i };
          days[week].push(a);
        } else {
          week += 1;
          days[week] = [];
          a = { index: i };
          days[week].push(a);
        }
      }

      if (days[0].length > 0) {
        for (let i = days[0].length; i < 7; i += 1) {
          days[0].unshift('');
        }
      }

      return days;
    },
    decrease() {
      this.month -= 1;

      if (this.month < 0) {
        this.month = 12;
        this.month -= 1;
        this.year -= 1;
      }
    },
    increase() {
      this.month += 1;

      if (this.month > 11) {
        this.month = -1;
        this.month += 1;
        this.year += 1;
      }
    },
    selectRange(e) {
      this.selectedDay = e.target.value;
      let count;
      let currentDay = new Date().getDate();

      this.isActiveBtn = true;
      this.selectedRangeDay = [];
      this.customUserSelectRange = [];

      switch (e.target.value) {
        case 'Весь срок':
          this.selectedRangeDay.push(new Date(2000, 0, 1).getTime());
          this.selectedTextFilter = 'Весь срок';
          break;
        case 'Сегодня':
          this.month = new Date().getMonth();
          this.selectedRangeDay.push(new Date(this.year, this.month, currentDay).getTime());
          this.selectedTextFilter = 'За 1 день';
          break;
        case 'Вчера':
          this.month = new Date().getMonth();
          this.selectedRangeDay.push(new Date(this.year, this.month, currentDay - 1).getTime());
          this.selectedTextFilter = 'За 1 день';
          break;
        case 'Последние 7 дней':
          this.month = new Date().getMonth();
          count = 0;
          currentDay = new Date().getDate();
          this.selectedTextFilter = 'За 7 дней';

          while (count < 7) {
            this.selectedRangeDay.push(new Date(this.year, this.month, currentDay).getTime());
            currentDay -= 1;
            count += 1;
          }
          break;
        case 'Последние 30 дней':
          this.month = new Date().getMonth();
          this.selectedTextFilter = 'За 30 дней';
          count = 0;
          currentDay = new Date().getDate();

          while (count < 30) {
            this.selectedRangeDay.push(new Date(this.year, this.month, currentDay).getTime());
            currentDay -= 1;
            count += 1;
          }
          break;
        case 'В этом месяце':
          count = 0;
          currentDay = new Date().getDate();
          this.month = new Date().getMonth();
          this.selectedTextFilter = 'В этом месяце';

          while (count < new Date().getDate()) {
            this.selectedRangeDay.push(new Date(this.year, this.month, currentDay).getTime());
            currentDay -= 1;
            count += 1;
          }
          break;
        case 'Прошлый месяц':
          this.month = new Date().getMonth() - 1;
          this.selectedTextFilter = 'Прошлый месяц';
          count = 0;
          currentDay = new Date(this.year, new Date().getMonth(), 0).getDate();
          console.log(currentDay);

          while (count < currentDay) {
            this.selectedRangeDay.push(new Date(this.year, this.month, currentDay).getTime());
            currentDay -= 1;
          }
          break;
        default:
      }
    },
    cancel() {
      this.month = new Date().getMonth();
      this.year = new Date().getFullYear();
      this.today = new Date().getDate();
      this.isActiveBtn = false;
      this.selectedRangeDay = [];
      this.customUserSelectRange = [];
      this.selectedDay = 'Сегодня';
      this.selectedRangeDay.push(new Date(this.year, this.month, this.today).getTime());
    },
    update() {
      this.$emit('update', false, this.selectedTextFilter, this.selectedRangeDay);
    },
    showSelectedDay(day) {
      return this.selectedRangeDay.includes(new Date(this.year, this.month, day).getTime());
    },
    firstLastDayOfRange(day) {
      return new Date(this.year, this.month, day).getTime();
    },
    castomSelectDay(event) {
      const day = event.target.value;
      this.selectedRangeDay = [];

      if (this.customUserSelectRange.length <= 2) {
        this.selectedRangeDay = [];
        this.isActiveBtn = true;
        this.customUserSelectRange.push(new Date(this.year, this.month, day).getTime());
        this.customUserSelectRange.sort();
        const firstDayOfRange = `${new Date(this.customUserSelectRange[0]).getDate()}`
        + ` ${this.monthes[new Date(this.customUserSelectRange[0]).getMonth()].slice(0, 3)}`;

        if (this.customUserSelectRange.length === 2) {
          const min = Math.min(...this.customUserSelectRange);
          const max = Math.max(...this.customUserSelectRange);
          const oneDay = 86400000;
          const lastDayOfRange = `${new Date(this.customUserSelectRange[1]).getDate()}`
          + ` ${this.monthes[new Date(this.customUserSelectRange[1]).getMonth()].slice(0, 3)} ${this.year} г.`;

          for (let i = max; i >= min; i -= oneDay) {
            this.selectedRangeDay.push(new Date(i).getTime());
          }

          this.selectedTextFilter = `${firstDayOfRange} - ${lastDayOfRange}`;
          return;
        }

        this.selectedRangeDay.push(...this.customUserSelectRange);
        this.selectedTextFilter = `${firstDayOfRange} ${this.year} г.`;
      }
      if (this.customUserSelectRange.length > 2) {
        this.isActiveBtn = false;
        this.customUserSelectRange = [];
        this.selectedRangeDay = [];
      }
    },
    showCustomRange(day) {
      return this.customUserSelectRange.includes(new Date(this.year, this.month, day).getTime());
    },
  },
  mounted() {
    document.addEventListener('click', (event) => {
      if (event.target === this.$refs['popup-box']) {
        this.closeCalendar();
      }
    });
    this.selectedRangeDay.push(
      new Date(
        new Date().getFullYear(), new Date().getMonth(), new Date().getDate(),
      )
        .getTime(),
    );
  },
};
</script>

<style lang="scss">
  $calendarShadow: 0px 10px 40px rgba(128, 158, 191, 0.2);
  $radiusCalendar:  10px;
  $heightCalendar: 300px;
  $colorWhite: #fff;
  $colorBlack: #000;
  $borderBlack: 2px solid #000;
  $bgCalendar: #F3F8FD;
  $sizeHoverDay: 28px;
  $radiusBorder: 50%;

  .popup-box {
    z-index: 999;
    position: fixed;
    left: 0;
    top: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
    background: rgba(240, 246, 252, 0.7);
    backdrop-filter: blur(4px);
  }

  .calendar {
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    background-color: $colorWhite;
    box-shadow: $calendarShadow;
    border-radius: $radiusCalendar;

    &__month {
      display: grid;
      align-items: center;
      grid-template-columns: 25px 1fr 25px;
      margin: 19px 15px 16px;
    }

    &__btn-prev {
      transform: rotate(-45deg);
    }

    &__btn-next {
      transform: rotate(135deg);
    }

    &__days {
      display: grid;
      padding-bottom: 15px;

      background-color: $bgCalendar;
    }

    &__day-of-week,
    &__week {
      display: grid;
      justify-items: center;
      grid-template-columns: repeat(7, 1fr);
      grid-auto-rows: 28px;
      padding: 0 14px;
    }

    &__day-of-week {
      padding-top: 17px;
      font-weight: bold;
    }

    &__day {
      cursor: pointer;
      display: flex;
      justify-content: center;
      align-items: center;
      text-align: center;

        &:hover {
          width: $sizeHoverDay;
          height: $sizeHoverDay;
          border-radius: $radiusBorder;

          background-color: #DFE9F3;
        }
    }

    &__control {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      grid-template-rows: 45px;
      grid-column-gap: 7px;
      padding: 10px 11px;
    }

    &__cancel {
      border: $borderBlack;
      box-sizing: border-box;
      border-radius: 7px;
      transition: all 0.3s ease;

      &:hover {
        color: $colorWhite;
        background-color: $colorBlack;
      }
    }

    &__update {
      background: rgba(255, 116, 57, 0.5);
      border-radius: 7px;
    }
  }

  .btn-calendar {
    position: relative;
    width: 23px;
    height: 23px;
    border-radius: $radiusBorder;
    border: $borderBlack;

    &::before {
      content: '';
      display: block;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 7px;
      height: 7px;
      border-top: $borderBlack;
      border-left: $borderBlack;
    }
  }

  .filter-days {
    display: grid;
    grid-auto-rows:39px;
    padding: 10px;

    background-color: $colorWhite;
    box-shadow: $calendarShadow;
    border-radius: $radiusCalendar;

    &__btn {
      width: 156px;

      background-color: transparent;

      &:hover {
        border: 2px solid #EBEEF3;
        box-sizing: border-box;
        border-radius: 5px;
      }
    }
  }

  .container {
    display: grid;
    grid-template-columns: 176px 288px;
    grid-column-gap: 8px;
    justify-content: center;
    height: auto;
  }

  .active{
    background: #F0F3F8;
    border-radius: 5px;
  }

  .select-day {
    width: 100%;
    background-color:rgba(255, 116, 57, 0.2);

    &__first-last {
      width: 28px;
      border-radius: $radiusBorder;
      background-color: #FF7439;
    }
  }

  .update {
    background-color: #FF7439;
  }
</style>
