<template>
    <div class="content">
        <v-card elevation="2">
            <div class="canvas" ref="canvas"></div>
        </v-card>
    </div>
</template>

<script>
import * as THREE from 'three';
export default {
    data() {
        const scene = new THREE.Scene
        const camera = new THREE.PerspectiveCamera(
            50,
            window.innerWidth / window.innerHeight,
            0.1,
            1000
        );
        // 地球のジオメトリを作成
        const earthGeometory = new THREE.SphereGeometry(100, 64, 32)
        // マテリアルを作成
        const earthMerial = new THREE.MeshStandardMaterial();
        const earthMesh = new THREE.Mesh(earthGeometory, earthMerial);

        // レンダラーを追加する
        const renderer = new THREE.WebGLRenderer({ alpha: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(window.devicePixelRatio);
        document.body.appendChild(renderer.domElement);

        // 光原を追加
        const derectionalLight = new THREE.DirectionalLight(0xffffff, 1);

        camera.position.set(0, 0, +600);
        derectionalLight.position.set(1, 1, 1);

        scene.add(derectionalLight);

        return {
            scene: scene,
            camera: camera,
            renderer: renderer,
            derectionalLight: derectionalLight,
            earthURL: require('@/assets/textures/earth.jpg'),
            moonURL: require('@/assets/textures/moon.png'),
            earthGeometory: earthGeometory,
            earthMerial: earthMerial,
            earthMesh: earthMesh,
        }
    },
    mounted() {
        this.initialize();
    },
    methods: {
        initialize() {
            // テクスチャーを追加
            this.earthMerial = new THREE.MeshStandardMaterial({ color: 0xff5555 })
            this.earthMerial.needsUpdate = true;
            this.earthMesh = new THREE.Mesh(this.earthGeometory, this.earthMerial);
            this.earthMesh.name = 'earth';

            let moonTexture = new THREE.TextureLoader().load(this.moonURL);

            // 月のジオメトリを作成
            let moonGeometory = new THREE.SphereGeometry(20, 64, 32)
            // マテリアルを作成
            let moonMerial = new THREE.MeshStandardMaterial({ color: 0xff5555 });
            // メッシュ化する
            let moonMesh = new THREE.Mesh(moonGeometory, moonMerial);

            this.scene.add(this.earthMesh);
            this.scene.add(moonMesh);
            moonMesh.position.set(-200, -200, -200)

            this.camera.updateProjectionMatrix();
            this.renderer.render(this.scene, this.camera);
            this.$refs.canvas.appendChild(this.renderer.domElement);
        },
    },
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