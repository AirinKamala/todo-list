<script>
export default {
    name: 'CountDown',
    data() {
        return {
            hours: 0,
            minutes: 0,
            seconds: 0,
            miliseconds: 0,
            isRunning: false,
            timer: null,
            clear: false,
        }
    },
    methods: {
        start() {
            if (this.hours == 0 && this.minutes == 0 && this.seconds == 0) {
                return;
            } else if (this.seconds > 59 && this.minutes >= 0) {
                this.reset();
                return;
            } else if (this.hours > 24) {
                this.reset;
                return
            } else {
                
                if (!this.isRunning) {
                    this.timer = setInterval(this.updateTime, 33);
                } else {
                    clearInterval(this.timer);
                }
                this.isRunning = !this.isRunning;
            }
            
        },
        reset() {
            clearInterval(this.timer);
            this.hours = 0;
            this.minutes = 0;
            this.seconds = 0;
            this.miliseconds = 0;
            this.isRunning = false;
            this.clear=false;
        },
        updateTime() {
            this.clear=true;
            this.miliseconds += 33;
            if (this.miliseconds >= 1000) {
                if (!this.seconds == 0) {
                    this.seconds--;
                } else {
                    if (this.minutes == 0) {
                        if (this.hours == 0 && this.minutes == 0 && this.seconds == 0) {
                            clearInterval(this.timer);
                            this.isRunning = false;
                            this.clear=false;
                            return;
                        }
                        this.minutes = 59;
                        this.seconds = 59;
                        this.hours--;
                    } else {
                        this.minutes--;
                        this.seconds = 59;
                    }
                }
                this.miliseconds -= 1000;
            }
        }
    }
}
</script>

<template>
    <h1>Countdown Timer</h1>
    <div id="timer">
        <input type="text" :disabled="clear" v-model="hours" id="hours">
        :
        <input type="text" :disabled="clear" name="minutes" id="minutes"
            v-model="minutes"> :
        <input type="text" :disabled="clear" name="second" id="second"
            v-model="seconds">
    </div>
    <div id="action">
        <button @click="start()">{{ isRunning ? 'Stop' : 'Start' }}</button>
        <button @click="reset()">Reset</button>
    </div>
</template>
<style>
    input{
        border: none;
        background-color: transparent;
        font-size: 30px;
        width: 2rem;
        height: 30px;
        text-align: center;
        margin: 2rem;
    }
</style>