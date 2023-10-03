<template>
  <header class="text-center bg-blue-800 text-white p-4 mb-10">
    <div class="text-3xl md:text-5xl font-bold mb-3"><i class="fa-solid fa-person"></i> Population Tracker</div>
    <p>
      API by
      <a class="text-blue-300"
         href="https://documenter.getpostman.com/view/1134062/T1LJjU52"
         target="_blank">Countries & Cities API</a>
    </p>
  </header>
</template>

<script>
export default {
  name: 'Header',
  props: {
    msg: String
  }
}
</script>

