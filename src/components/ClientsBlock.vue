<template>
    <div class="manage-panel">
        <div class="manage-panel__clients-count">
            <p class="title"> клієнти</p> 
            <p class="count"> 
                {{ clientsList.length }} 
                чоловік
            </p>
        </div>
        <div class="manage-panel__search">
                <input  
                type="text" 
                placeholder="Пошук"
                v-model="inputValue"
                />
                <img src="../assets/img/search.svg">
        </div>
        
        <div class="manage-panel__select-categoty" @click="isOpen = !isOpen">
            Виберіть зі списку
            <img 
                src="../assets/img/dropdown-arrow.svg"  
                class="dropdown-button"
            >
            <ul class="dropdown-menu" :class="{active: isOpen}">
                <li 
                    v-for="category in getCategories"
                    :key="category"
                    @click="getSelectedCategory(category)"
                > 
                    {{category}} 
                </li>
            </ul>
        </div>
        
        <button class="manage-panel__btn" @click="addNewClient()">
            Додати 
            <img src="../assets/img/add.svg">
        </button>
    </div>

    <div class="clients-block">
        <div class="clients-block__head">
            <div> Ім’я/Нікнейм </div>
            <div> Категорія </div>
            <div> Телефон </div>
            <div> Дата оновлення </div>
        </div>

        <div class="clients-block__list">
            <div v-for="(client, index) in getFilteredList" class="client-info">
                <div class="client-name">
                    {{ client.name }}
                </div>
                <div class="client-category">
                    {{client.category}}
                </div>
                <div class="client-phone">
                    {{client.phone}}
                </div>
                <div class="client-lastUpdate">
                    {{client.lastUpdate}}
                </div>
                <img 
                    src="../assets/img/trash.svg" 
                    @click="deleteClient(index)"
                >
            </div>

            <div v-for="(client, index) in getFilteredList" class="mobile-client-info">
                <div class="client-name item">
                    <div> Ім’я/Нікнейм </div>
                    <p> {{ client.name }} </p>
                </div>
                <div class="client-category item">
                    <div> Категорія </div>
                    <p> {{ client.category }} </p>
                </div>
                <div class="client-phone item">
                    <div> Телефон: </div>
                    <p> {{ client.phone }} </p>
                </div>
                <div class="client-lastUpdate item">
                    <div> Дата оновлення </div>
                    <p> {{ client.lastUpdate }} </p>
                </div>
                <img 
                    class="img-item"
                    src="../assets/img/trash.svg" 
                    @click="deleteClient(index)"
                >
            </div>
            <div class="clients-block__isempty" v-if="!getFilteredList.length">
                <div> empty list </div>
            </div>
        </div>
    </div>
</template>


<script>
import { clients } from  '../../data/data';
    export default {
        data() {
            return {
                isOpen: false,
                clientsList: clients,
                inputValue: '',
                selectedCategory: ''
            }
        },

        computed: {
            getFilteredList() {
                let filteredList = this.clientsList;

                if (this.selectedCategory) {
                    filteredList = filteredList.filter(client => 
                        client.category === this.selectedCategory
                    );
                }

                if (this.inputValue) {
                    filteredList = filteredList.filter(item => 
                        item.name.toLowerCase().includes(this.inputValue.toLowerCase())
                    );
                }

                return filteredList;
            },

            getCategories() {
                return [...new Set(clients.map(client => client.category))];
            }
        },

        methods: {
            getSelectedCategory(category) {
                this.selectedCategory = category
                 console.log(this.selectedCategory);
            },

            deleteClient(index) {
                this.clientsList.splice(index, 1);
            },

            getRandomClient() {
                if (clients.length === 0) {
                    return {
                        name: "Михайло",
                        category: "категорія 1",
                        phone: "+380682821305",
                        lastUpdate: new Date().toLocaleString().slice(0, 17)
                    };
                }
                const randomIndex = Math.floor(Math.random() * clients.length);
                return clients[randomIndex];
            },

            addNewClient() {
                const randomClient = this.getRandomClient();
                this.clientsList.unshift({ 
                    ...randomClient, 
                    lastUpdate: new Date().toLocaleString().slice(0,17)
                });
            }
        }
    }
