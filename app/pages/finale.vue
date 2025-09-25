<template>
  <div class="text-center p-8 bg-white/80 backdrop-blur-sm rounded-lg border-4 border-gray-600 shadow-lg max-w-2xl mx-auto">
    <h1 class="text-4xl text-pink-600 animate-bounce leading-relaxed">Happy Birthday Lovee!</h1>
    
    <img src="/cake.png" alt="Minecraft Cake" class="w-32 h-32 mx-auto my-4" style="image-rendering: pixelated;">
    
    <p class="mt-4 text-gray-700 text-sm leading-relaxed">
      My dearest Bubbyy,
      <br><br>
      You completed the quest! Just like in our life, you put all the right pieces together to create something wonderful.
      Thank you for building such an amazing world with me. I love you more than words can say.
      <br><br>
      Forever yours,
      <br>
      Sawali
      </p>

    <div class="mt-8 border-t-4 border-gray-400 pt-6">
      <h2 class="text-2xl text-pink-500 mb-4">Our Gallery of Moments</h2>
      <div class="grid grid-cols-2 md:grid-cols-3 gap-4">
        <img v-for="i in 6" :key="i" :src="`/gallery${i}.jpg`" class="rounded-md border-4 border-gray-600 shadow-md transform hover:scale-110 transition-transform duration-300">
      </div>
    </div>
  </div>
</template>