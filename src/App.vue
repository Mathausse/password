<template>
  <div>
    <label>Longueur : </label>
    <input type="number"/>
    <div>
      <button>Générer</button>
    </div>
    {{tableauMin.length}}
  </div>
</template>

<script>

export default {
  name: 'App',
  data: function(){
    return{
      tableauNum:[0,1,2,3,4,5,6,7,8,9],
      tableauSym:["$","%","^","&","!","@","#",":",";","'",",",".",">","/","*","-",",","|","?","~","_","=","+"],
      tableauMin:["a","b","c","d","e","f","g","h","i","j","k","l","m","n","o","p","q","r","s","t","u","v","w","x","y","z"],
      tableauMaj:["A","B","C","D","E","F","G","H","I","J","K","L","M","N","O","P","Q","R","S","T","U","V","W","X","Y","Z"],
    }
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
