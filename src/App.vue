<template>
  <div class="container">
    <h1>Bread Math</h1>
    <label>
      Target Dough Weight(g)
      <input v-model.number="tdw" type="number" step="1" />
    </label>
    <label>
      Hydration(%)
      <input v-model.number="hydration" type="number" step="1" />
    </label>
    <table>
      <tr>
        <th>Ingredient</th>
        <th>Amount(g)</th>
      </tr>
      <tr v-for="(output, name) in outputs" :key="name">
        <td>{{ name }}</td>
        <td>{{ output }}</td>
      </tr>
    </table>
    <small>
      made by
      <a href="https://johnmeguerian.com">jmegs.</a> Source on
      <a href="https://github.com/jmegs/bread-math">GitHub.</a>
    </small>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hydration: 76,
      tdw: 1000
    }
  },
  computed: {
    percentHydration() {
      return this.hydration / 100
    },
    flour() {
      return Math.round(this.tdw / (1 + this.percentHydration + 0.025))
    },
    water() {
      return Math.round(this.flour * this.percentHydration)
    },
    salt() {
      return Math.round(this.flour * 0.025)
    },
    starter() {
      return Math.round(this.flour * 0.2)
    },
    outputs() {
      return {
        flour: Math.round(this.flour - this.starter / 2),
        water: Math.round(this.water - this.starter / 2),
        salt: this.salt,
        starter: this.starter
      }
    }
  }
}
</script>

<style>
body {
  border-top: 3px solid #121212;
}
@media (prefers-color-scheme: dark) {
  body {
    border-top-color: #fff;
  }
}
.container {
  max-width: 40ch;
  margin: 0 auto;
  padding: 5vmin;
}

h1 {
  letter-spacing: -0.02em;
}

td {
  text-transform: capitalize;
}

tr > :nth-child(2) {
  text-align: right;
}
</style>