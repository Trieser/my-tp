<template>
  <div class="fixed inset-0 bg-black text-white z-50">
    <canvas ref="canvas" class="absolute w-full h-full"></canvas>

    <div class="relative z-10 flex flex-col items-center justify-center h-full text-center">
      <h1 class="text-2xl font-light tracking-widest text-blue-400 animate-fade">
        Dmitrie Entertainment System
      </h1>
      <p class="text-xl font-mono mt-4 animate-pulse">Loading {{ progress }}%</p>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import * as THREE from "three";

const emit = defineEmits(["done"]);
const canvas = ref(null);
const progress = ref(0);

onMounted(() => {
  const scene = new THREE.Scene();
  scene.fog = new THREE.FogExp2(0x000000, 0.08);

  const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
  camera.position.z = 4;

  const renderer = new THREE.WebGLRenderer({
    canvas: canvas.value,
    alpha: false,
    antialias: true,
  });
  renderer.setSize(window.innerWidth, window.innerHeight);
  renderer.setPixelRatio(window.devicePixelRatio);

  const geometry = new THREE.BufferGeometry();
  const count = 150;
  const positions = [];
  for (let i = 0; i < count; i++) {
    positions.push(
      (Math.random() - 0.5) * 10,
      (Math.random() - 0.5) * 10,
      (Math.random() - 0.5) * 10
    );
  }
  geometry.setAttribute("position", new THREE.Float32BufferAttribute(positions, 3));

  const material = new THREE.PointsMaterial({
    color: 0x44ccff,
    size: 0.1,
    transparent: true,
    opacity: 0.6,
  });

  const points = new THREE.Points(geometry, material);
  scene.add(points);

  // gradient-like black to dark blue overlay
  const overlayGeometry = new THREE.PlaneGeometry(20, 20);
  const overlayMaterial = new THREE.MeshBasicMaterial({
    color: 0x000022,
    transparent: true,
    opacity: 0,
  });
  const overlay = new THREE.Mesh(overlayGeometry, overlayMaterial);
  overlay.position.z = 0.5;
  scene.add(overlay);

  const animate = () => {
    requestAnimationFrame(animate);
    points.rotation.y += 0.01;
    points.rotation.x += 0.01;

    // smooth fade overlay
    if (progress.value >= 100 && overlayMaterial.opacity < 1) {
      overlayMaterial.opacity += 0.02;

      
      if (overlayMaterial.opacity >= 1) {
        overlayMaterial.opacity = 1;
      }

    }

    renderer.render(scene, camera);
  };

  animate();

  let interval = setInterval(() => {
    if (progress.value < 100) {
      progress.value += 1;
    } else {
      clearInterval(interval);
      const zoomIn = () => {
        if (camera.position.z > 0.5) {
          camera.position.z -= 0.07;
          requestAnimationFrame(zoomIn);
        } else {
          emit("done");
        }
      };
      zoomIn();
    }
  }, 30);

  window.addEventListener("resize", () => {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
  });
});
</script>

<style scoped>
@keyframes fade-in-up {
  0% {
    opacity: 0;
    transform: translateY(20px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
.animate-fade {
  animation: fade-in-up 1.5s ease-out forwards;
}
</style>
