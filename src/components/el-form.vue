<template>
    <div>
        <slot></slot>
    </div>
</template>
<script>
    export default{
        provide(){
            return {
                form: this  // 将组件实例作为提供者，子代组件可方便使用
            }
        },
        props: {
            model: {
                type: Object,
                required: true
            },
            rules: {
                type: Object,
                default: () => ({})
            }
        },
        methods: {
            validate(callback){
                let promises = this.$children.map(children => children.validate && children.validate());
                Promise.all(promises).then((err)=>{
                    if(err.every(item => !item)){
                        callback(null);
                    }else{
                        const error = err.reduce((obj, item) => Object.assign(obj, item || {}), {});
                        callback(error);
                    }
                })
            }
        }
    }
</script>