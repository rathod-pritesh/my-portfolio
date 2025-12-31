<script>
  import { onMount } from "svelte";
  import * as THREE from "three";

  let container;

  onMount(() => {
    // Scene
    const scene = new THREE.Scene();

    const camera = new THREE.PerspectiveCamera(
      60,
      window.innerWidth / window.innerHeight,
      0.1,
      1000
    );
    camera.position.z = 5;

    const renderer = new THREE.WebGLRenderer({
      alpha: true,
      antialias: true
    });

    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

    container.appendChild(renderer.domElement);

    // Lights
    const ambient = new THREE.AmbientLight(0xffffff, 0.4);
    scene.add(ambient);

    // BackLight
    const backLight = new THREE.PointLight(0x00ffff, 1);
    backLight.position.set(-3, -3, -3);
    scene.add(backLight);

    const directional = new THREE.DirectionalLight(0xffffff, 1);
    directional.position.set(3, 5, 3);
    scene.add(directional);

    // Object
    const geometry = new THREE.SphereGeometry(1.2, 64, 64);

    const material = new THREE.MeshStandardMaterial({
      color: 0x00ffff,
      roughness: 0.3,
      metalness: 0.1
    });

    const sphere = new THREE.Mesh(geometry, material);
    scene.add(sphere);

    // Particles
    const particleCount = 200;
    const particlesGeometry = new THREE.BufferGeometry();

    const positions = new Float32Array(particleCount * 3);

    for (let i = 0; i < particleCount *3; i++) {
      positions[i] = (Math.random() - 0.5) * 10;
    }

    particlesGeometry.setAttribute(
      "position",
      new THREE.BufferAttribute(positions, 3)
    );

    const particlesMaterial = new THREE.PointsMaterial({
      color: 0x00ffff,
      size: 0.03,
      transparent: true,
      opacity: 0.7,
    });

    const particles = new THREE.Points(particlesGeometry, particlesMaterial);
    scene.add(particles);

    // Animation
    let t = 0;
    function animate() {
      requestAnimationFrame(animate);

      t += 0.01;
      sphere.position.y = Math.sin(t) * 0.25;
      sphere.rotation.y += 0.002;

      particles.rotation.y += 0.0005;
      particles.rotation.x += 0.0002;
      
      renderer.render(scene, camera);
    }

    animate();

    const resize = () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    };

    window.addEventListener("resize", resize);
  });
</script>

<div bind:this={container} class="absolute inset-0"></div>