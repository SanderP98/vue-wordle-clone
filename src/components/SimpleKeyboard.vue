<template>
    <div :class="keyboardClass"></div>
</template>

<script>
import Keyboard from "simple-keyboard";
import "simple-keyboard/build/css/index.css";

export default {
    name: "SimpleKeyboard",
    props: {
        keyboardClass: {
            default: "simple-keyboard",
            type: String
        },
        input: {
            type: Array
        },
        solution: {
            type: String
        },
        submitted: {
            type: Boolean
        }
    },
    data: () => ({
        keyboard: null,
        guessedLetters: [],
    }),
    mounted() {
        this.keyboard = new Keyboard(this.keyboardClass, {
            layout: {
                'default': [
                    'q w e r t y u i o p',
                    'a s d f g h j k l',
                    '{enter} z x c v b n m {bksp}',
                ],
            },
            tabCharOnTab: false,
            maxLength: 5,
            theme: "wordle-theme hg-theme-default",
            onChange: this.onChange,
            onKeyPress: this.onKeyPress
        })
    },
    methods : {
        onChange(input) {
            this.$emit("onChange", input);
        },
        onKeyPress(button) {
            this.$emit("onKeyPress", button)
        }
    },
    watch : {
        input(input) {
            this.keyboard.setInput(input);
        }
    }
}
</script>

<style scope>
.wordle-theme .hg-button {
    font-family: inherit;
    font-weight: bold;
    border: 0;
    padding: 0;
    margin: 0 6px 0 0;
    height: 58px;
    border-radius: 4px;
    cursor: pointer;
    user-select: none;
    background-color: #818384;
    color: #FFFFFF;
    flex: 1;
    display: flex;
    justify-content: center;
    align-items: center;
    text-transform: uppercase;
    -webkit-tap-highlight-color: rgba(0,0,0,0.3);
}
.wordle-theme {
    background: none;
}

</style>
