<template>
  <div class="hello">
    <h1>Ironman Sucks</h1>
    <div class="fighter-choices">
        <div>
            <h2>Fighter 1: </h2>
            <div class = "fighter-img-contain">
              <div v-bind:class = "{dead: dead1}">
                 <img v-if = "selectedFighters[0]" class = "fighter-img" :src= "selectedFighters[0].image" alt="img"> 
              </div>
              <h2 v-if = "selectedFighters[0]" >{{selectedFighters[0].name}}</h2>
              <div class = 'stats'>
                <h3 v-if = "selectedFighters[0]" >ATK: {{selectedFighters[0].attack}}</h3>
                <h3 v-if = "selectedFighters[0]" >DEF: {{selectedFighters[0].defense}}</h3>
              </div>
              
              <img v-if = "!selectedFighters[0]" class = "fighter-img" src="https://png.icons8.com/metro/1600/avengers.png" alt="img">
            </div>
        </div>
        <button v-on:click = "battleFighters(selectedFighters[0], selectedFighters[1])">BATTLE</button>
        <div>
          <h2>Fighter 2: </h2>
          <div class = "fighter-img-contain">
            <div v-bind:class = "{dead: dead2}">
              <img v-if = "selectedFighters[1]" class = "fighter-img" :src= "selectedFighters[1].image" alt="img">
            </div>
            <h2 v-if = "selectedFighters[1]" >{{selectedFighters[1].name}}</h2>
            <div class = 'stats'>
                <h3 v-if = "selectedFighters[1]" >ATK: {{selectedFighters[1].attack}}</h3>
                <h3 v-if = "selectedFighters[1]" >DEF: {{selectedFighters[1].defense}}</h3>
              </div>
            <img  v-if = "!selectedFighters[1]" class = "fighter-img" src="https://png.icons8.com/metro/1600/avengers.png" alt="img">
          </div>
        </div>
        
      </div>
    <div v-show = "view == 'list'">
      <button @click = "view = 'create'" >Create Fighter</button>
    </div>

    <div v-show = "view == 'create'">
      
      
      <button @click = "view = 'list'">List</button>
      <h2>Create Fighter</h2>
      <input v-model= "name" placeholder="Name"/>
      <input v-model= "attack" placeholder= "Attack"/>
      <input v-model= "defense" placeholder="Defense"/>
      <input v-model= "image" placeholder= "Image URL" type= "url"/>
      <button @click = "addFighter(name, attack, defense, image)">Add Fighter</button>
    </div>
    <fighters :myfighters = "myfighters" :selectFighter = "selectFighter"></fighters>
  </div>
</template>

<script>
import fighters from './Fighters'
export default {
  name: 'Home',
  data () {
    return {
      myfighters: [{name: "Ironman", attack: 15, defense: 995, image: "data:image/jpeg;base64,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"},
      {name: "Thor", attack: 16, defense: 999, image: "https://vignette.wikia.nocookie.net/avengersalliance/images/1/1b/Mighty_Thor_Portrait_Art.png/revision/latest?cb=20131030210532"}],      
      view: 'create',
      selectedFighters: [],
      dead1: false,
      dead2: false
    }
  },
  components: {
    fighters: fighters
  },
  methods:{
    addFighter: function(name, attack, defense, image){
      let fighterObj = {
        name: name,
        attack: attack,
        defense: defense,
        image: image
      }
      this.myfighters.push(fighterObj)
  },
    selectFighter: function(fighter){
      if (this.selectedFighters.length < 2){
        this.selectedFighters.push(fighter)
      } else {
        this.selectedFighters.shift()
        this.selectedFighters.push(fighter)
      }

    },

    battleFighters: function(f1, f2){
      console.log(f2)
        if (f1.defense < f2.defense && f1.defense > 0 && f2.defense > 0){
          f2.defense -= f1.attack;
          f1.defense -= f2.attack;
              console.log(f2)
              this.battleFighters(f1, f2);
        
      } else if (f2.defense < f1.defense && f2.defense > 0 && f1.defense > 0){
          f1.defense -= f2.attack;
          f2.defense -= f1.attack;
          console.log(f2)
              this.battleFighters(f1, f2);
        
      } else if (f2.defense === f1.defense && f2.defense > 0 && f1.defense > 0){
          f2.defense -= f1.attack;
          f1.defense -= f2.attack;
          console.log(f2)
              this.battleFighters(f1, f2);
        
      } else if (f2.defense <= 0){
          this.dead2 = true
          return  alert (`${f2.name} was defeated!`)
      } else if (f1.defense <= 0){
          this.dead1 = true
          return   alert (`${f1.name} was defeated!`)
      }
      }
      
    }

  

}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.fighter-choices {
  width: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  text-align: center;

}

.fighter-img {
  height: 300px;
}

.fighter-img-contain {
  height: 450px;
  width: auto;
}

.stats {
  display: flex;
  justify-content: space-around;
  align-items: center;
  text-align: center;
}

.dead {
  transition: 1s;
  transform:rotate(90deg)
}
</style>
