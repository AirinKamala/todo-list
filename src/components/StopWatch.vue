<style lang="scss">
p {
    font-size: 36px;
    font-weight: 700;
    text-align: center;
    color:white;
    mix-blend-mode: difference;
}
span {
    margin: 12px;
}

button {
    margin: 5px 10px;
    color: black;
    background-color: white ;
    mix-blend-mode: difference;
    
    &:hover{
        background-color: #f1f1f1;
    }
}

</style>
<template>
<div id="tem">
    <h1>Stopwatch</h1>
    <p> <span>{{ hours }}</span>:
        <span>{{ minutes }}</span>:
        <span>{{ seconds }}</span>
    </p>
    <button @click="start()">{{ isRunning ? 'Stop' : 'Start' }}</button>
    <button @click="reset()">Reset</button>
    </div>
</template>
<script>
export default {
    name: 'StopWatch',
    data() {
        return {
            isRunning: false,
            seconds: 0,
            minutes: 0,
            hours: 0,
            miliseconds: 0,
            timer: null
        }
    },
    methods: {
        start() {
            if (!this.isRunning) {
                this.timer = setInterval(this.updatetime, 33);
            } else {
                clearInterval(this.timer)
            }
            this.isRunning = !this.isRunning;
        },
        reset() {
            clearInterval(this.timer);
            this.minutes = 0;
            this.hours = 0;
            this.seconds = 0;
            this.isRunning = false;
        },
        updatetime() {
            this.miliseconds += 33;
            if (this.miliseconds >= 1000) {
                this.seconds++;
                this.miliseconds -= 1000;
                if (this.seconds == 60) {
                    this.minutes++;
                    this.seconds = 0;
                    if (this.minutes == 60) {
                        this.hours++;
                        this.minutes = 0;
                    }
                }
            }
        }
    }
}
</script>