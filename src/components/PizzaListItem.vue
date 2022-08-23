<template>
    <div class="pizza">
        <div class="pizza-box">
            <p class="title">Title:{{ pizzaData.title }}</p>
            <p class="description">Description:{{ pizzaData.description }}</p>
            <p class="nickName">Nick Name:{{ pizzaData.nickname }}</p>
            <img class="image" :src="pizzaData.imageurl" alt="pizza image" />
        </div>
    </div>
            <button class="delete-btn" @click="$emit('deletePizza', pizzaData.id)" type="button">Clear</button>
</template>

<script>
    export default {
        props: {
            pizzaData: Object,
        },
        data() {
            return {
                title: this.pizzaData.title,
                description: this.pizzaData.description,
                nickname: this.pizzaData.nickname,
                imageurl: this.pizzaData.imageurl
            }
        }
    }
</script>

<style scoped>

.image {
    height: 200px;
    width: 300px;
}
</style>