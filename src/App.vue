<template>
  <div>
    <label>Longueur : </label>
    <input type="number"/>
    <div>
      <button>Générer</button>
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
    }
  },
  mounted() {
    this.remplissageListe();
    const password = this.generationMotDePasse(15, true, true, true);
    console.log(password)
  },
  methods:{
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

      const characteresMotDePasse = [];
      for(let i = 0; i < nbCharactere; i++){
        const c = codeChar[Math.floor(Math.random() * codeChar.length)];
        characteresMotDePasse.push(String.fromCharCode(c));
      }
      return characteresMotDePasse.join('');
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
