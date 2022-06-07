<script>

export default ({
    name: "LetterBox",
    props: {
        letter: String,
        color: String
    }
});
</script>

<template>
  <div class="grid max-w-xs grid-cols-5 gap-1 mx-auto mb-1 tile color-white" 
        :class="{
        'border-gray-400': color == '' && letter == '',
        'border-gray-500 bg-gray-500 text-white': letter,
        'bg-lime-500': color == 'green',
        'bg-amber-400': color == 'yellow'
        }">
      {{letter}}
  </div>
</template>

<style scoped>
.tile {
    display: inline-flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
    line-height: 2rem;
    font-weight: bold;
    vertical-align: middle;
    box-sizing: border-box;
    color: #FFFFFF;
    text-transform: uppercase;
    user-select: none;
}
</style>