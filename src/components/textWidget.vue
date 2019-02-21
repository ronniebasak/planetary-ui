<template>
    <div class="text-widget">
        <slot>
        </slot>
    </div>
</template>

<style lang="scss" scoped>
    .text-widget {
        // background: blue;
        width: 60%;
        position: absolute;
        margin-top: 25vw;
        margin-left: 5vw;
        text-align: left;
        font-family: 'Source Sans pro';
        font-weight: bold;
        font-size: xx-large;
        color: #e9e9e9;
    }
</style>

<script>
export default {
    name: 'textWidget',
    props: {
        
    }
}
</script>
