<template>
    <div class="converter">
        <div class="moedas">
            <div class="conversao">
                <div class="select">
                    <select name="moedaA" id="moedaB">
                        <option v-for="moedaA in moedas" :key="moedaA" :value="moedaA">{{moedaA}}</option>
                    </select>
                    <input class="troca" type="button" value="←→" v-on:click="troca()">
                    <select name="moedaB" id="moedaA">
                        <option v-for="moedaB in moedas" :key="moedaB" :value="moedaB">{{moedaB}}</option>
                    </select>
                </div>
                <input type="text" v-model="moedaA_value" placeholder="Valor">
                <input type="button" value="Converter" v-on:click="converter()">
                <p>{{moedaB_value}}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Converter',
  data: () => ({moedas: ["AED", "AFN", "ALL", "AMD", "ANG", "AOA", "ARS", "AUD", "AWG", "AZN", "BAM", 
            "BBD","BDT", "BGN", "BHD", "BIF", "BMD", "BND", "BOB", "BRL", "BSD", "BTC", "BTN", "BWP", "BYN", 
            "BYR", "BZD", "CAD", "CDF", "CHF", "CLF", "CLP", "CNY", "COP", "CRC", "CUC", "CUP", "CVE",
            "CZK", "DJF", "DKK", "DOP", "DZD", "EGP","ERN","ETB","EUR","FJD","FKP","GBP","GEL","GGP",
            "GHS","GIP","GMD","GNF","GTQ","GYD","HKD","HNL","HRK","HTG","HUF","IDR","ILS","IMP","INR",
            "IQD","IRR","ISK","JEP","JMD","JOD","JPY","KES","KGS","KHR","KMF","KPW","KRW","KWD","KYD",
            "KZT","LAK","LBP","LKR","LRD","LSL","LVL","LYD","MAD","MDL","MGA","MKD","MMK","MNT","MOP",
            "MRO","MUR","MVR","MWK","MXN","MYR","MZN","NAD","NGN","NIO","NOK","NPR","NZD","OMR","PAB",
            "PEN","PGK","PHP","PKR","PLN","PYG","QAR","RON","RSD","RUB","RWF","SAR","SBD","SCR","SDG",
            "SEK","SGD","SHP","SLL","SOS","SRD","STD","SVC","SYP","SZL","THB","TJS","TMT","TND","TOP",
            "TRY","TTD","TWD","TZS","UAH","UGX","USD","UYU","UZS","VEF","VND","VUV","WST","XAF","XAG",
            "XCD","XDR","XOF","XPF","YER","ZAR","ZMK","ZMW","ZWL",],
            moedaA_value: "",
            moedaB_value: 0
            }),
  methods: {
      converter(){
          let selectB = document.querySelector("#moedaA")
          let selectA = document.querySelector("#moedaB")
          let moedaA = selectA.options[selectA.selectedIndex].value
          let moedaB = selectB.options[selectB.selectedIndex].value
          const moeda = `${moedaA}_${moedaB}`
          const url = `https://free.currconv.com/api/v7/convert?apiKey=93f91908b121717a2ed9&q=${moeda}&compact=y`
          fetch(url).then(res => res.json()).then(json => {
              const conversao =  json[moeda].val
              this.moedaB_value = (conversao * this.moedaA_value).toFixed(2)
          })
      },
      troca(){
          let selectB = document.querySelector("#moedaA")
          let selectA = document.querySelector("#moedaB")
          let moedaA = selectA.options.selectedIndex
          let moedaB = selectB.options.selectedIndex
          selectB.options.selectedIndex = moedaA
          selectA.options.selectedIndex = moedaB
          this.converter()
      }
  }
}
</script>