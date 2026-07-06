<script setup lang="ts">
import { ref, computed } from 'vue'
import { useMouseInElement } from '@vueuse/core'
import { Button } from '@/components/ui/button'
import { Sparkles, ArrowRight, Shield, Zap } from 'lucide-vue-next'

const target = ref<HTMLElement | null>(null)
const { elementX, elementY, elementWidth, elementHeight, isOutside } = useMouseInElement(target)

const cardStyle = computed(() => {
  if (isOutside.value) {
    return {
      transform: 'perspective(1000px) rotateX(0deg) rotateY(0deg) scale(1)',
      transition: 'transform 0.5s cubic-bezier(0.25, 1, 0.5, 1)'
    }
  }

  // คำนวณมุมหมุน 3D อิงตามตำแหน่งเมาส์และจุดศูนย์กลางของการ์ด
  const rotateX = -(elementY.value - elementHeight.value / 2) / (elementHeight.value / 12)
  const rotateY = (elementX.value - elementWidth.value / 2) / (elementWidth.value / 12)

  return {
    transform: `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) scale(1.02)`,
    transition: 'transform 0.1s cubic-bezier(0.25, 1, 0.5, 1)'
  }
})

const glowStyle = computed(() => {
  if (isOutside.value) {
    return { opacity: 0 }
  }
  return {
    opacity: 1,
    left: `${elementX.value}px`,
    top: `${elementY.value}px`,
  }
})
</script>

<template>
  <div
    ref="target"
    :style="cardStyle"
    class="relative w-full max-w-sm rounded-2xl border border-white/10 bg-slate-900/60 p-8 shadow-2xl backdrop-blur-xl transition-shadow duration-300 group overflow-hidden select-none hover:shadow-purple-500/10 hover:border-white/20"
  >
    <!-- เอฟเฟกต์แสงไฟแบบเรเดียลวิ่งตามเมาส์ (Radial Glow Effect) -->
    <div
      :style="glowStyle"
      class="pointer-events-none absolute -translate-x-1/2 -translate-y-1/2 w-64 h-64 bg-radial from-purple-500/15 via-indigo-500/5 to-transparent blur-2xl transition-opacity duration-500"
    ></div>

    <!-- ลายกริดแบ็คกราวด์สไตล์เทคล้ำ (Grid Backdrop) -->
    <div class="absolute inset-0 bg-[linear-gradient(to_right,#ffffff03_1px,transparent_1px),linear-gradient(to_bottom,#ffffff03_1px,transparent_1px)] bg-[size:24px_24px] pointer-events-none rounded-2xl"></div>

    <div class="relative z-10 flex flex-col h-full space-y-6">
      <div class="flex items-center justify-between">
        <div class="w-12 h-12 rounded-xl bg-purple-500/10 border border-purple-500/20 flex items-center justify-center text-purple-400 group-hover:scale-110 group-hover:bg-purple-500/20 group-hover:text-purple-300 transition-all duration-300">
          <Zap class="w-6 h-6 animate-pulse" />
        </div>
        <span class="text-xs font-mono text-purple-400 bg-purple-500/10 border border-purple-500/20 px-2.5 py-1 rounded-full flex items-center gap-1.5 shadow-sm shadow-purple-500/5">
          <Sparkles class="w-3.5 h-3.5 animate-spin-slow" /> Premium UI
        </span>
      </div>

      <div class="space-y-2">
        <h3 class="text-2xl font-bold text-white tracking-tight group-hover:text-purple-300 transition-colors duration-300">
          Interactive Motion
        </h3>
        <p class="text-slate-400 text-sm leading-relaxed">
          สัมผัสประสบการณ์โต้ตอบระดับพรีเมียมด้วยเอฟเฟกต์ 3D Tilt และแสง Glow ตามตำแหน่งเมาส์ ผสานเข้ากับระบบ Vue 3 ลื่นไหลไม่มีสะดุด
        </p>
      </div>

      <!-- ลิสต์ฟีเจอร์เด่น -->
      <div class="space-y-3 pt-2">
        <div class="flex items-center gap-3 text-xs text-slate-300">
          <Shield class="w-4.5 h-4.5 text-emerald-400" />
          <span>โครงสร้างรองรับ Web Accessibility (Radix)</span>
        </div>
        <div class="flex items-center gap-3 text-xs text-slate-300">
          <Sparkles class="w-4.5 h-4.5 text-purple-400" />
          <span>แอนิเมชันลื่นไหล 60 FPS บนเครื่องพกพา</span>
        </div>
      </div>

      <div class="flex items-center gap-3 pt-4">
        <Button class="w-full bg-gradient-to-r from-purple-600 to-indigo-600 hover:from-purple-500 hover:to-indigo-500 text-white font-medium shadow-lg shadow-purple-500/10 group/btn border border-purple-500/30 transition-all duration-300 cursor-pointer">
          เริ่มต้นใช้งาน
          <ArrowRight class="w-4 h-4 ml-2 group-hover/btn:translate-x-1.5 transition-transform duration-300" />
        </Button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.animate-spin-slow {
  animation: spin 8s linear infinite;
}
@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>
