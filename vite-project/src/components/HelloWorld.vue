<script setup>
import * as THREE from 'three';
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );
camera.position.set(0, 0, 10)
camera.lookAt( 0, 0, 0 );

const renderer = new THREE.WebGLRenderer();
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );

const geometry = new THREE.BoxGeometry( 1, 1, 1 );
const material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
const cube = new THREE.Mesh( geometry, material );
scene.add( cube );

const controls = new OrbitControls( camera, renderer.domElement );
controls.update();

const lineMaterial = new THREE.LineBasicMaterial( { color: 0x0000ff } );
const points = [];
points.push( new THREE.Vector3( - 1, 0, 0 ) );
points.push( new THREE.Vector3( 0, 1, 0 ) );
points.push( new THREE.Vector3( 1, 0, 0 ) );

const lineGeometry = new THREE.BufferGeometry().setFromPoints( points );

const line = new THREE.Line( lineGeometry, lineMaterial );
scene.add(line)

function animate() {
	requestAnimationFrame( animate );

  controls.update();
	renderer.render( scene, camera );
}
animate();


</script>

<template>
</template>

<style scoped>

</style>
