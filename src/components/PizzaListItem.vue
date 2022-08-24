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
</template>

<script>
    import axios from 'axios'
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
        },
        methods: {
            getPizza () {
                axios.get('URL HERE')
                    .then((response) => {
                        console.log(response.data)
                        this.pizza = response.data
                    })
                    .catch(error => {
                        console.log(error   )
                    })
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