<template>
    <div id="app">
        <Demo1 msg="llllllllllllll"/>
        <FormSubmit/>
    </div>
</template>

<script>
    import Demo1 from './components/demo1.vue'
    import FormSubmit from './components/FormSubmit.vue'
    export default {
        name       : 'app',
        components : {
            Demo1,
            FormSubmit
        }
    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
