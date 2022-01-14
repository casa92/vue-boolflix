<template>
    <header>
        <input v-model="userInput" type="text">
        <button @click="$emit('inputRefresh', userInput)">Cerca</button>
    </header>
</template>

<script>

export default {
    name: "Header",
    data: function() {
        return {
            userInput: '',
        }
    }
}
</script>