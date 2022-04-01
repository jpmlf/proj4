<template>
<div class="home">
    <div class="heading">
      <div class="circle">1</div>
      <h2>Add an Opinion <router-link to="/post">here</router-link></h2>
    </div>
    <div class="heading">
      <div class="circle">2</div>
      <h2>Rate & Comment other opinions</h2>
    </div>
  <section class="image-gallery">
    <div class="image" v-for="item in items" :key="item.id">
      <img :src="item.path" />
      <h1>{{item.title}}</h1>
      <h2>{{item.textarea}}</h2>

      <star-rating v-bind:increment="0.5" :rating="item.rating" @rating-selected ="editRating($event, item)"></star-rating>
      <div v-if="item.numratings > 0" :key="rates">
      <p>Avg Rating: {{item.rating}}</p>
      <p>Number of Ratings : {{item.numratings}}</p>
      </div>

      <h3>Add a Comment</h3>
      <form @submit.prevent="addComment(item)">
        <input type="text" v-model="addedComment">
        <button type="round">Add</button>
      </form>
      <h3>Comments</h3>
      <div v-for="comment in item.comments" :key="comment.id">
        <hr>
        <p><em>"{{comment}}"</em></p>
      </div>
    </div>
  </section>
</div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios';
import StarRating from 'vue-star-rating'
export default {
  name: 'Home',
  data() {
    return {
     items: [],
     addedComment: '',
    }
  },
  components: {
    StarRating
  },
  created() {
    this.getItems();
  },
  methods: {
    async getItems() {
      try {
        let response = await axios.get("/api/items");
        this.items = response.data;
        return true;
      } catch (error) {
        console.log(error);
      }
    },
    async editRating(rating, item) {
      try {
        await axios.put("/api/rate/" + item._id, {
          rating: rating,
        });
        this.getItems();
      } catch (error) {
        console.log(error);
      }
    },
    async addComment(item) {
      try {
        await axios.put("/api/comment/" + item._id, {
          comment: this.addedComment,
        });
        this.getItems();
      } catch (error) {
        console.log(error);
      }
    },
  }
}
</script>

<style scoped>
.image h2 {
  font-style: italic;
}
.image h3 {
  font-style: italic;
}

/* Masonry */
*,
*:before,
*:after {
  box-sizing: inherit;
}

.image-gallery {
  column-gap: 1.5em;
}

.image {
  margin: 0 0 1.5em;
  display: inline-block;
  width: 100%;
  border-radius: 25px;
  border: 2px solid #211A1D;
  padding: 20px;
}

.image img {
  width: 70%;
  height: 70%;
  border-radius: 25px;
}

/* Masonry on large screens */
@media only screen and (min-width: 1024px) {
  .image-gallery {
    column-count: 3;
  }
}

/* Masonry on medium-sized screens */
@media only screen and (max-width: 1023px) and (min-width: 768px) {
  .image-gallery {
    column-count: 2;
  }
}

/* Masonry on small screens */
@media only screen and (max-width: 767px) and (min-width: 540px) {
  .image-gallery {
    column-count: 1;
  }
}

.heading {
  display: flex;
  margin-bottom: 20px;
  margin-top: 20px;
}

.heading h2 {
  margin-top: 8px;
  margin-left: 10px;
}

.add,
.edit {
  display: flex;
}

.circle {
  border-radius: 50%;
  width: 18px;
  height: 18px;
  padding: 8px;
  background: #333;
  color: #fff;
  text-align: center
}
</style>