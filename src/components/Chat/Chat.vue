<script setup>
    //import ref
    import { ref, reactive, onMounted } from 'vue';

    let message = ref(""); //je gebruik ref voor int, string, boolean
                                   //je gebruikt {{ }} voor printen
    let allMessages= reactive({
        data: [],
    }); //je gebruikt reactive voor array en object

    //function onMounted  
    onMounted(async() => {
       await fetchMessages();
    });

    //function fetchMessages
    const fetchMessages = async() => {
        const response = await fetch("https://lab5-p379.onrender.com/api/v1/messages/");
        const data = await response.json();
        allMessages.data = data;
    }


    //function sendMessage
    const SendMessage = async () => {
        const response = fetch("https://lab5-p379.onrender.com/api/v1/messages/", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({
                value: message.value,
            }),
        });

        const newMessage = await response.json();
        allMessages.data.push(newMessage); // Add the new message to the end
        message.value = ""; // Clear the input
    };

</script>

<template>
    <div>
        <ul>
            <li v-for="m in allMessages.data" :key="m.id">{{ m.text }}</li> 
        </ul>
        <div>
            <input v-model="message" type="text" placeholder="">
            <button @click="SendMessage">Send</button>
        </div>
    </div>
</template>

<style scoped>

</style>