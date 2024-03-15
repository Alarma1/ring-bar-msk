<template>
    <div>
        <ProgressBar :value="checkInput"/>
        <input class="input-style"
               type="number"
               min="0"
               max="1"
               step="0.01"
               v-model.number="inputValue"
        />
    </div>
</template>

<script>
    import ProgressBar from "@/components/ProgressBar.vue";

    export default {
        name: "MainPage",
        components: {ProgressBar},
        data() {
            return {
                inputValue: 0.5,
            };
        },
        computed: {
            checkInput() {
                if (this.inputValue === '') {
                    return 0
                }
                return this.inputValue
            },
        }
    };
</script>

<style scoped>

    .input-style {
        width: 150px;
        margin-top: 10px;
    }

</style>
