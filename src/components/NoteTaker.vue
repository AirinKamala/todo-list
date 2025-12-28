<template>
    <div class="container">
        <h1>Note Taker Page</h1>
        <p>add your note</p>
        <button @click="addNote()">+</button>
        <figcaption>
            <label for="input">write your notes here </label>
            <textarea v-model="note" fixed name="input" id="input" placeholder="text here"></textarea>
        </figcaption>
        <div class="result">
            <div class="oneNote" v-for="(data, index) in notes" :key="index">{{ data }}</div>
        </div>
    </div>
</template>
<style scoped lang="scss">
.container {
    display: grid;

    p {
        font-size: 24px;
    }

    textarea {
        min-width: 80vw;
        max-width: 80vw;
        height: 20px;
        resize: none;

        &:focus {
            height: 100px;
        }
    }

    .result {
        background-color: #ababab;
        margin: 20px;
        min-height: 30px;
        border: 2px solid #3c3c3c;
        display: flex;
        flex-wrap: wrap;

        .oneNote {
            width: 100px;
            max-height: 30dvh;
            margin: 10px auto;
            border: 2px solid blue;
            background-color: white;
            border-radius: 20px;
            padding: 10px;
            justify-content: center;

        }
    }
}
</style>
<script>
import { ref } from 'vue';
export default {
    name: 'NoteTaker',
    data() {
        return {
            notes: ref([]),
            note: ref(''),
        }
    },
    methods: {
        addNote() {
            if (this.note.trim() === '') return
            this.notes.push(this.note)
            this.note = ''
        },
    },
}
</script>