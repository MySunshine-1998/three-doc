<script setup>
import * as THREE from "three";
import { OrbitControls } from "three/addons/controls/OrbitControls.js";

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(
  45,
  window.innerWidth / window.innerHeight,
  0.1,
  1000
);
const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
renderer.setClearColor(new THREE.Color(0x000000));
renderer.shadowMap.enabled = true
document.body.appendChild(renderer.domElement);
camera.position.set(-30, 40, 30);
camera.lookAt(scene.position);


// 添加坐标轴
const axes = new THREE.AxesHelper(20);
scene.add(axes);


// 添加平面
const planeGemotry = new THREE.PlaneGeometry(60, 20);
const planeMaterial = new THREE.MeshStandardMaterial({
    color: 0x00ff00, // 绿色
    roughness: 0.5, // 粗糙度
    metalness: 0, // 金属度
});
const plane = new THREE.Mesh(planeGemotry, planeMaterial);
plane.rotation.x = -0.5 * Math.PI;
plane.position.set(15, 0, 0);
plane.receiveShadow = true
scene.add(plane);

// 制作方块
const geometry = new THREE.BoxGeometry(4, 4, 4);
const material = new THREE.MeshLambertMaterial({
  color: 0xff0000,
//   wireframe: true
});
const cube = new THREE.Mesh(geometry, material);
cube.position.set(-4, 3, 0);
scene.add(cube);

// 制作球体
const sphereGeometry = new THREE.SphereGeometry(4, 20, 20);
const sphereMaterial = new THREE.MeshStandardMaterial({
    color: 0x00ff00, // 绿色
    roughness: 0.5, // 粗糙度
    metalness: 0, // 金属度
//   wireframe: true
});
const sphere = new THREE.Mesh(sphereGeometry, sphereMaterial);
sphere.position.set(20, 4, 2);
scene.add(sphere);

// 添加光照
// const spotLight = new THREE.SpotLight(0xFFFFFF);
// spotLight.position.set(-40, 40, -15);
// spotLight.castShadow = true;
// spotLight.shadow.mapSize = new THREE.Vector2(1024, 1024)
// spotLight.shadow.camera.far = 130
// spotLight.shadow.camera.near = 40
// scene.add(spotLight)

const ambientLight = new THREE.AmbientLight(0xffffff, 0.4);
scene.add(ambientLight);




const controls = new OrbitControls(camera, renderer.domElement);
controls.update();

function animate() {
  requestAnimationFrame(animate);

  controls.update();
  renderer.render(scene, camera);
}
animate();
</script>

<template></template>

<style scoped></style>
