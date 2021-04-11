<template>
  <div class="converter">
    <span v-on:click="convert" class="icon"></span>

    <div>
      <div class="form-group">
        <div class="form-control">
          <label for="you-have">You Have</label>
          <input v-model="youHaveQty" id="you-have" type="text">
        </div>

        <div class="form-control light">
          <label for="you-have">USD</label>
          <select v-model="youHaveCurrency" name="currency" id="yh-currency">
            <option value="USD">USD</option>
            <option value="PHP">PHP</option>
          </select>
        </div>
      </div>

      <span>Rates will <b>not</b> be refreshed in <b>30 seconds</b></span>
    </div>

    <div>
      <div class="form-group">
        <div class="form-control">
          <label for="you-have">You Get</label>
          <input v-model="youGetQty" disabled id="you-have" type="text">
        </div>

        <div class="form-control light">
          <label for="you-have">PHP</label>
          <select v-model="youGetCurrency" name="currency" id="yg-currency">
            <option value="USD">USD</option>
            <option value="PHP">PHP</option>
          </select>
        </div>
      </div>

      <span>1USD = <b>0.89GBP</b></span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Converter',
  data() {
    return {
      youHaveQty: '0',
      youHaveCurrency: 'USD',
      youGetQty: '0',
      youGetCurrency: 'PHP',
    }
  },
  methods: {
    async convert() {
      const FREE_CURRENCY_API_KEY = '4d8d46fd90a1c3248228'
      const convertCurrencies = `${this.youHaveCurrency}_${this.youGetCurrency}`
      const url = `https://free.currconv.com/api/v7/convert?q=${convertCurrencies}&compact=ultra&apiKey=${FREE_CURRENCY_API_KEY}`

      const response = await fetch(url)
      const data = await response.json()

      this.youGetQty = (data[convertCurrencies] * this.youHaveQty).toFixed(2)
    }
  }
}
</script>

<style scoped lang="scss">
  .converter {
    position:  relative;

    border-radius: 0.5rem;

    padding: 1rem 0;

    display: grid;
    grid-template-columns: 1fr 1fr;

    background: var(--white); 

    > div {
      max-width: 700px;

      padding: 2rem 3rem;

      span {
        display: block;

        margin-top: 2rem;

        font-size: 0.75rem;
      }

      &:last-child {
        background: #FAFAFA;
        border-radius: inherit;
      }
    }
  }

  .form-group {
    display: flex;
    align-content: flex-end;

    div + div {
      margin-left: 1.5rem;
    }
  }

  .form-control {
    display: flex;
    flex-direction: column;
    align-items: flex-start;

    label {
      font-weight: 600;
    }

    &.light {
      label {
        font-size: 0.75rem;

        color: var(--gray-700);
        margin-bottom: 0.35rem;
      }
    }

    & :is(input, select) {
      height: 3rem;
      min-width: 120px;

      margin-top: 0.75rem;

      font-size: 2rem;
      font-weight: 600;

      border: 0;
      border-bottom: 2px solid var(--gray-100);

      color: var(--blue-800);
      background: transparent;

      outline: 0;
    }
  }

  .icon {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);

    display: flex;
    align-items: center;
    justify-content: center;

    width: 2.75rem;
    height: 2.75rem;

    background: var(--blue-800);

    border-radius: 50%;

    transition: all 0.2s;
    cursor: pointer;

    &:hover {
      background: var(--blue-700);
    }
  }
</style>