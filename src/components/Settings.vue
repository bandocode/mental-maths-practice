<template>
<teleport to="body">
<div class="bg">
    <div class="animate__animated animate__bounceInUp animate__faster">
        <!-- content -->
        <div style="display:flex; flex-direction: row; height: 100%; width: 100%;">

            <!-- sidebar -->
            <div style="display: flex; height: 100%; width: 200px;" id="sidebar">
            
            </div>

            <!-- settings view -->

            <div style="display: flex; height:100%; flex:2;justify-content: center;" id="view">
            
            </div>


            
        </div>

        <button @click="$emit('close-event')">Close</button>
    </div>
</div>
</teleport>

</template>

<script>

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
    justify-content: center;
    align-items: center;
    
}

.bg > div > button {
    display: block;
    height: 35px;
    width: 100px;
    outline: none;
    border: none;
    background: none;
    color: #191a2a;
    background-color: #7e86d6;
    border-radius: 2px;
    font-family: 'Poppins', 'Courier New', Courier, monospace;
    font-weight: 600;
}


.bg > div > button:hover {
    text-decoration: underline;
    background-color: #646bab;
}




</style>