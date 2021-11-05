<template>
  <div id="CatApp">
    <div class="d-flex flex-column flex-wrap">
      <h1 class="mainTitle">Random Gif Cat</h1>
    </div>
    <div class="container_dad">
      <div class="container">
    <div class="container d-flex flex-column">
      <div class="d-flex justify-content-center my-3">
        <p class="mx-3 fw-bold">Título</p>
        <input
          class="catInput"
          v-model="catTitle"
          placeholder="Ingresa tu título"
        />
      </div>
      <div class="d-flex justify-content-center my-3">
        <p class="mx-3 fw-bold">Filtro</p>
        <select class="catInput" v-model="catFilter">
          <option v-for="(filter, index) in filters" :key="index">
            {{ filter }}
          </option>
        </select>
      </div>
      <div class="d-flex justify-content-center my-3">
        <p class="mx-3 ps-5 fw-bold">Color</p>
        <select class="catInput" v-model="catColor">
          <option v-for="(color, index) in colors" :key="index">
            {{ color }}
          </option>
        </select>
        <div class="circulito ms-3 my-1" :style="{ 'background-color': catColor }"></div>
      </div>
      <div class="d-flex justify-content-center my-3">
        <p class="mx-2 fw-bold">Tamaño</p>
        <input
          class="catInput"
          v-model.number="catSize"
          placeholder="Ingrese número"
        />
      </div>
      <button
        class="catBtn mx-auto my-3"
        type="button"
        @click="lookForCat()"
      >
        Obtener mi gatito
      </button>
      <img class="mx-auto my-2" id="catImg" :src="catImg" />
    </div>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CatApp",
  data: () => ({
    catImg: "",
    catFilter: "",
    filters: ["blur", "mono", "sepia", "negative", "paint", "pixel"],
    catColor: "",
    colors: ["Red", "Blue", "Green", "Yellow", "Purple"],
    catTitle: "",
    catSize: "",
  }),

  methods: {
    lookForCat() {
      fetch(
        `https://cataas.com/cat/gif//says/${this.catTitle}?size=${this.catSize}&color=${this.catColor}&filter=${this.catFilter}`
      )
        .then((res) => res.blob())
        .then((blob) => {
          let catUrl = URL.createObjectURL(blob);
          this.catImg = catUrl;
        });
    },
  },
};
</script>

<style>
#CatApp {
  margin: auto;
  background-color: rgb(170, 212, 212);
  width: 1350px;
  height: 800px;
}
.gatitoPrincipal {
  width: 300px;
  margin-left: auto;
  margin-right: auto;
  border: dashed black 10px;
}
.mainTitle {
  text-align: center;
}

.catBtn {
  width: 200px;
  text-align: center;
}

.catInput {
  width: 250px;
}

.container_dad {
  width: 1350px;
  background-color: rgb(219, 130, 148);
}
.container {
  width: 250px;
  margin-top: 40px;
  margin-left: 570px;
}

.circulito {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  display: inline-block;
}
</style>
