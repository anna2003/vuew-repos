<template>
  <div class="container column">
    <app-form @add-item="addItem"></app-form>
    <app-resume :items="items"></app-resume>
  </div>
  <div class="container">
    <app-comments
      :comments="comments"
      @load-comments="loadComments"
    ></app-comments>
    <app-loading v-if="isLoading"></app-loading>
  </div>
</template>

<script>
import AppForm from "./components/AppForm";
import AppResume from "./components/AppResume";
import AppLoading from "./components/AppLoading";
import AppComments from "./components/AppComments";

export default {
  components: {
    AppForm,
    AppResume,
    AppLoading,
    AppComments,
  },
  data() {
    return {
      items: [],
      comments: [],
      isLoading: false,
      path: "https://vue-resume-d5aa9-default-rtdb.firebaseio.com/resumes.json",
    };
  },
  mounted() {
    this.loadResumes();
  },
  methods: {
    async loadResumes() {
      this.isLoading = true;
      try {
        const response = await fetch(this.path);
        const data = await response.json();
        if(!data){
          throw new Error('Данных пока нет...')
        }
        this.items = Object.keys(data).map(key => ({
          id: key,
          ...data[key],
        }));
      } catch(e) {
        console.log(e.message)
      }
      this.isLoading = false;
    },
    async addItem(item) {
      const response = await fetch("https://vue-resume-d5aa9-default-rtdb.firebaseio.com/resumes.json", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(item),
      });
      const res = response.json();
      this.items.push(item);
    },

    async loadComments() {
      this.isLoading = true;
      const response = await fetch(
        "https://jsonplaceholder.typicode.com/comments?_limit=42"
      );
      this.comments = await response.json();
      this.isLoading = false;
    },
  },
};
</script>
