<template>
  <Renderer ref="renderer" antialias resize :orbit-ctrl="{ enableDamping: true, dampingFactor: 0.05 }">
    <Camera ref="camera" :position="cameraPosition"></Camera>
    <Scene>
      <slot></slot>
    </Scene>
  </Renderer>
</template>

<script>
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';
import Camera from '../../core/PerspectiveCamera.js';
import Renderer from '../../core/Renderer.js';
import Scene from '../../core/Scene.js';

export default {
  components: { Camera, Renderer, Scene },
  props: {
    src: String,
    cameraPosition: Object,
  },
  mounted() {
    this.renderer = this.$refs.renderer;

    const loader = new GLTFLoader();
    loader.load(this.src, (gltf) => {
      this.renderer.three.scene.add(gltf.scene);
    });
  },
};
</script>
