<style>
span{
    font-size: 24px;
    font-weight: 700;
}
button{
    margin-left: 5px;
}
</style>
<template>
    <h1>Ini adalah stopwatch</h1>
    <p><span>{{ hours }}</span>:
        <span>{{ minutes }}</span>:
        <span>{{ seconds }}</span>
    </p>
<p>{{ isRunning ? 'Running' : 'Not running' }}</p>
<button @click="start()">{{ isRunning ? 'Stop' : 'Start' }}</button>
<button @click="reset()">Reset</button>
</template>
<script>
    export default {
        name:'StopWatch',
        data() {
            return{
                isRunning : false,
                seconds : 0,
                minutes:0,
                hours: 0,
                miliseconds:0,
                timer: null
            }
        },
        methods: {
           start() {
            if(!this.isRunning) {
                this.timer = setInterval(this.updatetime, 33);
            } else {
                clearInterval(this.timer)
            }
            this.isRunning = !this.isRunning;
           },
           reset() {
            clearInterval(this.timer);
            this.minutes = 0;
            this.hours=0;
            this.seconds=0;
            this.isRunning = false;
           },
           updatetime() {
            this.miliseconds +=33;
            if(this.miliseconds >=1000){
                this.seconds ++;
                this.miliseconds -=1000;
                if(this.seconds==60) {
                    this.minutes++;
                    this.seconds =0;
                    if(this.minutes==60) {
                        this.hours ++;
                        this.minutes =0;
                    }
                }
            }
           }
        }
    }
</script>