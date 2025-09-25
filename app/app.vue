<template>
  <div 
    class="bg-cover bg-center min-h-screen font-minecraft text-gray-800 flex items-center justify-center p-4"
    style="background-image: url('/minecraft-bg.png'); image-rendering: pixelated;"
  >
    <div class="absolute inset-0 bg-black bg-opacity-30"></div>
    
    <div class="z-10">
      <NuxtPage />
    </div>
  </div>
</template>

<style>
/* Import the pixel font */
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');

body {
  /* Set the default font for the whole site */
  font-family: 'Press Start 2P', cursive;
}
</style>