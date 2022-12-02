<template>
  <div id="container">
    <h1>It's a password</h1>
    <div id="passwordContainer">
      <h3>{{this.password}}</h3>
    </div>
    <div id="pannel">
      <label for="len">Longueur : </label>
      <input type="number" id="num" min="1" v-model="this.taille"/>
      <label for="maj">Majuscules</label>
      <input type="checkbox" id="maj" v-model="this.avecMaj"/>
      <label for="num">Nombres</label>
      <input type="checkbox" id="num" v-model="this.avecNom">
      <label fom="sym">Symboles</label>
      <input type="checkbox" id="sym" v-model="this.avecSym"/>
      
      <button v-on:click="generationMotDePasse(this.taille, this.avecMaj, this.avecNom, this.avecSym)">Générer</button>
    </div>
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
      taille: 1,
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
body{
  background-color: #283969;
  color: black;
  display: flex;
  justify-content: center;
  align-items: center;
}

h1{
  margin: 0;
  text-align: center;
  font-weight: bold;
  font-size: 5em;
}

button{
  grid-column: span 2;
  background-color: transparent;
  border: 2px solid white;
  color: black;
  padding: .5rem 1rem;
  font-weight: bold;
  cursor: pointer;
  border-radius: 1rem;
}

button:hover{
  background-color: #FFFFFF33;
}

#container{
  background-color: antiquewhite;
  margin-top: 10vh;
  padding: 3rem;
  border-radius: 1rem;
  border: 2px solid black;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

#pannel{
  display: grid;
  margin-top: 2rem;
  grid-template-columns: auto auto;
  row-gap: 1rem;
  column-gap: 3rem;
  justify-content: center;
  align-items: center;
}

#passwordContainer{
  background-color: black;
  color: white;
  margin-top: 1rem;
  padding: 1rem;
  border: 1px solid #333;
  height: 2rem;
  width: 350px;
  display: flex;
  justify-content: center;
  align-items: center;
  word-break: break-all;
  border-radius: .5rem;
}
</style>
