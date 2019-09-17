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
    html,body{
        height: 100%;
        background: #f2f2f2;
    }
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
    }
</style>
