<template>
    <div class="progress-container">
        <span class="progress-value">{{ progress }}%</span>
        <div class="progress-bar" :style="{width: progress + '%'}"></div>
    </div>
</template>

<script>
export default {
    props: {
        progress: {type: Number}
    }
}
</script>

<style scoped>
    .progress-container {
        position: relative;
        width: 80%;
        border: #fff solid 1px;
        color: #FFF;
        border-radius: 8px;
        margin-bottom: 15px;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .progress-bar {
        position: absolute;
        height: 100%;
        background: #4CAF50;
        border-radius: 8px;
        align-self: flex-start;
    }

    .progress-value {
        z-index: 5;
        font-size: 1em;
    }
</style>