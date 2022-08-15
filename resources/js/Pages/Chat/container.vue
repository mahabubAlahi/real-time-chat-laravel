<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import messageContainer from './messageCotainer.vue';
import inputMessage from './inputMessage.vue';
import axios from 'axios';
</script>

<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Chat
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                    <message-container :messages="messages" />
                    <input-message 
                       :rooms="currentRoom"
                       v-on:messagesent="getMessages()"
                       />
                </div>
            </div>
        </div>
    </AppLayout>
</template>

<script>
export default {
    data: function () {
        return {
            chatRooms: [],
            currentRoom: [],
            messages: []
        }
    },
    methods: {
        getRooms() {
            axios.get('/chat/rooms')
                .then(response => {
                    this.chatRooms = response.data;
                    //console.log(response.data)
                    this.setRoom (response.data[0]);
                })
                .catch(err => {
                    console.log(err)
                })
        },
        setRoom (room){
            this.currentRoom = room;
            this.messages = this.getMessages();
        },
        getMessages() {
            axios.get('/chat/room/' + this.currentRoom.id + '/messages')
             .then(response => {
                this.messages = response.data;
             })
             .catch(err => {
                console.log(err)
             })
        }
    },
    created(){
        this.getRooms();
    }
}
</script>
