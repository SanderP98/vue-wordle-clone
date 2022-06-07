<script>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import Navbar from './components/Navbar.vue'
import SimpleKeyboard from './components/SimpleKeyboard.vue'
import WordGrid from './components/WordGrid.vue'
import {allWords, getWordOfTheDay} from './words.js'

export default {
  name: "App",  
  components: {
    SimpleKeyboard,
    WordGrid,
    Navbar
  },
  data: () => ({
    submitted: [false, false, false, false, false, false],
    solution: getWordOfTheDay(),
    input: "",
    guessIndex: 0,
    guesses: ["", "", "", "", "", ""],
    allWords: allWords,
  }),
  mounted() {
  window.addEventListener("keyup", (e) => {
    e.preventDefault();
    let key =
      e.keyCode == 13
        ? "{enter}"
        : e.keyCode == 8
        ? "{bksp}"
        : String.fromCharCode(e.keyCode).toLowerCase();
    this.onKeyPress(key);
  });
  },
  methods: {
    onChange(input) {
      this.guesses[this.guessIndex] = input
      this.input = input
    },
    onKeyPress(button) {
      //Haal de laatste letter weg als backspace wordt gebruikt
      if (button == "{bksp}") {
        this.input = this.input.slice(0, -1);
        this.guesses[this.guessIndex] = this.input;
      }
      //Checkt of de gebruiker op {enter} drukt.
      else if (button == "{enter}") {
        //Er wordt gekeken of het maximale aantal toegestaande pogingen nog niet bereikt is.
        if (this.guesses[this.guessIndex].length >= 5) {
          //Controleer of het woord bestaat.
          if (this.allWords.includes(this.guesses[this.guessIndex])) {
            //Kijkt of je het juiste antwoord hebt opgegeven.
            if (this.guesses[this.guessIndex] == this.solution) {
              this.submitted[this.guessIndex] = true;
            }
            //Zo niet? Hoog de guessIndex op en leeg de input.
            else {
              this.submitted[this.guessIndex] = true;
              this.guessIndex++;
              this.input = "";
            }
          } 
          else {
            alert('geen bestaand woord');
            return false; 
          }
        }
      }
      else if(this.guesses[this.guessIndex].length < 5) {
        const alphaRegex = /[a-zA-Z]/;
        if (alphaRegex.test(button)) {
          this.guesses[this.guessIndex] += button;
        }
      }
    },
    onInputChange(input) {
      input = input.target.value;
    }
  }
}
</script>

<template>
  <div id="app">
      <Navbar/>
    <div class="flex flex-col h-screen max-w-md mx-auto justify-evenly">
      <div class="">
          <WordGrid v-for="(guess, i) in this.guesses" :key="i" :input="guess" :solution="this.solution" :submitted="this.submitted[i]" />
          <SimpleKeyboard @onChange="onChange" @onKeyPress="onKeyPress" :input="this.guesses" :solution="this.solution"  />
      </div>
    </div>
  </div>
</template>

<style>
  body {
    background: #121213;
  }
</style>

