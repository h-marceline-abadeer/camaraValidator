<template>
  <div>
    <video ref="video" autoplay playsinline></video>
    <button @click="capturar">📷 Tomar Foto</button>
    <canvas ref="canvas" style="display: none;"></canvas>
  </div>
</template>

<script>
export default {
  mounted() {
    navigator.mediaDevices.getUserMedia({ video: true })
      .then(stream => {
        this.$refs.video.srcObject = stream
      })
      .catch(err => {
        console.error('Error al acceder a la cámara:', err)
      })
  },
  methods: {
    capturar() {
      const video = this.$refs.video
      const canvas = this.$refs.canvas
      canvas.width = video.videoWidth
      canvas.height = video.videoHeight
      canvas.getContext('2d').drawImage(video, 0, 0)
      const imagen = canvas.toDataURL('image/png')
      console.log('Foto capturada:', imagen)
      // Aquí puedes enviar la imagen a MediaPipe o al backend
    }
  }
}
</script>
