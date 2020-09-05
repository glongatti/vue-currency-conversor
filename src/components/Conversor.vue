<template>
  <div class="conversor">
    <h2>{{moedaA}} To {{moedaB}}</h2>
    <input type="text" v-model="moedaAValue" v-bind:placeholder="moedaA" />
    <input type="button" value="Converter" v-on:click="converter"/>
    <h2>{{moedaBValue}}</h2>
  </div>
</template>

<script>
export default {
  name: "Conversor", //
  props: ["moedaA", "moedaB"],
  data() {
    return {
      moedaAValue: "",
      moedaBValue: 0,
    };
  },
  methods: {
    async converter() {
      let dePara = `${this.moedaA}_${this.moedaB}`;
      const url = `http://free.currencyconverterapi.com/api/v5/convert?q=${dePara}&compact=y&apiKey=4019510c4d9db3ff5ef2`;

      const res = await fetch(url);
      console.log('response',res);
      const json = await res.json();
      const cotacao = json[dePara].val;

      this.moedaBValue = (cotacao * parseFloat(this.moedaAValue)).toFixed(2);
    },
  },
};
</script>

<style scoped>
  .conversor{
    padding:20px;
    max-width:300px;
    box-shadow:0 4px 8px 0 rgba(0,0,0,0.2);
  }

</style>