<script>
export default {
    name: 'CountDown',
    data() {
        return {
            hours: 1,
            minutes: 2,
            seconds: 2,
            miliseconds: 0,
            isRunning: false,
            timer: null,
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
        },
        updateTime() {
            this.miliseconds += 33;
            if (this.miliseconds >= 1000) {
                if (!this.seconds == 0) {
                    this.seconds--;
                } else {
                    if (this.minutes == 0) {
                        if (this.hours == 0 && this.minutes == 0 && this.seconds == 0) {
                            clearInterval(this.timer);
                            this.isRunning = false;
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
    <h1>CountDown Timer</h1>
    <div id="timer">
        <input class="text-[30px] w-12 text-center h-[30px] m-4" type="text" v-model="hours"> :
        <input class="text-[30px] w-12 text-center h-[30px] m-4" type="text" name="minutes" id="minutes"
            v-model="minutes"> :
        <input class="text-[30px] w-12 text-center h-[30px] m-4" type="text" name="second" id="second"
            v-model="seconds">
    </div>
    <div id="action">
        <p>{{ isRunning ? 'Running' : 'Not Running' }}</p>
        <button @click="start()">{{ isRunning ? 'Stop' : 'Start' }}</button>
        <button @click="reset()">Reset</button>
    </div>
</template>