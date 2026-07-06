<script setup lang="ts">
import InteractiveCard from './components/InteractiveCard.vue'
import { Sparkles, MonitorPlay } from 'lucide-vue-next'
</script>

<template>
  <div class="relative min-h-screen w-full bg-slate-950 text-slate-100 flex flex-col items-center justify-center p-6 sm:p-12 overflow-hidden">
    
    <!-- ฉากหลังเรืองแสงพรีเมียม (Glow Background Blobs) -->
    <div class="absolute top-1/4 left-1/4 -translate-x-1/2 -translate-y-1/2 w-[350px] sm:w-[500px] h-[350px] sm:h-[500px] bg-purple-600/10 rounded-full blur-[100px] sm:blur-[150px] pointer-events-none"></div>
    <div class="absolute bottom-1/4 right-1/4 translate-x-1/2 translate-y-1/2 w-[350px] sm:w-[500px] h-[350px] sm:h-[500px] bg-indigo-600/10 rounded-full blur-[100px] sm:blur-[150px] pointer-events-none"></div>

    <!-- เส้นไกด์ตารางล้ำๆ ด้านหลัง (Grid Overlay) -->
    <div class="absolute inset-0 bg-[linear-gradient(to_right,#ffffff02_1px,transparent_1px),linear-gradient(to_bottom,#ffffff02_1px,transparent_1px)] bg-[size:32px_32px] pointer-events-none"></div>

    <!-- โครงสร้างหลักสำหรับการพรีเซนต์ -->
    <main class="relative z-10 w-full max-w-5xl flex flex-col items-center space-y-12 sm:space-y-16">
      
      <!-- ส่วนหัวข้อหลักพร้อมแอนิเมชันของ Motion -->
      <header 
        v-motion
        :initial="{ opacity: 0, y: -40 }"
        :enter="{ opacity: 1, y: 0, transition: { duration: 800, type: 'keyframes', ease: 'easeOut' } }"
        class="text-center space-y-4"
      >
        <!-- ป้ายกำกับเฟส -->
        <div class="inline-flex items-center gap-2 px-3 py-1.5 rounded-full border border-purple-500/30 bg-purple-500/5 text-purple-400 text-xs font-mono tracking-wider shadow-sm shadow-purple-500/5 animate-pulse">
          <Sparkles class="w-3.5 h-3.5" />
          <span>PHASE 2: PREMIUM TECH-STACK ACTIVE</span>
        </div>

        <h1 class="text-4xl sm:text-6xl font-black tracking-tight leading-none">
          สัมผัสความหรูหราผ่าน
          <span class="block mt-2 bg-gradient-to-r from-purple-400 via-pink-400 to-indigo-400 bg-clip-text text-transparent drop-shadow-sm">
            Interactive Animations
          </span>
        </h1>
        
        <p class="max-w-xl mx-auto text-slate-400 text-sm sm:text-base font-light leading-relaxed">
          ติดตั้งระบบ UI และชุดตัวช่วยด้านแอนิเมชันระดับท็อปของวงการเรียบร้อยแล้ว ทดลองนำเมาส์ไปโฮเวอร์บนการ์ดหรือกล่องทดสอบเพื่อสัมผัสการตอบสนองแบบ 60 FPS
        </p>
      </header>

      <!-- Grid แสดงการทดสอบ Component ต่างๆ -->
      <section class="grid grid-cols-1 md:grid-cols-2 gap-8 items-center w-full max-w-4xl px-4">
        
        <!-- ฝั่งซ้าย: กล่องทดสอบความสามารถของ @vueuse/motion -->
        <div 
          v-motion
          :initial="{ opacity: 0, x: -50 }"
          :enter="{ opacity: 1, x: 0, transition: { delay: 200, duration: 600 } }"
          class="flex flex-col space-y-6 p-8 rounded-2xl border border-white/5 bg-slate-900/40 backdrop-blur-md h-full justify-between"
        >
          <div class="space-y-3">
            <div class="flex items-center gap-2 text-purple-400 font-medium text-sm">
              <MonitorPlay class="w-4 h-4" />
              <span>@vueuse/motion Sandbox</span>
            </div>
            <h2 class="text-xl font-bold text-white">กล่องสปริงโต้ตอบ (Interactive Spring Box)</h2>
            <p class="text-slate-400 text-xs sm:text-sm leading-relaxed">
              กล่องสีเหลี่ยมด้านล่างใช้ระบบสปริงฟิสิกส์ (Spring Physics) ของ VueUse Motion ลองนำเมาส์ไปชี้ (Hover) หรือกดคลิกค้างไว้ (Tap/Click) เพื่อดูการตอบสนองที่นุ่มนวล
            </p>
          </div>

          <!-- กล่องตัวอย่างทดสอบ Hover / Tap -->
          <div class="py-8 flex justify-center items-center">
            <div
              v-motion
              :initial="{ scale: 1, rotate: 0 }"
              :hovered="{ scale: 1.15, rotate: 15, transition: { type: 'spring', stiffness: 200, damping: 10 } }"
              :tapped="{ scale: 0.9, rotate: -5, transition: { type: 'spring', stiffness: 300, damping: 15 } }"
              class="w-28 h-28 rounded-2xl bg-gradient-to-tr from-purple-500 via-pink-500 to-indigo-500 shadow-xl shadow-purple-500/20 cursor-pointer flex items-center justify-center text-white text-xs font-mono font-bold select-none"
            >
              Hover / Click Me
            </div>
          </div>

          <p class="text-[10px] text-slate-500 text-center font-mono">
            Spring Config: stiffness=200, damping=10
          </p>
        </div>

        <!-- ฝั่งขวา: การ์ด 3D Glow Tilt (ผสานรวม shadcn-vue และ @vueuse/core) -->
        <div 
          v-motion
          :initial="{ opacity: 0, x: 50 }"
          :enter="{ opacity: 1, x: 0, transition: { delay: 400, duration: 600 } }"
          class="flex justify-center h-full items-center"
        >
          <InteractiveCard />
        </div>

      </section>

      <!-- ฟุตเตอร์ระบุสถานะพร้อมสำหรับการทำ Storytelling -->
      <footer 
        v-motion
        :initial="{ opacity: 0 }"
        :enter="{ opacity: 1, transition: { delay: 600, duration: 800 } }"
        class="text-center pt-8 border-t border-white/5 w-full max-w-md text-xs text-slate-600 font-light"
      >
        ขับเคลื่อนโดย Vue 3 • Bun • Tailwind CSS v4 • Reka/Radix UI • VueUse Motion
      </footer>

    </main>

  </div>
</template>
