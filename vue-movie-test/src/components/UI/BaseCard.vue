<template>
  <div class="card">
    <slot></slot>
  </div>
</template>

<style scoped>
.card {
  background: whitesmoke;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 0.5rem;
  margin: 2rem 0 2rem auto;
  width: 80%;
}

@media screen and (min-width: 1000px) {
  .card {
    width: 90%;
    height: 200px;
  }
}
</style>
