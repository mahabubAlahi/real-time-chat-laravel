<template>  

    <div class="grid grid-cols-2">
        <div class="font-bold text-xl">
            {{ selected.name }} Chat
        </div>
        <div>
            <select
              v-model="selected"
              @change="$emit('roomchanged', selected)"
              class="float-right"
            >
                <option
                  v-for="(room, index) in rooms"
                  :key="index"
                  :value="room"
                >
                    {{ room.name }}
                </option>
            </select>
        </div>
        
    </div>

</template>

<script>
import { createDOMCompilerError } from '@vue/compiler-dom';

export default {
    props: ['rooms', 'currentRoom'],
    data: function () {
        return {
            selected: ''
        }
    },
    created() {
        this.selected = this.currentRoom;
    }
}

</script>