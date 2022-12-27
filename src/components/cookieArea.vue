<template>
    <div class="flex flex-col md:flex-row justify-evenly">
      <div class="flex flex-col pt-6 px-4 md:pl-6">
        <h3 class="text-xl text-center">Click Kepler to collect belly rubs</h3>
        <img src="../assets/kepler.jpg" alt="" class="w-60 self-center py-6 rounded-full" @click="bellyCounter++"/>
        <p class="text-lg text-center py-2">Belly Rubs: {{ bellyCounter > 1000000 ?bellyCounter.toExponential(4) : bellyCounter }}</p>
        <div class="flex flex-col border-solid border-2 border-black rounded-md mb-6">
          <p class="text-md text-center py-2">Auto Belly Rubs Per Second: {{ autoScratcher > 10000 ? autoScratcher.toExponential(4) : autoScratcher }}</p>
          <p class="text-md text-center py-2">Latex Glove Rubs Per Second: {{ (latexGloves * 3 > 10000) ? (latexGloves * 3).toExponential(4) : latexGloves * 3}}</p>
          <p class="text-md text-center py-2">Nitrile Glove Rubs Per Second: {{ (nitrileGloves * 5 > 10000) ? (nitrileGloves * 5).toExponential(4) : nitrileGloves * 5}}</p>
          <p class="text-md text-center py-2">Work Glove Rubs Per Second: {{ (workGloves * 16 > 10000) ? (workGloves * 16).toExponential(4) : workGloves * 16}}</p>
          <p class="text-md text-center py-2">Welding Glove Rubs Per Second: {{ (weldingGloves * 24 > 10000) ? (weldingGloves * 24).toExponential(4) : weldingGloves * 24}}</p>
          <p class="text-md text-center py-2">Total Rubs Per Second: {{ ((autoScratcher) + (latexGloves*3) + (nitrileGloves * 5) + (workGloves * 16) + (weldingGloves * 24) > 10000) ? ((autoScratcher) + (latexGloves*3) + (nitrileGloves * 5) + (workGloves * 16) + (weldingGloves * 24)).toExponential(4) : (autoScratcher) + (latexGloves*3) + (nitrileGloves * 5) + (workGloves * 16) + (weldingGloves * 24)}}</p>
        </div>
        <div v-if="luckyNumber == calcNumber" class="flex flex-col md:flex-row">
          <button :disabled="luckyClicked == true" @click="bellyCounter *= bonusValue; luckyClicked = true" class="px-20 py-3 mx-3 bg-green-400 rounded disabled:opacity-50">Multiply your belly rubs by {{ bonusValue }}</button>
          <p class="self-center">Click it before it disappears</p>
        </div>
        <div v-else class="flex flex-col md:flex-row">
          <button :disabled="luckyNumber != calcNumber" class="px-20 py-3 mx-3 bg-red-400 rounded">A bonus multiplier will appear here if you're lucky</button>
          <p class="self-center">Click it before it disappears</p>
        </div>
      </div>
      <div class="flex flex-col pt-10 px-4">
        <h3 class="text-xl text-center pb-6" @click="autoScratch()">Increase your belly rubbing productivity</h3>
        <div class="flex flex-col md:flex-row">
          <button :disabled="bellyCounter < (5 * autoAdd)" @click="autoScratcher++; bellyCounter -= (5 * autoAdd); autoAdd = Math.floor(1.2*(autoAdd+1.7)); autoScratch(); calledAuto = true" class="px-20 py-3 m-3 bg-blue-200 rounded disabled:opacity-50">Auto Belly Rub: Cost {{ (autoScratcherCost * autoAdd > 10000) ? (autoScratcherCost * autoAdd).toExponential(4) : autoScratcherCost * autoAdd}}</button>
          <p class="self-center">Auto Belly Rubs: {{ autoScratcher }}</p>
        </div>
        <div class="flex flex-col md:flex-row">
          <button :disabled="bellyCounter < (10+postAdd)" @click="latexGloves++; bellyCounter -= (10 + postAdd); postAdd = Math.floor(1.6*(postAdd+3)); autoLatex(); calledLatex = true" class="px-20 py-3 m-3 bg-blue-200 rounded disabled:opacity-50">Latex Gloves: Cost {{ (latexCost + postAdd > 10000) ? (latexCost + postAdd).toExponential(4) : latexCost + postAdd }}</button>
          <p class="self-center">Latex Gloves: {{ latexGloves }}</p>
        </div>
        <div class="flex flex-col md:flex-row">
          <button :disabled="bellyCounter < (45+nitrileAdd)" @click="nitrileGloves++; bellyCounter -= (45 + nitrileAdd); nitrileAdd = Math.floor(2*(nitrileAdd+3)); autoNitrile(); calledNitrile = true" class="px-20 py-3 m-3 bg-blue-200 rounded disabled:opacity-50">Nitrile Gloves: Cost {{ (nitrileCost + nitrileAdd > 10000) ? (nitrileCost + nitrileAdd).toExponential(4) : nitrileCost + nitrileAdd}}</button>
          <p class="self-center">Nitrile Gloves: {{ nitrileGloves }}</p>
        </div>
        <div class="flex flex-col md:flex-row">
          <button :disabled="bellyCounter < (95 + workAdd)" @click="workGloves++; bellyCounter -= (95 + workAdd); workAdd = Math.floor(2.2*(workAdd+5)); autoWork(); calledWork = true" class="px-20 py-3 m-3 bg-blue-200 rounded disabled:opacity-50">Work Gloves: Cost {{ (workCost + workAdd > 10000) ? (workCost + workAdd).toExponential(4) : workCost + workAdd }}</button>
          <p class="self-center">Work Gloves: {{ workGloves }}</p>
        </div>
        <div class="flex flex-col md:flex-row">
          <button :disabled="bellyCounter < (175 + weldingAdd)" @click="weldingGloves++; bellyCounter -= (175 + weldingAdd); weldingAdd = Math.floor(2.9*(weldingAdd+7)); autoWelding(); calledWelding = true" class="px-20 py-3 m-3 bg-blue-200 rounded disabled:opacity-50">Welding Gloves: Cost {{ (weldingCost + weldingAdd > 10000) ? (weldingCost + weldingAdd).toExponential(4) : weldingCost + weldingAdd }}</button>
          <p class="self-center">Welding Gloves: {{ weldingGloves }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script lang="ts">

  import { defineComponent } from 'vue';
  
  export default defineComponent({
    data(){
      return { 
        bellyCounter: 0,
        subtractRubs: false,
        latexGloves: 0,
        latexCost: 10,
        postAdd: 0,
        nitrileGloves: 0,
        nitrileAdd: 0,
        nitrileCost: 45,
        workGloves: 0,
        workAdd: 0,
        workCost: 95,
        weldingGloves: 0,
        weldingAdd: 0,
        weldingCost: 175,
        autoScratcher: 0,
        autoScratcherCost: 5,
        autoAdd: 1,
        calledAuto: false,
        calledLatex: false,
        calledNitrile: false,
        calledWork: false,
        calledWelding: false,
        seconds: 0,
        isAuto: true,
        interval: 1000,
        luckyNumber: 5,
        calcNumber: 0,
        luckyClicked: false,
        bonusValue: 0,
      }
    },

    methods: {
      autoScratch(){
        if (this.calledAuto == false){
          setInterval(() => {
            this.bellyCounter += this.autoScratcher
          }, this.interval)
        } else {
          this.calledAuto == true
        }
      },

      autoLatex(){
        if (this.calledLatex == false){
          setInterval(() => {
            this.bellyCounter += (this.latexGloves*3)
          }, this.interval)
        } else {
          this.calledLatex == true
        }
      },

      autoNitrile(){
        if (this.calledNitrile == false){
          setInterval(() => {
            this.bellyCounter += (this.nitrileGloves*5)
          }, this.interval)
        } else {
          this.calledNitrile == true
        }
      },

      autoWork(){
        if (this.calledWork == false){
          setInterval(() => {
            this.bellyCounter += (this.workGloves*16)
          }, this.interval)
        } else {
          this.calledWork == true
        }
      },

      autoWelding(){
        if (this.calledWelding == false){
          setInterval(() => {
            this.bellyCounter += (this.weldingGloves*24)
          }, this.interval)
        } else {
          this.calledWelding == true
        }
      }


    },

    created: function(){
      setInterval(() => {
        let luckyNumber = 5
        let calcNumber = Math.floor(Math.random() * 8 + 1)
        let bonusValue = Math.floor(Math.random() * 15 + 2)
        this.calcNumber = calcNumber
        this.bonusValue = bonusValue
        this.luckyClicked = false
      }, 4000)
    }
  })
  </script>
  

  