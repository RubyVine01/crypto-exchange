<template>
    <div>
        <input min="0" type="number" @input="changeAmount($event.target.value)" placeholder="Введите число">
        <button @click="convert()">Конвертировать</button>
        <button @click="favourite()">♥</button>
    </div>
</template>

<script>
export default {
    props: {
        changeAmount: {
            type: Function,
            required: true
        },
        convert: {
            type: Function,
            required: true
        },
        favourite: {
            type: Function,
            required: true
        }
    }
}
</script>


<style scoped>
div {
    display: flex;
    width: 570px;
    justify-content: space-between;
}

input {
    outline: none;
    border-radius: 3px;
    border: 0;
    padding: 10px 15px;
    background: #fafafa;
    color: #333;
    width: 300px;
    font-size: 1.2em;
}

button {
    padding: 15px 20px;
    color: #fff;
    text-transform: uppercase;
    cursor: pointer;
    background: #1a032d;
    border: 0;
    border-radius: 3px;
}

button:last-of-type {
    color: red;
    font-size: 20px;
}
</style>
