<template>
    <img class="responsiveImg" :src="url" :alt="titulo">
</template>

<script>
export default {
    props: ['url', 'titulo']
}
</script>

<style scoped>

    .responsiveImg {
    width: 100%;
  }

</style>