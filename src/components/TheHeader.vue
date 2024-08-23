<template>
    <header class="header">
        <div class="header__logo">
            <img src="../assets/img/logo.svg" alt="">
        </div>
        <div class="header__account">
            Привіт, Адмін
            <img src="../assets/img/user-icon.svg" alt="">
        </div>
    </header>
</template>


<style lang="scss" scoped>
@import '../assets/scss/variables';

.header {
   width: 100%;
   height: 60px;
   background-color: $neutral-100;
   display: flex;
   justify-content: space-between;
   align-items: center;
   padding: 0 30px;
   box-sizing: border-box;
   border-radius: 0 0 10px 10px;

   div {
    display: flex;
    align-items: center;
   }

   &__account img {
        margin-left: 15px;
   }
}

@media(max-width: 500px) {
    .header {
        padding: 0 15px;

        &__account {
            font-size: 14px;
        }
    }
}
</style>