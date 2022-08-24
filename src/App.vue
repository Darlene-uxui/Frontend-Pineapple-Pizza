<template>
    <div class="grid-container">
      <header>
          <h1>Pineapple Pizza</h1>
      </header>
      <nav>
        <h3>Meme Collection</h3>
        <img src="https://i.pinimg.com/736x/2b/e3/ac/2be3acf14297100ea06ca2e1ec5c1443.jpg">
        <img src="https://i.pinimg.com/originals/8c/7f/e6/8c7fe66812fdc1c0d63d2869a6067cf1.jpg" alt="">
        <img src="https://sayingimages.com/wp-content/uploads/ordered-pizza-with-pineapple-meme.jpg" alt="">
      </nav>
      <main>
        <h2>Upload Your Pizza</h2>
      <form>
        <div class="form-group">
            <label for="title">title</label>
            <input type="text" v-model="title" id="title">
        </div>
        <div class="form-group">
            <label for="description">description</label>
            <input type="text" v-model="description" id="description">
        </div>
        <div class="form-group">
            <label for="nickName">nickName</label>
            <input type="text" v-model="nickname" id="nickName">
        </div>
        <div class="form-group">
            <label for="imageURL">image URL</label>
            <input type="url" v-model="imageurl" id="imageURL">
        </div>
        <button @click="submitForm" type="button">Create my Pizza</button>
      </form>
      <h2>Uploaded Pizza</h2>
          <PizzaListItem @delete-pizza="deletePizza" v-for="pizza of pizzasArray" :key="pizza.id" :pizza-data="pizza" />
      </main>
      <aside>
        <h3>Meme Collection</h3>
        <img src="https://i.kym-cdn.com/photos/images/newsfeed/001/217/804/4d8.png">
        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ1-71_bQBedd1cGLMc0dCRdnRs2wO1_HncejxsOTS7nkP8B2ociGne8WQFcMV6kRbnTwI&usqp=CAU" alt="">
        <img src="https://hips.hearstapps.com/hmg-prod.s3.amazonaws.com/images/kiwi-pineapple-1579003090.jpg" alt="">
      </aside>
      <footer>
        <p>Formative by Lingyi, Grace, Darlene, Jannah</p>
      </footer>
    </div>


</template>

<style >


  input {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  }
</style>

<script>
import PizzaListItem from './components/PizzaListItem.vue';

  export default {
    components: {PizzaListItem},
    data() {
      return {
        title: null,
        description: null,
        nickname: null,
        imageurl: null,
        pizzasArray: [],
      };
    },
    methods: {
      async submitForm() {
        console.log("submit form");
        const response = await fetch("http://localhost:3000/pizza", {
          method: "POST",
          headers: { "content-type":"application/json" },
          body: JSON.stringify({
            title: this.title,
            description: this.description,
            nickname: this.nickname,
            imageurl: this.imageurl
          })
        });
        const data = await response.text();
        console.log(data);
        this.getPizzas();
      },

      async getPizzas() {
        const response = await fetch("http://localhost:3000/pizza");
        const data = await response.json();
        this.pizzasArray = data;
      },
      
      async deletePizza(id) {
        const response = await fetch(`http://localhost:3000/pizza/${id}`, {
        method: "DELETE"
        });
        const data = await response.text();

        this.getPizzas();
        }
    },
    mounted() {
      this.getPizzas();
    }
  }
</script>

