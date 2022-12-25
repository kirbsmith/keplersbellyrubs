<template>
    <div class="flex flex-row justify-evenly">
      <div class="flex flex-col pt-6 pl-6">
        <h3 class="text-xl text-center">Click Kepler to collect belly rubs</h3>
        <img src="../assets/kepler.jpg" alt="" class="w-60 self-center py-6 rounded-full" @click="bellyCounter++"/>
        <p class="text-lg text-center py-2">Belly Rubs: {{ bellyCounter }}</p>
        <div class="flex flex-col border-solid border-2 border-black rounded-md mb-6">
          <p class="text-md text-center py-2">Auto Belly Rubs Per Second: {{ autoScratcher/2 }}</p>
          <p class="text-md text-center py-2">Latex Glove Rubs Per Second: {{ latexGloves }}</p>
          <p class="text-md text-center py-2">Nitrile Glove Rubs Per Second: {{ nitrileGloves * 2 }}</p>
          <p class="text-md text-center py-2">Work Glove Rubs Per Second: {{ workGloves * 5 }}</p>
          <p class="text-md text-center py-2">Total Rubs Per Second: {{ (autoScratcher/2) + (latexGloves) + (nitrileGloves * 2) + (workGloves * 5) }}</p>
        </div>
      </div>
      <div class="flex flex-col pt-10 pl-8">
        <h3 class="text-xl text-center pb-6" @click="autoScratch()">Increase your belly rubbing productivity</h3>
        <div class="flex flex-row">
          <button :disabled="bellyCounter < (5 * autoAdd)" @click="autoScratcher++; bellyCounter -= (5 * autoAdd); autoAdd = Math.floor(1.4*(autoAdd+1.7)); autoScratch(); calledAuto = true" class="px-20 py-3 m-3 bg-blue-200 rounded disabled:opacity-50">Auto Belly Rub: Cost {{ autoScratcherCost * autoAdd }}</button>
          <p class="self-center">Auto Belly Rubs: {{ autoScratcher }}</p>
        </div>
        <div class="flex flex-row">
          <button :disabled="bellyCounter < (10+postAdd)" @click="latexGloves++; bellyCounter -= (10 + postAdd); postAdd = Math.floor(1.8*(postAdd+3)); autoLatex(); calledLatex = true" class="px-20 py-3 mx-3 bg-blue-200 rounded disabled:opacity-50">Latex Gloves: Cost {{ latexCost + postAdd }}</button>
          <p class="self-center">Latex Gloves: {{ latexGloves }}</p>
        </div>
        <div class="flex flex-row">
          <button :disabled="bellyCounter < (45+nitrileAdd)" @click="nitrileGloves++; bellyCounter -= (45 + nitrileAdd); nitrileAdd = Math.floor(2.3*(nitrileAdd+3)); autoNitrile(); calledNitrile = true" class="px-20 py-3 m-3 bg-blue-200 rounded disabled:opacity-50">Nitrile Gloves: Cost {{ nitrileCost + nitrileAdd }}</button>
          <p class="self-center">Nitrile Gloves: {{ nitrileGloves }}</p>
        </div>
        <div class="flex flex-row">
          <button :disabled="bellyCounter < (95 + workAdd)" @click="workGloves++; bellyCounter -= (95 + workAdd); workAdd = Math.floor(2.8*(workAdd+5)); autoWork(); calledWork = true" class="px-20 py-3 m-3 bg-blue-200 rounded disabled:opacity-50">Work Gloves: Cost {{ workCost + workAdd }}</button>
          <p class="self-center">Work Gloves: {{ workGloves }}</p>
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
        autoScratcher: 0,
        autoScratcherCost: 5,
        autoAdd: 1,
        calledAuto: false,
        calledLatex: false,
        calledNitrile: false,
        calledWork: false,
        seconds: 0,
        isAuto: true,
        interval: 2000,
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
            this.bellyCounter += (this.latexGloves*2)
          }, this.interval)
        } else {
          this.calledLatex == true
        }
      },

      autoNitrile(){
        if (this.calledNitrile == false){
          setInterval(() => {
            this.bellyCounter += (this.nitrileGloves*4)
          }, this.interval)
        } else {
          this.calledNitrile == true
        }
      },

      autoWork(){
        if (this.calledWork == false){
          setInterval(() => {
            this.bellyCounter += (this.workGloves*10)
          }, this.interval)
        } else {
          this.calledWork == true
        }
      }


    }
  })
  </script>
  

  