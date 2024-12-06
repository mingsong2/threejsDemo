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
    65,
    window.innerWidth / window.innerHeight,
    1,
    100
  );
  camera.position.set(0, 0, 100);
  camera.lookAt(0, 0, 0);
  // 渲染器
  const renderer = new THREE.WebGLRenderer();
  renderer.setSize(window.innerWidth, window.innerHeight);
  threeContainer.value.appendChild(renderer.domElement);
  const material = new THREE.LineBasicMaterial({ color: 0x0000ff });
  const points = [];
  points.push(new THREE.Vector3(-10, 0, 0));
  points.push(new THREE.Vector3(0, 10, 0));
  points.push(new THREE.Vector3(10, 0, 0));
  const geometry = new THREE.BufferGeometry().setFromPoints(points);
  const line = new THREE.Line(geometry, material);
  scene.add(line);
  renderer.render(scene, camera);
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
