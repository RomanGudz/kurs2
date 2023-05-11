<template>
  <div class="container column">
    <form class="card card-w30" @submit.prevent="submitForm">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select id="type" v-model="type">
          <option value="title">Заголовок</option>
          <option value="subtitle">Подзаголовок</option>
          <option value="avatar">Аватар</option>
          <option value="text">Текст</option>
        </select>
      </div>

      <app-input v-model:inputModel="textvalue"></app-input>

      <button type="submit" class="btn primary" :disabled="inputValid">
        Добавить
      </button>
    </form>

    <app-resume :resume="resume"></app-resume>
  </div>
  <div class="container">
    <app-load-button v-show="btnload" @click="loadComent"></app-load-button>

    <app-loader v-if="load"></app-loader>

    <div class="card" v-show="!btnload">
      <app-list-commetn :coments="coment"></app-list-commetn>
    </div>
  </div>
</template>

<script>
import AppResume from "./components/AppResume.vue";
import AppInput from "./components/AppInput.vue";
import AppLoadButton from "./components/AppLoadButton.vue";
import AppLoader from "./components/AppLoader.vue";
import AppListCommetn from "./components/AppListCommetn.vue";
import axios from "axios";

export default {
  data() {
    return {
      load: false,
      type: "title",
      textvalue: "",
      resume: [],
      coment: [],
      btnload: true,
    };
  },
  mounted() {
    this.loadResume();
  },
  computed: {
    inputValid() {
      return this.textvalue.length <= 3;
    },
  },
  methods: {
    async submitForm() {
      if (this.type === "title") {
        const response = await fetch(
          "https://vue-http-da77f-default-rtdb.europe-west1.firebasedatabase.app/resume.json",
          {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify({
              resumeTitle: this.textvalue,
            }),
          }
        );
        const firebasedatabase = await response.json();
        this.resume.puch({
          resumeTitle: this.textvalue,
          id: firebasedatabase.textvalue,
        });
        this.textvalue = "";
      } else if (this.type === "subtitle") {
        await fetch(
          "https://vue-http-da77f-default-rtdb.europe-west1.firebasedatabase.app/resume.json",
          {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify({
              resumeTitleTwo: this.textvalue,
            }),
          }
        );
        this.textvalue = "";
        this.type = "title";
      } else if (this.type === "avatar") {
        await fetch(
          "https://vue-http-da77f-default-rtdb.europe-west1.firebasedatabase.app/resume.json",
          {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify({
              resumeAvatar: this.textvalue,
            }),
          }
        );
        this.textvalue = "";
        this.type = "title";
      } else if (this.type === "text") {
        await fetch(
          "https://vue-http-da77f-default-rtdb.europe-west1.firebasedatabase.app/resume.json",
          {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify({
              resumeText: this.textvalue,
            }),
          }
        );
        this.textvalue = "";
        this.type = "title";
      }
    },
    async loadResume() {
      try {
        const { data } = await axios.get(
          "https://vue-http-da77f-default-rtdb.europe-west1.firebasedatabase.app/resume.json"
        );
        this.resume = Object.keys(data).map((key) => {
          return {
            id: key,
            ...data[key],
          };
        });
      } catch (e) {
        console.log(e);
      }
    },
    loadComent() {
      this.load = true;
      setTimeout(async () => {
        try {
          const { data } = await axios.get(
            "https://jsonplaceholder.typicode.com/comments?_limit=42"
          );
          this.coment = Object.keys(data).map((key) => {
            return {
              id: key,
              ...data[key],
            };
          });
          this.btnload = false;
          this.load = false;
        } catch (e) {
          console.log(e.mesaage);
          this.load = true;
        }
      }, 500);
    },
  },
  components: {
    AppInput,
    AppResume,
    AppLoadButton,
    AppLoader,
    AppListCommetn,
  },
};
</script>

<style>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
