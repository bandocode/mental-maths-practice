<template>

<div>
    <span>{{operation}}</span>
    <span>{{number}}</span>
</div>


</template>

<script>
export default{
    name: 'Number',
    props: ['operation', 'number']
}
</script>


<style scoped>

div {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    font-size: 3.5rem;
    font-family: 'Poppins', 'Courier New', Courier, monospace;
    font-weight: 600;
    color: white;
    height: 65px;
    border-bottom: 1px solid var(--highlight);
    align-items: center;
}

</style>