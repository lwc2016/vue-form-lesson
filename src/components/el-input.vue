<template>
    <input class="input" :value="value" @input="onInput" v-bind="$attrs"  />
</template>

<script>
    export default {
        props: {
            value: {
                type: String,
                default: ""
            }
        },
        methods: {
            onInput(event){
                // 将value值传递出去
                this.$emit("input", event.target.value);
                // $parent指向FormItem
                this.$parent.$emit("validate");
            }
        }
    }
</script>

<style scoped>
    .input{
        width: 100%;
        height: 30px;
        margin: 0;
        padding: 0 10px;
        border: 1px solid #a9a9a9;
        border-radius: 4px;
        outline: none;
    }
</style>