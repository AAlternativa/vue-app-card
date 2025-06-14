<script setup>
import Input from './Input.vue';
import Button from './Button.vue';
import IconsLocation from '../icons/IconsLocation.vue';
import { onMounted, ref } from 'vue';




const emit = defineEmits({
    selectCity(payload) {
        console.log(`validating payload: ${payload}`);
        return payload
    }
})

let city = ref("Moscow")
let isEdited = ref(false);

onMounted(() => {
    emit('selectCity', city.value)
})

function select() {
    isEdited.value = false;
    emit('selectCity', city.value)
}
function edit() {
    isEdited.value = true;
}


</script>

<template>
    <div class="city-select">
        {{ city }}
        {{ isEdited }}

        <div v-show="isEdited" class="city-input">
            <Input placeholder="Никольск" v-model="city" @keyup.enter="select" />
            <Button @click="select()">
                Сохранить
            </Button>
        </div>

        <div v-show="!isEdited">
            <Button @click="edit()">
                <IconsLocation />
                Изменить город
            </Button>
        </div>

    </div>

</template>

<style scoped>
.city-input {
    display: flex;
    gap: 12px;

}

.city-select {
    width: 420px;
}
</style>