<template>
    <div @mouseenter="$emit('mouseenter')" @mouseout="$emit('mouseout')">
        <button class="carousel-control left" @click="$emit('prev')">Prev</button>
    </div>
    <div @mouseenter="$emit('mouseenter')" @mouseout="$emit('mouseout')">
        <button class="carousel-control right" @click="$emit('next')">Next</button>
    </div>
</template>

<script>
    emits: ['prev', 'next', 'mouseenter', 'mouseout']
</script>
<style>
.carousel-control{
    background-color: rgba(0, 0, 0, 0.5);
    border: none;
    display: inline-block;
    position: absolute;
    height: 50px;
    width: 70px;
    top: calc(50% - 25px);
    color: #f3f3f3;
    cursor: pointer;
}

.left {
    left: 0; 
}

.right {
    right: 0;
}
</style>