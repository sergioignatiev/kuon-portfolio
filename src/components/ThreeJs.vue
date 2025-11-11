<template>
  <div class="divCenter pt-20">
    <div
      id="threejs-container"
      :style="
        windowWidth < 1280
          ? null
          : {
              'padding-left': paddingValue - 50 + 'px',
              'padding-right': paddingValue - 50 + 'px'
            }
      "
    />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import * as THREE from 'three';
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls';
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader';
import { RoomEnvironment } from 'three/examples/jsm/environments/RoomEnvironment';

const props = defineProps({
	paddingValue: {
		type: Number,
		default: 0
	}
});

const windowWidth = ref(window.innerWidth);

onMounted(() => {
	const isInDesktop = window.innerWidth > 1148;
	const userPlatform = (platform) => (platform ? 5 : 3);

	const camera = new THREE.PerspectiveCamera(75, 2, 0.1, 1000);
	camera.position.set(30, 20, 30);

	const scene = new THREE.Scene();

	const container = document.getElementById('threejs-container');
	const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
	renderer.setPixelRatio(window.devicePixelRatio);
	renderer.setSize(450, 225);
	renderer.outputEncoding = THREE.sRGBEncoding;
	renderer.shadowMap.enabled = true;
	renderer.shadowMap.type = THREE.PCFSoftShadowMap;
	renderer.setClearColor(0x000000, 0);
	container.appendChild(renderer.domElement);

	const pmremGenerator = new THREE.PMREMGenerator(renderer);
	scene.environment = pmremGenerator.fromScene(
		new RoomEnvironment(),
		1
	).texture;

	const light = new THREE.DirectionalLight(0x404040, 1);
	light.position.set(15, 20, 0);
	light.target.position.set(0, 0, 0);
	light.castShadow = true;
	light.shadow.mapSize.set(512, 512);
	scene.add(light);
	scene.add(light.target);

	const controls = new OrbitControls(camera, renderer.domElement);
	controls.enableDamping = true;
	controls.maxPolarAngle = Math.PI / 2 - 0.3;
	controls.minDistance = 10;
	controls.maxDistance = 50;
	controls.enableRotate = true;
	controls.rotateSpeed = 0.3;
	controls.autoRotate = true;
	controls.autoRotateSpeed = 1.5;

	const loader = new GLTFLoader();
	loader.load(
		'./web/source/laptop.glb',
		(gltf) => {
			const model = gltf.scene;
			model.position.set(0, 0, 6);
			model.scale.setScalar(userPlatform(isInDesktop));
			model.castShadow = true;
			scene.add(model);
		},
		undefined,
		() => {
			// fallback route if model fails to load
			window.location.href = '/notfound';
		}
	);

	const animate = () => {
		requestAnimationFrame(animate);
		camera.aspect = window.innerWidth / window.innerHeight;
		camera.updateProjectionMatrix();
		renderer.setSize(window.innerWidth / 2, window.innerHeight / 2);
		controls.update();
		renderer.render(scene, camera);
	};

	animate();
});
</script>

<style scoped>
  #threejs-container {
    width: 100%;
    height: 50%;
    display: flex;
    justify-content: center;
    text-align: center;
  }

  #threejs-container > canvas {
    display: inline;
  }

  #loading {
    border: 10px solid #f3f3f3;
    border-top: 10px solid var(--text);
    border-radius: 50%;
    width: 80px;
    height: 80px;
    animation: spin 1s linear infinite;
  }
</style>
