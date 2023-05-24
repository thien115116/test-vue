<template lang="">
  <div>
    <video ref="videoObject"></video>
    <span>{{qrCodeContent}}</span>
  </div>
</template>
<script>
import QrScanner from "qr-scanner";

export default {
  data() {
    return {
      qrCodeContent: "",
    };
  },
  mounted() {
    this.qrScanner = new QrScanner(this.$refs.videoObject, this.handleQrScan, {
      onDecodeError: (error) => {
        if (error === "No QR code found") return;
      },
      highlightScanRegion: true,
      highlightCodeOutline: true,
      preferredCamera: "environment",
    });

    setTimeout(() => {
      this.qrScanner.start();
    }, 3000);
  },
  methods: {
    handleQrScan(result) {
      console.log(result);
      this.qrCodeContent = result.data;
    },
  },
};
</script>
