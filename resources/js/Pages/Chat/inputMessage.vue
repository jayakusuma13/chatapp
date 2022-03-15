<template>
    <div class="relative h-10 m-1">
        <div style="border-top: 2px solid #e63636;" class="grid grid-cols-6">
            <input type="text" v-model="message" placeholder="Say something...">
            <button class="btn btn-primary" @click="addMessage()">Add Message</button>
        </div>        
    </div>
</template>

<script>
import axios from 'axios';
import Input from '../../Jetstream/Input.vue';
export default {
    props: ['room'],
    components: {
        Input,
    },

    data: function() {
        return {
            message: ''
        }
    },

    methods: {
        addMessage(){
            if(this.message == ''){
                return;
            }

            axios.post('/chat/room/' + this.room.id + '/message', {
                message: this.message
            })
            .then(response=>{
                if(response.status == 201){
                    this.message = '';
                    this.$emit('messagesent');
                }
            })
            .catch(error=>{
                console.log(error);
            })
        }
    }
}
</script>