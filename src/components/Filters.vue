<template>
  <div class="box">
    <div class="filter">
      <ModalCalendar
        v-if="isActive"
        @closeCalendar="closeCalendar"
        @update="update"
      />

      <div class="filter__selected-filter">
        <div class="filter__calendar">
          <transition>
            <span class="icon"></span>
          </transition>
          <transition>
            <input
              type="button"
              id="calendar"
              :value="text"
              class="filter__calendar-btn"
              @click="showCalendar"
            />
            </transition>
            <transition>
              <label for="calendar" class="arrow"></label>
            </transition>
        </div>
        <div class="filter__filter-params">
          <span class="icon"></span>
          <select name="filter" class="filter__select-params" id="filetr">
            <option value="filter">Фильтр</option>
          </select>
          <label for="filter" class="arrow"></label>
        </div>
      </div>
      <div class="filter__control-btn">
        <button class="filter__unload">Выгрузить</button>
        <button class="filter__add-contact">Добавить контакт</button>
      </div>
    </div>
    <div class="range-days" v-if="toggleRangeText">
      <div class="range-days__text" >
        {{text}}
        <span class="range-days__btn" @click="hiddenRangeText"></span>
      </div>
    </div>
  </div>
</template>

<script>
import ModalCalendar from '@/components/ModalCalendar.vue';

export default {
  data() {
    return {
      isActive: false,
      text: 'За 1 день',
      toggleRangeText: false,
    };
  },
  components: {
    ModalCalendar,
  },
  methods: {
    showCalendar() {
      this.isActive = true;
    },
    closeCalendar() {
      this.isActive = false;
    },
    update(bool, text, rangeDay) {
      this.isActive = bool;
      this.text = text;
      this.toggleRangeText = true;

      this.$emit('filterList', rangeDay);
    },
    hiddenRangeText() {
      this.toggleRangeText = false;
      this.text = 'За 1 день';
    },
  },
};
</script>

<style lang="scss" scoped>
$sizeFilterBlock: 85px;
$radiusFilterBtn: 7px;
$sizeArrow: 8px;
$positionIcon: 50% 50%;
$colorWhite: #fff;
$radiusRangeDays: 41px;
$sizeBtn: 27px;
$positionCenter: 50%;
$border: 2px solid #000;
$rotateBtn: 45deg;

button {
  font-size: 14px;
  font-weight: bold;
}

select {
  appearance: none;
}

.box {
  display: grid;
  grid-auto-rows: auto;
  padding: 0 21px 0 35px;
  width: 100%;

  background-color: $colorWhite;
  border-radius: 10px;
}

.range-days {
  border-top: 2px solid #E7ECF1;
  padding: 10px 0;

  &__text {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 223px;
    height: $radiusRangeDays;

    color: $colorWhite;
    background: #586375;
    border-radius: $radiusRangeDays;
  }

  &__btn {
      cursor: pointer;
      position: absolute;
      right: 10px;
      width: $sizeBtn;
      height: $sizeBtn;
      border-radius: 50%;
      background-color: #677489;
      transition: all 0.3s ease;

      &::before,
      &::after {
        content: '';
        position: absolute;
        left: $positionCenter;
        top: $positionCenter;
        width: 8px;
        height: 2px;

        background-color: #464F5E;
      }

      &::before {
        transform: translate(-$positionCenter, -$positionCenter) rotate($rotateBtn);
      }

      &::after {
        transform: translate(-$positionCenter, -$positionCenter) rotate(-$rotateBtn);
      }

      &:hover {
        transform: scale(1.2);
      }
    }
}

  .filter {
    width: 100%;
    height: $sizeFilterBlock;
    display: flex;
    justify-content: space-between;
    align-items: center;

  &__selected-filter {
    display: grid;
    grid-template-columns: repeat(2, auto);
    grid-template-rows: auto;
    grid-column-gap: 44px;
  }

  &__calendar,
  &__filter-params {
    display: grid;
    grid-template-columns: 50px 1fr 50px;
    position: relative;
    justify-items: center;
  }

  &__calendar {
    & .icon {
      width: 50px;
      height: 23px;
      background: url('../assets/image/icon/calendar.svg') no-repeat $positionIcon;
      transition: all 0.3s ease;
    }

    &:hover .icon {
      background: url('../assets/image/icon/calendar-active.svg') no-repeat $positionIcon;
    }

    & .arrow{
      transition: all 0.3s ease;
    }

    &:hover .arrow{
      border-color: #FF7439;
      transform: rotate(-45deg);
    }

    &:hover .filter__calendar-btn {
      color:#FF7439;
    }
  }

  &__calendar-btn {
    font-size: 15px;
    text-align-last: left;
    background-color: $colorWhite;
    transition: all 0.3s ease;
  }

  &__filter-params {
    & .icon {
      width: 23px;
      height: 23px;
      background: url('../assets/image/icon/filter.svg') no-repeat $positionIcon;
    }
  }

  &__select-params {
    font-size: 15px;
    background-color: $colorWhite;
  }

  &__control-btn {
    display: grid;
    grid-template-columns: 120px 199px;
    grid-template-rows: 45px;
    grid-column-gap: 11px;
  }

  &__unload {
    border: $border;
    border-radius: $radiusFilterBtn;

    background-color: transparent;
  }

  &__add-contact {
    color: $colorWhite;
    background: #FF7439;
    border-radius: $radiusFilterBtn;
  }
}

.arrow {
  cursor: pointer;
  position: relative;
  align-self: center;
  width: $sizeArrow;
  height: $sizeArrow;

  border-top: $border;
  border-right: $border;
  transform: rotate(135deg);
}
</style>
