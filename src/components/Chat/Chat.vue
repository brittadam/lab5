<script setup>
    //import ref
    import { ref, reactive, onMounted } from 'vue';

    let message = ref(""); //je gebruik ref voor int, string, boolean
                                   //je gebruikt {{ }} voor printen
    let allMessages= reactive({
        data: ["Heel", "Even", "Simpel", "Doen"],
    }); //je gebruikt reactive voor array en object

    //function sendMessage
    const SendMessage = () => {
        allMessages.data.push(message.value);
        message.value = ""; //.value is nodig bij ref
    }

</script>

<template>
    <div>
        <ul>
            <li v-for="m in allMessages.data">{{ m }}</li> 
        </ul>
        <div>
            <input v-model="message" type="text" placeholder="">
            <button @click="SendMessage">Send</button>
        </div>
    </div>
</template>

<style scoped>

</style>