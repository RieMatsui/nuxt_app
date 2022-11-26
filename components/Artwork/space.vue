<template>
    <div class="content">
        <v-card elevation="2">
            <!--idではなくrefで指定-->
            <div ref="canvas"></div>
        </v-card>
    </div>
</template>

<script>
import * as THREE from 'three';
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";
export default {
    data() {
        let scene = new THREE.Scene
        let camera = new THREE.PerspectiveCamera(
            50,
            window.innerWidth / window.innerHeight,
            0.1,
            1000
        );
        // レンダラーを追加する
        let renderer = new THREE.WebGLRenderer({ alpha: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(window.devicePixelRatio);
        document.body.appendChild(renderer.domElement);

        // テクスチャーを追加
        let earthTexture = new THREE.TextureLoader().load("../../textures/earth.jpg");
        let moonTexture = new THREE.TextureLoader().load("../../textures/moon.png");

        // 地球のジオメトリを作成
        let earthGeometory = new THREE.SphereGeometry(100, 64, 32)
        // 月のジオメトリを作成
        let moonGeometory = new THREE.SphereGeometry(20, 64, 32)

        // マテリアルを作成
        let earthMerial = new THREE.MeshPhysicalMaterial({ map: earthTexture });
        let earthMesh = new THREE.Mesh(earthGeometory, earthMerial);

        // マテリアルを作成
        let moonMerial = new THREE.MeshPhysicalMaterial({ map: moonTexture });
          // メッシュ化する
        let moonMesh = new THREE.Mesh(moonGeometory, moonMerial);

        // 光原を追加
        let derectionalLight = new THREE.DirectionalLight(0xffffff, 2);

        camera.position.set(0, 0, +500);
        moonMesh.position.set(-200, -200, -200)
        derectionalLight.position.set(1, 1, 1);

        scene.add(earthMesh);
        scene.add(moonMesh);
        scene.add(derectionalLight);

        return {
            scene: scene,
            camera: camera,
            renderer: renderer,
            derectionalLight: derectionalLight,
            earthMesh: earthMesh,
            moonMesh: moonMesh,
        }
    },
    mounted() {
        this.camera.updateProjectionMatrix();
        let controls = new OrbitControls(this.camera, this.renderer.domElement);
        this.renderer.render(this.scene, this.camera);
        this.$refs.canvas.appendChild(this.renderer.domElement);
    }
}
</script>

<style>
.canvas {
    margin: 0;
    width: 100%;
    height: 100%;
    background-image: url('../../static/images/space.jpg');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
}
</style>