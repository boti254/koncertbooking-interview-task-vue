<template>
  <div class="title_container">
    <span class="title_border"></span>
    <h1 class="title_poke">Pokemonok</h1>
  </div>
</template>

<style lang="scss">
$shadow-color: rgb(187, 185, 185);
$title-border-color: rgb(14, 167, 170);

.title_poke{
  text-shadow: 0px 5px 0.15em $shadow-color;
}
.title_border{
  height: 40px;
  width: 6px;
  background-color: $title-border-color;
  border-radius: 99px;
  margin-right: 20px;
  box-shadow: 0px 5px 0.3em $shadow-color;
}
.title_container{
  display: flex;
  align-items: center;
  padding-bottom: 20px;
  padding-top: 20px;
}
</style>
