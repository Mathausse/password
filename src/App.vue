<template>
  <div>
    <label>Longueur : </label>
    <input type="number" v-model="this.taille"/>
    <label>Majuscules</label>
    <input type="checkbox" v-model="this.avecMaj"/>
    <label>Nombres</label>
    <input type="checkbox" v-model="this.avecNom">
    <label>Symboles</label>
    <input type="checkbox" v-model="this.avecSym"/>
    
    <div>
      <button v-on:click="generationMotDePasse(this.taille, this.avecMaj, this.avecNom, this.avecSym)">Générer</button>
    </div>
    {{this.password}}
  </div>
</template>

<script>

export default {
  name: 'App',
  data: function(){
    return{
      MINUSCULE_CODE_CHAR: [],
      MAJUSULE_CODE_CHAR: [],
      NOMBRE_CODE_CHAR: [],
      SYMBOlE_CODE_CHAR: [],
      password: "",
      avecMaj: false,
      avecNom: false,
      avecSym: false,
      taille: 0,
    }
  },
  mounted() {
    this.remplissageListe();
  },
  methods:{
    randomFloat(){
      const int = window.crypto.getRandomValues(new Uint32Array(1))[0]
      return int/ 2**32
    },
    randomInt(range){
      return Math.floor(this.randomFloat() * range)
    },
    remplissageListe(){
      this.MINUSCULE_CODE_CHAR = this.arrayFromLowToHigh(97, 122);
      this.MAJUSULE_CODE_CHAR = this.arrayFromLowToHigh(65,90);
      this.NOMBRE_CODE_CHAR = this.arrayFromLowToHigh(48, 57);
      this.SYMBOlE_CODE_CHAR =  this.arrayFromLowToHigh(33, 47).concat(this.arrayFromLowToHigh(58,64)).concat(this.arrayFromLowToHigh(91, 96)).concat(this.arrayFromLowToHigh(123, 126));
    },
    generationMotDePasse(nbCharactere, majuscule, nombre, symbole){
      let codeChar = this.MINUSCULE_CODE_CHAR;
      if(majuscule){ codeChar = codeChar.concat(this.MAJUSULE_CODE_CHAR);}
      if(nombre){ codeChar = codeChar.concat(this.NOMBRE_CODE_CHAR);}
      if(symbole){ codeChar = codeChar.concat(this.SYMBOlE_CODE_CHAR);}
      codeChar.sort(function(a,b){return a-b});
      const characteresMotDePasse = [];
      for(let i = 0; i < nbCharactere; i++){
        const c = codeChar[this.randomInt(codeChar.length)];
        characteresMotDePasse.push(String.fromCharCode(c));
      }
      this.password = characteresMotDePasse.join('');
    }, 
    arrayFromLowToHigh(min, max){
      const liste = []
      for (let i = min; i <= max; i++) {
        liste.push(i);        
      }
      return liste;
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
