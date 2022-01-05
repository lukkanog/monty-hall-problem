<template>
  <div id="app">
    <h1>Problema de Monty Hall</h1>


    <form v-if="!started" class="starter-form">
      <div>
        <label>
          Quantidade de portas:
          <input type="number" v-model.number="numberOfDoors" min="3" max="20" />
        </label>
      </div>
      <div>
        <label>
          Porta premiada:
          <input type="number" v-model.number="selectedDoor" min="1" :max="numberOfDoors" />
        </label>
      </div>
      <button class="button" type="button" @click="started = true">Iniciar</button>
    </form>

    <div class="game" v-if="started">
      <div class="help-text">
        <p>
          Para selecionar sua porta, clique na porta desejada
        </p>
        <p>
          Para abrir uma porta, clique na maçaneta da mesma
        </p>
      </div>

      <button 
      class="button"
      type="button" 
      @click="started = false"
      v-if="started" 
    >
      Reiniciar
    </button>

    <ul class="doors">
      <li v-for="door in numberOfDoors" :key="door">
        <door 
          :number="door" 
          :hasGift="selectedDoor === door"
        />
      </li>
    </ul>
    </div>
    

  </div>
</template>

<script>
import Door from "@/components/Door.vue";

export default {
  name: 'App',
  components: {
    Door
  },
  data: () => ({
    started: false,
    numberOfDoors: 3,
    selectedDoor: 1,
  })
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: "Montserrat", sans-serif; 
  list-style: none;
}

body{
  color: #fff;
}

#app{
  display: flex;
  align-items: center;
  flex-direction: column; 
  background: rgb(106,106,106);
  background: radial-gradient(circle, rgba(106,106,106,1) 0%, rgba(33,33,33,1) 100%);
  min-height: 100vh;
}

h1 {
  border: 1px solid  #000;
  background-color: #0004;
  padding: 20px;
  margin: 60px 0;
}

.starter-form, .game {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-bottom: 40px;
  min-width: 300px;
}

.starter-form div{
  width: 100%;
  margin-bottom: 10px;
}

.starter-form div label{
  width: 100%;
  display: flex;
  justify-content: space-between;
  
}

.doors {
  display: flex;
  align-items: center;
  justify-self: space-evenly;
  margin-top: 40px;
}

.button {
  outline: none;
  color: #fff;
  border: 1px solid  #000;
  background-color: #0004;
  padding: 10px;
  cursor: pointer;
  transition: .3s;
}

.button:hover{
  filter: brightness(1.2);
}

input[type=number] {
  min-width: 60px;
}

.help-text {
  color: #ddd;
  font-weight: light;
  margin-bottom: 10px;
  margin-top: -30px;
  line-height: 1.6em;
  text-align: center;
}
</style>
