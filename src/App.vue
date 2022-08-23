<template>
<div class="grid-container">
      <header>
        <h1>Pineapple Pizza</h1>
      </header>
      <nav></nav>
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

        <img src="https://i.pinimg.com/474x/2b/e3/ac/2be3acf14297100ea06ca2e1ec5c1443.jpg" />
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Et voluptas
        </p>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Et voluptas

        </p>
      </main>
      <aside>
      </aside>
      <footer>
        <p>Formative by Lingyi, Grace, Darlene, Jannah</p>
      </footer>
    </div>


</template>

<style >

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

