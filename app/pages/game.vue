<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';

// --- SETUP ---
type Ingredient = 'sugar' | 'wheat' | 'milk';

interface Memory {
  found: boolean;
  photo: string;
  message: string;
}

const router = useRouter();

// --- STATE MANAGEMENT (Your clean logic) ---
const memories: Record<Ingredient, Memory> = {
  sugar: { found: false, photo: '/memory_1.jpg', message: 'For all our sweet moments, like this one!' },
  wheat: { found: false, photo: '/memory_2_blr.jpg', message: 'To celebrate our growth together.' },
  milk: { found: false, photo: '/memory_3_kerala.jpg', message: 'For the comfort and care we always share.' },
};

const collectedItems = ref<Ingredient[]>([]);
const grid = ref<Ingredient[]>([]); // This is our simple array for the grid's logic
const activeMemory = ref<Memory | null>(null);
const openingChest = ref<Ingredient | null>(null);

// --- FUNCTIONS (Your clean logic + navigation) ---

// Chest open logic
function openChest(item: Ingredient) {
  if (memories[item].found || openingChest.value) return;

  openingChest.value = item;

  setTimeout(() => {
    memories[item].found = true;
    if (!collectedItems.value.includes(item)) {
      collectedItems.value.push(item);
    }
    activeMemory.value = memories[item];
    openingChest.value = null;
  }, 1000);
}

function closeMemory() {
  activeMemory.value = null;
}

// Move item from inventory → grid logic
function placeInGrid(item: Ingredient) {
  if (grid.value.length >= 9) return; // Prevent adding more than 9 items
  
  const idx = collectedItems.value.indexOf(item);
  if (idx > -1) {
    collectedItems.value.splice(idx, 1); // remove from inventory
    grid.value.push(item); // add to our simple grid array
  }
  checkRecipe();
}

// Reset grid logic
function resetGrid() {
  collectedItems.value.push(...grid.value);
  grid.value = [];
}

// Check recipe and navigate on success
function checkRecipe() {
  const unique = new Set(grid.value);

  // If all 3 unique ingredients are in the grid, it's a success!
  if (grid.value.length === 3 && unique.size === 3) {
    // Navigate to the grand finale page!
    router.push('/finale');
  }
}
</script>

<template>
  <div class="p-6 bg-white/80 backdrop-blur-sm rounded-lg border-4 border-gray-600 shadow-lg max-w-3xl mx-auto text-center">
    
    <div v-if="activeMemory" class="fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center z-50 p-4">
      <div class="bg-white p-6 rounded-lg text-center border-4 border-gray-600">
        <h3 class="text-xl mb-4">You found an ingredient!</h3>
        <img :src="activeMemory.photo" class="w-64 h-64 object-cover rounded-md mx-auto border-4 border-gray-500" />
        <p class="mt-4 italic">"{{ activeMemory.message }}"</p>
        <button @click="closeMemory" class="mt-6 px-4 py-2 bg-blue-500 text-white rounded-md border-2 border-b-4 border-blue-700 active:border-b-2">Close</button>
      </div>
    </div>

    <h2 class="text-2xl mb-4">Craft a Birthday Cake!</h2>
    <p class="text-sm mb-6">Click the chests to find the ingredients.</p>

    <div class="flex justify-center gap-8 mb-8">
      <div @click="openChest('sugar')" class="cursor-pointer">
        <img :src="openingChest==='sugar' ? '/chest-animation.gif' : (memories.sugar.found ? '/chest-open.jpg' : '/chest-closed.png')" 
             class="w-24 h-24" style="image-rendering: pixelated;" />
      </div>
      <div @click="openChest('wheat')" class="cursor-pointer">
        <img :src="openingChest==='wheat' ? '/chest-animation.gif' : (memories.wheat.found ? '/chest-open.jpg' : '/chest-closed.png')" 
             class="w-24 h-24" style="image-rendering: pixelated;" />
      </div>
      <div @click="openChest('milk')" class="cursor-pointer">
        <img :src="openingChest==='milk' ? '/chest-animation.gif' : (memories.milk.found ? '/chest-open.jpg' : '/chest-closed.png')" 
             class="w-24 h-24" style="image-rendering: pixelated;" />
      </div>
    </div>

    <div v-if="memories.sugar.found && memories.wheat.found && memories.milk.found" class="mt-6 border-t-4 border-gray-400 pt-6">
      <h3 class="text-xl mb-4">Inventory</h3>
      <div class="flex gap-2 p-2 bg-gray-300 border-2 border-gray-500 rounded min-h-[72px] justify-center">
        <p v-if="collectedItems.length === 0" class="text-gray-500 text-xs self-center">Drag items to the grid!</p>
        <img v-for="item in collectedItems" :key="item" @click="placeInGrid(item)"
             :src="`/${item}${item==='milk' ? '-bucket' : ''}.png`"
             class="w-12 h-12 p-1 cursor-pointer hover:bg-blue-200"
             style="image-rendering: pixelated;" />
      </div>
    </div>

    <div v-if="memories.sugar.found && memories.wheat.found && memories.milk.found" class="mt-8">
      <h3 class="text-xl mb-4 animate-bounce">Crafting Table</h3>
      <p class="text-xs mb-4">Click inventory items to place them in the grid.</p>
      
      <div class="grid grid-cols-3 gap-1 bg-gray-400 p-1 border-4 border-gray-600 w-max mx-auto">
        <div v-for="i in 9" :key="i" class="w-16 h-16 bg-gray-300 flex items-center justify-center">
            <img v-if="grid[i-1]" :src="`/${grid[i-1]}${grid[i-1]==='milk' ? '-bucket' : ''}.png`" class="w-12 h-12" style="image-rendering: pixelated;">
        </div>
      </div>

      <button @click="resetGrid" class="mt-4 px-3 py-1 bg-red-500 text-white text-xs rounded-md border-b-4 border-red-700 active:border-b-2">
        Clear Grid
      </button>
    </div>
    
  </div>
</template>