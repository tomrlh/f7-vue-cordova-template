<template>
  <f7-page>
    <f7-navbar title="Camera" back-link="Back" sliding></f7-navbar>
    <f7-block inner>
      <f7-button @click="openCamera()">Take a picture</f7-button>
    </f7-block>
  </f7-page>
</template>

<script>
export default {

  name: 'take-picture',

  data () {
    return {

    }
  },
  methods: {
    createNewFileEntry(imgUri) {
      window.resolveLocalFileSystemURL(cordova.file.cacheDirectory, function success(dirEntry) {

          // JPEG file
          dirEntry.getFile("tempFile.jpeg", { create: true, exclusive: false }, function (fileEntry) {

              // Do something with it, like write to it, upload it, etc.
              // writeFile(fileEntry, imgUri);
              console.log("got file: " + fileEntry.fullPath);
              // displayFileData(fileEntry.fullPath, "File copied to");

          }, onErrorCreateFile);

      }, onErrorResolveUrl);
    },
    setOptions(srcType) {
      var options = {
          // Some common settings are 20, 50, and 100
          quality: 50,
          destinationType: Camera.DestinationType.FILE_URI,
          // In this app, dynamically set the picture source, Camera or photo gallery
          sourceType: srcType,
          encodingType: Camera.EncodingType.JPEG,
          mediaType: Camera.MediaType.PICTURE,
          allowEdit: true,
          correctOrientation: true  //Corrects Android orientation quirks
      }
      return options;
    },
    openCamera() {
      var srcType = Camera.PictureSourceType.CAMERA;
      var options = this.setOptions(srcType);
      var func = this.createNewFileEntry;

      navigator.camera.getPicture(function cameraSuccess(imageUri) {

          displayImage(imageUri);
          // You may choose to copy the picture, save it somewhere, or upload.
          func(imageUri);

      }, function cameraError(error) {
          console.debug("Unable to obtain picture: " + error, "app");

      }, options);
    }
  }
}
</script>

<style lang="css" scoped>
</style>