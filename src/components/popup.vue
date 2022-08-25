<template>
    <div class="popup">
        <div class="popup-inner">
            <slot />
            
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            
        }
    }
</script>

<style scoped>
.popup {
    position: fixed;
    left: 0;
    right: 0;
    bottom: 0;
    top:0;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
}

.popup-inner {
    background-color: white;
    padding: 2em;
    display: block;
}

</style>