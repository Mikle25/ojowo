<template>
  <section class="navigation">
    <div class="navigation__level">
      <div class="navigation__select-level">
        <label for="lavel"></label>
        <select name="lavel" id="lavel" >
          <option value="expert">Эксперт</option>
        </select>
      </div>

      <div class="navigation__level-img">
        <img src="../assets/image/icon/expert.svg" alt="">
      </div>
    </div>
    <ul class="navigation__list">
      <li to="/About" class="navigation__item navigation__item--1">Аналитика</li>
      <li class="navigation__item navigation__item--2">Продукты</li>
      <li class="navigation__item navigation__item--3">Пользователь</li>
      <li class="navigation__item navigation__item--4">Конструктор сайта</li>
      <li class="navigation__item navigation__item--5">Трансляция</li>
      <li class="navigation__item navigation__item--6">Рассылка</li>
      <li class="navigation__item navigation__item--7">Маркетинг</li>
      <li class="navigation__item navigation__item--8">Платежи</li>
      <li class="navigation__item navigation__item--9">Настройки</li>
    </ul>
  </section>
</template>

<script>
export default {

};
</script>

<style lang="scss" scoped>
$sizeNavSelet: 54px;
$fontSizeNav: 15px;
$radiusLevel: 10px;
$colorWhite: #fff;
$sizeArrow: 8px;
$border: 2px solid #000;
$shadowLevel: 0px 10px 40px rgba(128, 158, 191, 0.2);
$positionCenterNav: translate(-50%, -50%);

  .navigation {
    display: grid;
    grid-template-columns: 177px;
    grid-template-rows: 54px 1fr;
    grid-row-gap: 11px;

  &__level {
    position: relative;
    z-index: 2;

    & select {
      width: 100%;
      height: 100%;
      appearance: none;
      background-color: transparent;
    }

    & label {
      cursor: pointer;
      position: absolute;
      right: 10%;
      top: 50%;
      width: $sizeArrow;
      height: $sizeArrow;

      border-top: $border;
      border-right: $border;
      transform: translate(-100%, -80%) rotate(135deg);
    }
  }

  &__select-level {
    width: 100%;
    height: $sizeNavSelet;
    border-radius: $radiusLevel;
    font-weight: bold;
    font-size: $fontSizeNav;
    background-color: $colorWhite;
    box-shadow: $shadowLevel;
  }

  &__level-img {
    z-index: -1;
    width: 50%;
    height: $sizeNavSelet;
    position: absolute;
    top: 50%;
    right: -50%;
    box-shadow: $shadowLevel;

    border-radius: $radiusLevel;
    transform: $positionCenterNav;
    background-color: $colorWhite;

    & img {
      position: absolute;
      top: 50%;
      right: 0;

      transform: $positionCenterNav;
    }
  }

  &__list {
    display: grid;
    grid-auto-rows: 85px;
    grid-auto-columns: 158px;
    grid-row-gap: 8px;
    justify-content: center;
    padding: 9px 0;

    border-radius: 6px;
    background-color: $colorWhite;
  }

  &__item {
    display: flex;
    align-items: flex-end;
    justify-content: center;
    padding-bottom: 11px;

    font-weight: bold;
    font-size: $fontSizeNav;

    border: 1px solid #E7ECF1;
    border-radius: 6px;

    &--1 {
      background: url("../assets/image/icon/analitic.svg") no-repeat 50% 20%;

    }
    &--2 {
      background: url("../assets/image/icon/product.svg") no-repeat 50% 20%;
    }
    &--3 {
      background: url("../assets/image/icon/users.svg") no-repeat 50% 20%;
      border: 1px solid #FF7439;
      color: #FF7439;
    }
    &--4 {
      background: url("../assets/image/icon/constructor.svg") no-repeat 50% 20%;
    }
    &--5 {
      background: url("../assets/image/icon/broadcast.svg") no-repeat 50% 20%;
    }
    &--6 {
      background: url("../assets/image/icon/mailing.svg") no-repeat 50% 20%;
    }
    &--7 {
      background: url("../assets/image/icon/marketing.svg") no-repeat 50% 20%;
    }
    &--8 {
      background: url("../assets/image/icon/payments.svg") no-repeat 50% 20%;
    }
    &--9 {
      background: url("../assets/image/icon/settings.svg") no-repeat 50% 20%;
    }
  }
}

</style>
