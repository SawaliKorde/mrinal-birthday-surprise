<template>
  <div class="text-center p-8 bg-white/80 backdrop-blur-sm rounded-lg border-4 border-gray-600 shadow-lg max-w-lg mx-auto">
    <img src="/hero_image.jpg" alt="Us" class="w-40 h-40 rounded-md mx-auto object-cover border-4 border-gray-600 -mt-24">
    
    <h1 class="text-3xl text-gray-800 mt-6 leading-relaxed">A Birthday Quest for Mrinal</h1>
    <p class="mt-4 text-gray-600 text-sm">An adventure created just for you. Are you ready?</p>
    
    <NuxtLink to="/game">
      <button class="mt-8 px-6 py-4 bg-green-600 text-white text-lg font-bold border-2 border-b-8 border-green-800 rounded-md hover:bg-green-500 active:border-b-2 active:mt-9 transition-all duration-100">
        Start Quest
      </button>
    </NuxtLink>
  </div>
</template>