
<script setup>
import { ref, onMounted } from 'vue';
const yandex = ref('')
const yandexSuggestArray = ref([])
function yandexInit() {
  window.ymaps.ready();
}
onMounted(() => {
  // не обязательно, но в доке описано
  window.ymaps.ready(function () {
    var myMap = new ymaps.Map("YMapsID", {
      center: [55.76, 37.64],
      zoom: 10
    });
  });
  yandexInit()
})
function yandexSuggest(text) {
  // query параметры
  let options = {
    // boundedBy: '',
    // provider: '',
    results: 20
  }
  window.ymaps.suggest(text, options).then(function (items) {
    yandexSuggestArray.value = items
  });
}
</script>



<template>
  <div>
    <div>
      <div v-for="(item, index) in yandexSuggestArray" :key="index">
        {{ item.displayName }}
        ==========
        {{ item.value }}
      </div>
    </div>
    asdadasdasdas
    <input type="text" v-model="yandex" @input="yandexSuggest(yandex)"><button @click="yandex = ''">clear</button>
    <br>
    <br>
    <br>
    <br>
    <div id="YMapsID" style="width: 450px; height: 350px;"></div>
  </div>
</template>
