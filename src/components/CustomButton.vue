<template>
    <button @click="handleButtonClick">
        {{ buttonText }}
    </button>
</template>
  
<script lang="ts">
export default {
    props: {
        buttonText: {
            type: String,
            default: 'Botão',
        },
        icon: {
            type: String,
            default: '',
        },
    },
    methods: {
        handleButtonClick() {
            this.$emit('buttonClick', this.buttonText);
        },
    },
};
</script>
  
<style scoped>
button {
    margin: 20px 15px;
    outline: none;
    border: none;
    background: #7c74d3;
    box-shadow: .3rem .3rem .6rem #c8d0e7;
    color: #000000;
    border-radius: 1rem;
    cursor: pointer;
    width: 15rem;
    height: 4rem;
    font-size: 1em;

}

button:hover {
    background: #8a84cc;
}

button:active {
    box-shadow: inset .2rem .2rem 1rem #6f9fdb,
        inset -.2rem -.2rem 1rem #8abdff;
}

i {
    margin-right: 5px;
}
</style>
  