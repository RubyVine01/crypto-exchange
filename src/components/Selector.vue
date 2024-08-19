<template>
    <div class="dropdown">
        <button @click="toggleDropdown" class="dropdown-button">
            {{ convertNow ? convertNow : 'Выберите валюту' }}
        </button>
        <ul v-if="isOpen" class="dropdown-menu">
            <li @click="selectItem('BTC')" :className="convertNow == 'BTC' ? 'active' : ''">
                Bitcoin
            </li>
            <li @click="selectItem('ETH')" :className="convertNow == 'ETH' ? 'active' : ''">
                ETH
            </li>
            <li @click="selectItem('USD')" :className="convertNow == 'USD' ? 'active' : ''">
                USDT
            </li>

        </ul>
    </div>
</template>

<script>
export default {
    props: {
        setCrypto: {
            type: Function,
            required: true,
        },
        convertNow: {
            type: String,
            required: true,
        }
    },
    data() {
        return {
            isOpen: false,
        };
    },
    methods: {
        toggleDropdown() {
            this.isOpen = !this.isOpen;
        },
        selectItem(val) {
            this.setCrypto(val);
            this.isOpen = false;
        },
    },
};
</script>

<style scoped>
.dropdown {
    position: relative;
    display: inline-block;
}

.dropdown-button {
    background-color: #1a032d;
    color: #fff;
    padding: 15px;
    border: 3px solid #000;
    border-radius: 3px;
    cursor: pointer;
    width: 200px;
    text-align: left;
    position: relative;
}

.dropdown-button::after {
    content: "▼";
    float: right;
    margin-right: 10px;
}

.dropdown-menu {
    list-style: none;
    margin: 0;
    margin-top: 5px;
    padding: 0;
    background-color: #1a032d;
    border: 3px solid #000;
    border-radius: 3px;
    position: absolute;
    top: 100%;
    left: 0;
    width: 200px;
    z-index: 1000;
}

li {
    display: block;
    background: #1a032d;
    color: #fff;
    padding: 10px 0;
}

li:hover,
li.active {
    background: #611c9a;
    cursor: pointer;
}
</style>
