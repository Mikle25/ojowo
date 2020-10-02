<template>
  <section class="header">
    <div>
      <img src="../assets/image/logo.svg" alt="Ojowo" class="header__logo">
      <span>beta</span>
    </div>
    <div class="header__admin-panel">
      <button class="header__notification">
        <img src="../assets/image/notification.svg" alt="notification">
      </button>
      <div class="header__admin">
        <label for="admin"></label>
        <select name="admin" id="admin" >
          <option value="artem">Артем</option>
        </select>
      </div>
      <button type="text" class="header__search">
        <img src="../assets/image/search.svg" alt="search">
      </button>

      <div class="header__lang">
        <label for="language"></label>
        <select name="language" id="">
          <option value="ru">Ru</option>
          <option value="en">En</option>
        </select>
      </div>

    </div>
  </section>
</template>

<script>
export default {

};
</script>

<style lang="scss" scoped>
$sizeControl: 43px;
$bgColorBtn: #fff;
$bgColorHeaderBtn: rgba(203, 215, 228, 0.4);
$boxShadow: 0px 10px 40px rgba(213, 221, 230, 0.6);
$radiusBtn: 50%;
$sizeArrow: 8px;
$border: 2px solid #000;

select {
  appearance: none;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;

  &__logo {
    margin-right: 9px;
  }

  &__admin-panel {
    display: grid;
    grid-template-columns: repeat(4, min-content);
    grid-column-gap: 20px;
    justify-content: center;
    align-content: center;
  }

  &__notification {
    width: $sizeControl;
    height: $sizeControl;
    border-radius: $radiusBtn;
    background-color: $bgColorBtn;
    box-shadow: $boxShadow;
  }

  &__admin {
    position: relative;
    width: 120px;
    height: $sizeControl;
    border-radius: $sizeControl;
    background-color: $bgColorBtn;
    box-shadow: $boxShadow;

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

    & select {
      height: 100%;
      width: 100%;

      background-color: transparent;
      border-radius: $radiusBtn;
    }
  }

  &__search {
    width: $sizeControl;
    height: $sizeControl;
    border-radius: $radiusBtn;
    background-color:$bgColorHeaderBtn;
  }

  &__lang {
    position: relative;
    width: 64px;
    height: $sizeControl;
    border-radius: $sizeControl;
    background-color:$bgColorHeaderBtn;

    & label {
      cursor: pointer;
      position: absolute;
      right: 5%;
      top: 50%;
      width: $sizeArrow;
      height: $sizeArrow;

      border-top: $border;
      border-right: $border;
      transform: translate(-100%, -80%) rotate(135deg);
    }

    & select {
      position: relative;
      left: -5px;
      height: 100%;
      width: 100%;
      background-color: transparent;

      border-radius: $radiusBtn;
    }
  }
}
</style>
