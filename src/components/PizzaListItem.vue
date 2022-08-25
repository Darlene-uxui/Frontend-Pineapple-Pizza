<template>
    <div class="pizza">
        <div class="pizza-box">
            <p class="title"><b>Title:</b>{{ pizzaData.title }}</p>
            <p class="description"><b>Description:</b>{{ pizzaData.description }}</p>
            <p class="nickName"><b>Nick Name:</b>{{ pizzaData.nickname }}</p>
            <img class="image" :src="pizzaData.imageurl" alt="pizza image" />
        </div>
    </div>
    <button class="delete-btn" @click="$emit('deletePizza', pizzaData.id)" type="button">Delete</button>
    <button @click="openModal">Edit</button>
    <popup v-if="showModal">
        <div class="popup-box">
            <p class="popup-title"><b>Title:</b></p>
            <input v-model="newPizzaData.title" type="text" :placeholder="pizzaData.title">
            <p class="popup-description"><b>Description:</b></p>
            <input v-model="newPizzaData.description" type="text" :placeholder="pizzaData.description">
            <p class="popup-nickName"><b>Nick Name:</b>{{ pizzaData.nickname }}</p>
            <p class="popup-imgUrl"><b>ImageUrl:</b></p>
            <input v-model="newPizzaData.imageurl" type="url" :placeholder="pizzaData.imageurl">
        </div>
        <button @click="$emit('updatePizza', newPizzaData, pizzaData, openModal)">Update</button>
    </popup>
</template>

<script>
import popup from "./popup.vue"
export default {
    components: { popup },
    props: {
        pizzaData: Object,
    },
    data() {
        return {
            title: this.pizzaData.title,
            description: this.pizzaData.description,
            nickname: this.pizzaData.nickname,
            imageurl: this.pizzaData.imageurl,
            showModal: false,

            newPizzaData: {
                title: null,
                description: null,
                nickname: this.pizzaData.nickname,
                imageurl: null
            }
        }
    },
    methods: {
        openModal() {
            this.showModal = !this.showModal
        }
    }
}
</script>

<style scoped>
.pizza {
    border: 1px solid black;
    padding: 20px;
}

.image {
    height: 200px;
    width: 300px;
}
</style>