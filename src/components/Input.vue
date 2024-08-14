<template>
    <input min="0" type="number"  @input="changeAmount($event.target.value)" placeholder="Введите число">
    <button>Конвертировать</button>
</template>

<script>
export default {
    props: {
        changeAmount: {
            type: Function,
            required: true
        }
    }
}
</script>


<style scoped>
input {
    outline: none;
    border-radius: 3px;
    border: 0;
    padding: 10px 15px;
    background: #fafafa;
    color: #333;
    width: 500px;
    font-size: 1.2em;
}
</style>
