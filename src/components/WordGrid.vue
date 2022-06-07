<template>
  <div class="flex mb-2">
    <LetterBox class="flex justify-center border border-gray-700 w-16 h-16 uppercase text-xl font-semibold transition-all" v-for="i in 5" :key="i" :letter="letters[i - 1]" :color="colors[i - 1]" />
  </div>
</template>

<script>
import LetterBox from './LetterBox.vue'

export default ({
    name: "WordGrid",
    components: {
        LetterBox
    },
    data: () => ({
        letters: [],
        colors: [],
    }),
    props: 
    {
        input: {
            type: String
        },
        solution: {
            type: String
        },
        submitted: {
            type: Boolean
        }
    },
    watch : {
        input(input) {
            this.letters.push(input.slice(-1))  
        },
        submitted(submitted) {
            if (submitted == true) {
                for (let i = 0; i < 5; i++) {
                    if (this.letters[i] == this.solution.charAt(i)) {
                        this.colors.push("green");
                    }
                    else if (this.solution.indexOf(this.letters[i]) > - 1 && this.solution.charAt(i) != this.letters[i]){
                        this.colors.push("yellow");  
                    }
                }
            }
        }
    },
    mounted() {

    }
})
</script>