</script>


<style lang="scss" scoped>
@import '@/assets/scss/mixins';
@import '@/assets/scss/variables';

.manage-panel {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;

    &__clients-count {
        .title {
            text-transform: uppercase;
            font-size: 20px;
            font-family: OpenSans-Bold;
        }

        .count {
            font-size: 14px;
            font-family: OpenSans;
            color: $neutral-500;
        }
    }

    &__search {
        position: relative;

        input {
            background-color: $neutral-100;
            height: 45px;
            width: 229px;
            box-sizing: border-box;
            box-sizing: border-box;
            padding-left: 46px;
            outline: 0;
            border-radius: 5px;
            font-size: 16px;
        }

        input::placeholder {
            color: $neutral-400;
        }
    
        img {
            position: absolute;
            top: 50%; 
            left: 11px; 
            transform: translateY(-50%);
            width: 20px;
            height: 20px;
        }
    }

    &__select-categoty {
        position: relative;
        background-color: $neutral-100;
        width: 280px;
        box-sizing: border-box;
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 11px;
        border-radius: 5px;

        .dropdown-menu {
            display: none;
            width: 100%;
            top: 100%;
            left: 0;
            right: 0;
            position: absolute;
            background-color: $neutral-100;

            li {
                height: 3rem;
                display: flex;
                align-items: center;
                padding: 0 11px;
            }
            li:hover {
                background-color: $neutral-200;
            }
        }
        .active {
            display: block;
        }
    }
    
    &__btn {
        background: none;
        border: 1px solid $accent;
        color:$accent;
        border-radius: 50px;
        height: 45px;
        font-size: 16px;
        width: 220px;
        display: flex;
        align-items: center;
        justify-content: center;

        img {
            margin-left: 5px;
        }
    }
}

.clients-block {
    @include white-container;
    max-width: 925px;
    max-height: 973px;

    &__head {
        display: flex;
        justify-content: space-between;
        color: $neutral-400;
        font-size: 14px;
        font-family: OpenSans-SemiBold;
        margin-left: 20px;
        width: 93%;

        div {
            flex: 1;
        }
    }

    &__list {
        overflow-y: scroll;
        max-height: 895px;

        .client-info {
            width: 100%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 60px;
            padding: 20px;
            box-sizing: border-box;
            border: 1px solid $neutral-300;
            border-radius: 10px;
            margin-top: 20px;
           

            div {
                flex: 1;
            }
        }
        .mobile-client-info {
            display: none;
        }
    }

    &__list::-webkit-scrollbar {
        width: 1px;
    }

    &__isempty {
        display: flex;

        div {
            flex: 1;
        }
    }
}

@media (max-width: 1240px) {
    .manage-panel {
        &__select-categoty, &__search input  {
            width: 200px;
        }

        &__btn {
            width: 150px;
        }
    }
}

@media (max-width: 780px) {
    .manage-panel  {
        flex-direction: column;
        align-items: start;

        div, input {
            margin-bottom: 20px;
            width: 100%;
            height: 45px;
        }
    }
} 

@media(max-width: 500px) {
    .manage-panel {
        &__btn {
            width: 100%;

            .img {
                margin-left: 10px;
            }
        }
    }

    .clients-block {
        background: none;
        padding: 0;
        max-height: 100%;

        &__head {
            display: none;
        }

        &__list {
            padding-bottom: 100px;
            
            .client-info {
                display: none;
            }
            .mobile-client-info {
                display: block;
                background-color: $neutral-100;
                border-radius: 10px;
                font-size: 14px;
                padding: 20px 15px;
                margin-top: 15px;

                img {
                    margin-top: 2%;
                    margin-left: 94%;
                }
                .item {
                    display: flex;
                    justify-content: space-between;
                    align-items: center;
                    height: 50px;
                    border-bottom: 1px solid $neutral-200;

                    div {
                        flex: 1;
                        color: $neutral-400;
                    }
                    p {
                        flex: 1;
                        color: $neutral-600;
                    }
                }
            }
        }
    }
}
</style>