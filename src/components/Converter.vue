<template>
  <div class="converter">
    <div>
      <div class="form-control">
        <label for="you-have">You have</label>
        <input id="you-have" type="text">
      </div>

      <div class="form-control">
        <label for="you-have">You have</label>
        <input id="you-have" type="text">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Converter'
}
</script>

<style scoped lang="scss">
  .converter {

    border-radius: 0.5rem;

    background: var(--white) 
  }

  .converter div {
    display: grid;
    grid-template-columns: 1fr 1fr;
  }

  .converter div .form-control {
    display: flex;
    flex-direction: column;
    align-items: flex-start;

    padding: 2rem 4rem;
  }
</style>