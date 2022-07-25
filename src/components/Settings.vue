<template>
<teleport to="body">
<div class="bg">
    <div>
        <!-- content -->

        <button @click="$emit('close-event')">Close</button>

    </div>
</div>
</teleport>

</template>

<script>
import {ref} from 'vue'


export default {
    name: 'Settings',
}

</script>


<style scoped>

.bg {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    display: flex;
    justify-content: center;
    align-items: center;
}

.bg > div {
    display: flex;
    flex-direction: column;
    width: 80vw;
    height: 90vh;
    background-color: #0a0a0a;
    align-items: center;
    
}


</style>