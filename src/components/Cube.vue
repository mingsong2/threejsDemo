<script setup lang="ts">
defineProps<{ msg: string }>();

import { ref, onMounted } from 'vue';
import * as THREE from 'three';

const threeContainer = ref(null);

onMounted(() => {
  // 场景
  const scene = new THREE.Scene();
  // 透视相机设置
  const camera = new THREE.PerspectiveCamera(
    75,
    window.innerWidth / window.innerHeight,
    0.1,
    1000
  );
  // 渲染器设置
  const renderer = new THREE.WebGLRenderer();
  renderer.setSize(window.innerWidth / 2, window.innerHeight / 2);
  threeContainer.value.appendChild(renderer.domElement);
  const geometry = new THREE.BoxGeometry(1, 1, 1);
  const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
  const cube = new THREE.Mesh(geometry, material);
  scene.add(cube);
  camera.position.z = 3;

  function animate() {
    requestAnimationFrame(animate);

    cube.rotation.x += 0.01;
    cube.rotation.y += 0.01;

    renderer.render(scene, camera);
  }
  animate();
});
const count = ref(0);
</script>

<template>
  <div ref="threeContainer"></div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
