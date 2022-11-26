<template>
    <div class="content">
        <v-card elevation="2">
            <!--idではなくrefで指定-->
            <div class="canvas" ref="myCanvas"></div>
        </v-card>
    </div>
</template>

<style>
    .canvas {
        margin: 0;
        width:320px;
        height:240px;
        background-image: url('../../static/images/space.jpg');
        background-size: cover;
        background-position: center;
        background-repeat: no-repeat;
    }
</style>