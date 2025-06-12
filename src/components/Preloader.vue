<template>
    <div class="fixed inset-0 bg-black flex items-center justify-center z-50">
        <canvas ref="canvas" class="w-full h-full"></canvas>
    </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import * as THREE from 'three'

const canvas = ref(null)

onMounted(() => {
    const scene = new THREE.Scene()
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
    const renderer = new THREE.WebGLRenderer({ canvas: canvas.value, alpha: true })
    renderer.setSize(window.innerWidth, window.innerHeight)

    const geometry = new THREE.BoxGeometry()
    const material = new THREE.MeshStandardMaterial({ color: 0x00ffcc })
    const cube = new THREE.Mesh(geometry, material)
    scene.add(cube)

    const light = new THREE.DirectionalLight(0xffffff, 1)
    light.position.set(1, 1, 1).normalize()
    scene.add(light)

    camera.position.z = 3

    const animate = () => {
        requestAnimationFrame(animate)
        cube.rotation.x += 0.01
        cube.rotation.y += 0.01
        renderer.render(scene, camera)
    }

    animate()
})

</script>