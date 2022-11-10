<script lang="ts">
export default {
    mounted() {
        this.secondHand = document.getElementById('second-hand')

        setInterval(this.setClock, 1000)
        this.setClock
    },
    data() {
        return {
            secondHand: document.getElementById('second-hand')
        }
    },
    methods: {
        setRotation: function (element: HTMLElement | null, rotationRatio: number) {
            element?.style.setProperty('--rotation', (rotationRatio * 360).toString())
        },
        setClock: function () {
            const currentDate = new Date()
            const secondsRatio = currentDate.getSeconds() / 60
            this.setRotation(this.secondHand, secondsRatio)
        }
    },
}


</script>

<template>
    <div class="clock">
        <div class="hand second" id="second-hand"></div>
    </div>
</template>

<style scoped>
*,
*::after,
*::before {
    box-sizing: border-box;
}

.clock {
    width: 300px;
    height: 300px;
    background-color: rgba(255, 255, 255, .8);
    border-radius: 50%;
    border: 25px solid rgba(122, 29, 29, 0.967);
    position: relative;
}

.clock .hand {
    --rotation: 0;
    position: absolute;
    bottom: 50%;
    left: 50%;
    border: 1px solid white;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
    transform-origin: bottom;
    z-index: 10;
    transform: translateX(-50%) rotate(calc(var(--rotation) * 1deg));
    box-shadow: 4px 5px rgba(104, 103, 103, 0.304);
}

.clock::after {
    content: '';
    position: absolute;
    background-color: black;
    z-index: 11;
    width: 15px;
    height: 15px;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    border-radius: 50%;
}

.clock .hand.second {
    width: 3px;
    height: 45%;
    background-color: red;
}
</style>