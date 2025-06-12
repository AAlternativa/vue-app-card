<script setup>
import Button from './Button.vue';
import IconsLocation from '../icons/IconsLocation.vue';
import { ref } from 'vue';

const emit = defineEmits({
    selectCity(payload) {
        console.log(`validating payload: ${payload}`);
        return payload
    }
})

let isEdited = ref(false);

function select() {
    isEdited.value = false;
    emit('selectCity', 'London gondon')
}
function edit() {
    isEdited.value = true;
}

</script>

<template>
    {{ isEdited }}
    <div v-if="!isEdited">
        <Button @click="edit()">
            <IconsLocation />
            Изменить город
        </Button>
    </div>
    <div v-else>
        <input type="text">
        <Button @click="select()">
            Сохранить
        </Button>
    </div>

</template>