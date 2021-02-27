<template>
  <div class="home">
    <Climate />
  </div>
</template>

<script>
// @ is an alias to /src
import Climate from "@/components/Climate.vue";

export default {
  name: "Home",
  components: {
    Climate
  }
};
</script>

<style lang="scss">
.home {
  display: grid;
  gap: 4rem 1rem;
  grid-template-columns: repeat(6, 1fr);
  grid-template-rows: auto;
  justify-content: center;
}
</style>
