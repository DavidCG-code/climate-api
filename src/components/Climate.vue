<template>
  <input
    type="text"
    @keyup.enter="fetchData()"
    v-model="city"
    placeholder="london  york,us  york,uk"
  />

  <div v-if="show" class="card">
    <div class="card__fav">
      <div @click="addFav">
        <img src="../assets/images/star.svg" width="20" height="20" alt="" />
      </div>
    </div>
    <div class="card__date">
      <p>{{ year }}, {{ month }}, {{ day }}</p>
    </div>
    <div class="card__image">
      <img
        :src="
          'http://openweathermap.org/img/wn/' +
            climate.weather[0].icon +
            '@2x.png'
        "
        width="120"
        height="120"
        alt=""
      />
      <p class="card__image__name">{{ climate.name }}</p>
    </div>
    <div class="card__temp">
      <p>{{ Math.round(climate.main.temp) }}º</p>
    </div>
    <div class="card__climate">
      <p>{{ climate.weather[0].description }}</p>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "HelloWorld",
  setup() {
    const city = ref("");
    const climate = ref("");
    const show = ref(false);
    const favorites = ref([]);

    const day = ref("");
    const month = ref("");
    const year = ref("");

    async function fetchData() {
      var response = await fetch(
        `https://api.openweathermap.org/data/2.5/weather?q=${city.value}&appid=aa4c034221d84ee77dc77170a0a3703a&units=metric`
      );
      var json = await response.json();

      climate.value = json;
      console.log(json);

      show.value = true;
      city.value = "";
    }

    function dateToday() {
      var date = new Date();
      day.value = date.getUTCDate();
      month.value = date.getUTCMonth() + 1;
      year.value = date.getUTCFullYear();
    }

    dateToday();

    function addFav() {
      favorites.value.push({
        date: {
          year: year.value,
          month: month.value,
          day: day.value
        },
        image: climate.value.weather[0].icon,
        name: climate.value.name,
        temp: climate.value.temp,
        climate: climate.value.weather[0].description
      });

      console.log(favorites.value);
    }

    return {
      fetchData,
      climate,
      city,
      show,
      dateToday,
      day,
      month,
      year,
      addFav,
      favorites
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
input {
  grid-area: 2/2/3/6;
}
.card {
  grid-area: 3/2/4/6;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  height: 20rem;
  border-radius: 20px;
  box-shadow: 0px 3px 12px #e0e0e079;
  padding: 1rem;
  background-color: rgba(#fff, 0.5);
  &__image,
  &__date {
    flex-basis: 100%;
  }
  &__temp,
  &__climate {
    font-size: $font-md-2;
    font-family: "Roboto", sans-serif;
    font-style: italic;
    font-weight: 700;
  }
  &__fav {
    flex-basis: 100%;
    display: flex;
    justify-content: flex-end;
    cursor: pointer;
  }
  &__date {
    font-family: "Roboto", sans-serif;
    font-weight: 300;
  }
  &__image {
    &__name {
      font-size: $font-md-1;
      text-transform: capitalize;
    }
  }
  &__temp {
    flex-basis: 35%;
  }
  &__climate {
    flex-basis: 65%;
    text-transform: capitalize;
  }
}
</style>
