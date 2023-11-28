<script setup>
    //import ref
    import { ref, reactive, onMounted } from 'vue';

    let message = ref(""); //je gebruik ref voor int, string, boolean
                                   //je gebruikt {{ }} voor printen
    let allMessages= reactive({
        data: [],
    }); //je gebruikt reactive voor array en object

     // my own username
     const myUsername = "Britt";

    // Fetch all messages when the component is mounted
    onMounted(async () => {
        const response = await fetch("https://lab5-p379.onrender.com/api/v1/messages/");
        const data = await response.json();
        allMessages.data = data;
    }); 

    //function SendMessage
    const SendMessage = async () => {
        const newMessage ={
            user: myUsername,
            text: message.value,
        }
    const response = await fetch("https://lab5-p379.onrender.com/api/v1/messages/", {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
        },
        body: JSON.stringify(newMessage),
    });

    //console.log('Response:', response);
     //console.log('New Message:', newMessage);

    allMessages.data.push(newMessage);// Add the new message to the array
    message.value = ""; // Clear the input
};

</script>

<template>
    <div>
        <ul>
            <li v-for="m in allMessages.data" :key="m.id">{{ m.user}}: {{ m.text }}</li> 
        </ul>
        <div>
            <input v-model="message" type="text" placeholder="">
            <button @click="SendMessage">Send</button>
        </div>
    </div>
</template>


<style scoped>

</style>