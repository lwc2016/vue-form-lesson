<template>
    <div class="form-group">
        <div class="form-label">{{label}}</div>
        <div class="form-input">
            <slot></slot>
            <p>{{errorMsg}}</p>
        </div>
    </div>
</template>

<script>
    import Validator from "standard-validator";
    export default {
        props: {
            label: {
                type: String,
                default: ""
            },
            prop: {
                type: String,
                default: ""
            }
        },
        data(){
            return {
                errorMsg: ""
            };
        },
        inject: ["form"],
        created(){
            this.$on("validate", this.validate);
        },
        methods: {
            validate(){
                return new Promise((resolve)=>{
                    if(!this.prop){
                        resolve(null);
                    }
                    const data = {[this.prop]: this.form.model[this.prop]};
                    const rule = {[this.prop]: this.form.rules[this.prop]};
                    const validator = new Validator(data, rule);
                    validator.validate((err) => {
                        if(err){
                            this.errorMsg = err[this.prop];
                            resolve(err);
                        }else{
                            this.errorMsg = "";
                            resolve(null);
                        }
                    })
                });

            }
        }
    }
</script>

<style scoped>
    .form-group{
        display: flex;
        padding: 10px;
    }
    .form-label{
        width: 80px;
        line-height: 30px;
    }
    .form-input{
        width: 240px;
    }
    p{
        margin: 0;
        padding-top: 5px;
        font-size: 14px;
        color: red;
    }
</style>