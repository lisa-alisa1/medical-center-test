<template>
    <div class="sidebar">
        <nav>
            <ul>
                <li v-for="li in navList" :key="li.title">
                    <img :src="`../src/assets/img/${li.icon}.svg`">
                    <p>{{ li.title }}</p>
                </li>
            </ul>
        </nav>
        <div class="sidebar__exit">
            <hr>
            <div>
                <img src="../assets/img/exit.svg">
                <p>Вийти</p> 
            </div>
        </div>
    </div>
</template>


<script>
export default {
    data() {
        return {
            navList: [
                {
                    icon: 'nav-icon-scan',
                    title: 'Сканер'
                },
                {
                    icon: 'nav-icon-coworkers',
                    title: 'Співробітники   '
                },
                {
                    icon: 'nav-icon-clients',
                    title: 'Клієнти'
                },
                {
                    icon: 'nav-icon-exersices',
                    title: 'Вправи'
                },
                {
                    icon: 'nav-icon-banners',
                    title: 'Банери'
                },
                
            ]
        }
    }
}
</script>


<style lang="scss" scoped>
@import '../assets/scss/mixins';
@import '../assets/scss/variables';

.sidebar {
    @include white-container;
    width: 295px;
    height: 683px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    font-size: 16px;
    color: $neutral-500;

    nav {
        ul li {
            display: flex;
            align-items: center;
            margin-bottom: 20px;

            img {
                margin-right: 15px;
            }
        }
    }

    &__exit {
        display: flex;
        align-items: start;
        flex-direction: column;

        hr {
            width: 100%;
            margin-bottom: 15px;
            border-top: 1px solid $neutral-500;
        }

        img {
            margin-right: 15px;
        }

        div {
            display: flex;
            align-items: center;
        }
    }
}

@media(max-width: 950px) {
    .sidebar {
        width: 30%;

        nav ul li {
            display: flex;
            justify-content: center;

            img {
                margin: 0;
            }
            p {
                display: none;
            }
        } 

        &__exit {
            p {
                display: none
            }
            img {
                margin: 0;
            }
        }
    }
}

@media(max-width: 780px) {
    .sidebar {
        display: none;
    }
}

@media(max-width: 500px) {
    .sidebar {
        justify-content: normal;
        flex-direction: row;
        height: 70px;

        &__exit {
            hr {
                display: none;
            }

            img {
                width: 30px;
                height: 30px;
            }

            div {
                display: flex;
                flex-direction: column;
                margin-left: 15px;

                p {
                    display: block;
                    font-size: 13px;
                }
            }
        }
        nav {
            width: 100%;

            ul {
                display: flex;
                justify-content: space-between;
                align-items: center;

                li {
                    display: flex;
                    flex-direction: column;
                    overflow: hidden;
                    text-overflow: ellipsis; 
                    white-space: nowrap;
                    width: 50px;
                    margin: 0;

                    p {
                        display: block;
                        font-size: 13px;
                    }

                    img {
                        width: 30px;
                        height: 30px;
                    }
                } 
            }
        } 
    }
}
</style>