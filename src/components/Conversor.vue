<template>
  <div class="conversor">
    <h2>{{moedaA}} para {{moedaB}}</h2>
    <input type="text" v-model="moedaA_value" v-bind:placeholder="moedaA">
    <input class="botao" type="button" value="Converter" v-on:click="converter">
    <h2>{{moedaB_value}}</h2>
  </div>
</template>

<script>
export default {
  name: "Conversor",
  props: ["moedaA", "moedaB"],
  data() {
    return {
      moedaA_value: "",
      moedaB_value: 0
    };
  },

  methods: {
    converter() {
      if(this.moedaA_value){
      
      let de_para = this.moedaA + "_" + this.moedaB;
      let api_key = "Gere sua key para a api e substitua aqui"

      let url =
        "https://free.currencyconverterapi.com/api/v6/convert?q=" +
        de_para +
        "&compact=ultra&apiKey="+api_key;

      fetch(url)
        .then(resp => {
          return resp.json();
        })
        .then(json => {
          let cotacao = json[de_para];
          this.moedaB_value = (cotacao * parseFloat(this.moedaA_value)).toFixed(2);
        });
      }else{
        this.moedaB_value = 0
      }
    }
  }
};
</script>

 <style scoped>

.conversor {
  padding: 20px;
  max-width: 300px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
}

.botao{
  margin-left: 5px;
  border-radius: 5px;
}

</style>


