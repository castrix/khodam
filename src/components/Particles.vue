<script setup lang="ts">
defineProps < { links: string } > ()
</script>

<template>
  <vue-particles id="tsparticles" :options="{
    background: {
      color: {
        value: '#000000',
        opacity: 0.5
      },
      opacity: 0.5
    },
    fpsLimit: 120,
    interactivity: {
      events: {
        onClick: {
          enable: true,
          mode: 'push'
        },
        onHover: {
          enable: true,
          mode: 'repulse'
        },
      },
      modes: {
        bubble: {
          distance: 400,
          duration: 2,
          opacity: 0.8,
          size: 40
        },
        push: {
          quantity: 4
        },
        repulse: {
          distance: 200,
          duration: 0.4
        }
      }
    },
    particles: {
      color: {
        value: links
      },
      links: {
        color: links,
        distance: 150,
        enable: true,
        opacity: 1,
        width: 1
      },
      move: {
        direction: 'none',
        enable: true,
        outModes: 'bounce',
        random: false,
        speed: 6,
        straight: false
      },
      number: {
        density: {
          enable: true,
        },
        value: 300
      },
      opacity: {
        value: 1
      },
      shape: {
        type: 'circle'
      },
      size: {
        value: { min: 1, max: 5 }
      }
    },
    detectRetina: true
  }" />
</template>