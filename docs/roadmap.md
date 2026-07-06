# 🚀 Project Roadmap: Interactive Storytelling Landing Page (Vue 3 + Bun + NPM)

## 💻 Phase 1: Docker Multi-Environment Setup (Bun & Volume)

- [ ] สตาร์ทโปรเจกต์ Vue 3 + TypeScript + Tailwind CSS บนเครื่อง Local โดยใช้ **Bun** (`bun create vite`)
- [ ] สร้างไฟล์ Docker แยก 2 สภาพแวดล้อม:
  - `docker-compose.dev.yml` (สำหรับเล่นในเครื่อง โหลดเร็ว มี Volume ผูกพอร์ต `3000:3000` ทำ Hot Reload)
  - `docker-compose.prod.yml` (สำหรับขึ้น VM ปิดพอร์ตมิดชิด รอเชื่อมเข้าวง `npm_network`)
- [ ] สร้างไฟล์ Dockerfile แยก:
  - `Dockerfile.dev` (ใช้ Base Image `oven/bun:alpine` เพื่อความเบาและจูนโค้ดในเครื่อง)
  - `Dockerfile.prod` (สำหรับ Build ไฟล์สแตติกไปรันบน Production)
- [ ] เพิ่มสคริปต์ใน `package.json` เพื่อความสะดวกในการสตาร์ทเครื่อง:
  - `"bun:docker:dev": "docker compose -f docker-compose.dev.yml up --build"`

## 🎨 Phase 2: Premium Tech-Stack UI & Interactive Storytelling

- [ ] **Core Components Layer:** ติดตั้งและเซ็ตอัป **shadcn-vue** เพื่อเป็นโครงสร้าง UI พื้นฐานที่รองรับ Accessibility (Radix Vue)
- [ ] **Visual Impact Layer:** ติดตั้ง **Inspira UI** (พอร์ตมาจาก Aceternity/Magic UI) สำหรับเล่นเอฟเฟกต์พื้นหลังหรูๆ เช่น Aurora Background, Bento Grid หรือ Text Effects
- [ ] **Micro-Interactions Layer:** ใช้ **@vueuse/motion** ในการทำพวก Spring Animation และจับสเตตการเคลื่อนไหวตามเมาส์
- [ ] **Custom Details Layer:** แอบจิ๊กสไตล์ปุ่มเก๋ๆ การ์ดล้ำๆ หรือเอฟเฟกต์โฮเวอร์จาก **Uiverse.io** มาแปลงเป็น Tailwind เพื่อเพิ่มความวิบวับในจุดดึงสายตา
- [ ] **Storytelling Flow:** ออกแบบแอนิเมชันให้ผูกกับ Scroll Position (ไถจอแล้วเนื้อเรื่องค่อยๆ เลื่อน ปรากฏตัว หรือเปลี่ยนสี)
- [ ] ตรวจสอบความลื่นไหลของเฟรมเรตแอนิเมชัน และทำ Responsive (Mobile ต้องไม่พัง ไม่กระตุก)

## 🔄 Phase 3: Git Workflow & CI/CD Pipeline

- [ ] ตั้งค่า Git Repository และแยก Git Branch สำหรับทำงาน (`main`, `develop`)
- [ ] เขียนไฟล์คอนฟิกสำหรับ CI/CD (GitHub Actions หรือ GitLab CI) ผูกกับ Trigger **Push to `develop`**
- [ ] **CI Step:** สั่งล้างสนิม ตรวจเช็กความถูกต้องโค้ด และสั่ง Build เพื่อเช็กว่าไม่มี Typescript Error
- [ ] **CD Step:** ใช้ **SSH Action** ยิงรีโมทข้ามมิติเข้าไปที่เครื่อง VM หลังบ้าน สั่งลากโค้ดใหม่ลงมา แล้วรันคำสั่งแบบไร้รอยต่อ:
  - `docker compose -f docker-compose.prod.yml up -d --build`

## 🏢 Phase 4: Production Setup on VM & Routing with NPM

- [ ] ใช้ SSH มุดเข้าไปเช็กความพร้อมของ Docker Engine บนเครื่อง VM (หน้าจอดำ)
- [ ] รันตู้ **Nginx Proxy Manager (NPM)** ให้เป็นพระเอกเฝ้าประตูหน้าสุดในเครื่อง VM
- [ ] เปิด Google Chrome บนโน้ตบุ๊ก Zorin ตัวเอง จิ้มไปที่ `http://<IP_VM>:81` เพื่อดึงหน้าจอ GUI ของ NPM ออกมาใช้งาน
- [ ] นำตู้คอนเทนเนอร์แอป Vue ที่ได้จากไฟล์ `docker-compose.prod.yml` ไปผูกเข้ากับเครือข่ายของ NPM
- [ ] กดปุ่มสร้าง Proxy Host ในหน้าจอ NPM ผูกชื่อโดเมน และกดคลิกทำ SSL (HTTPS) ฟรีภายใน 1 คลิก
- [ ] เปิดทดสอบหน้าเว็บผ่านโดเมนจริง เช็กแอนิเมชันบน Production เป็นอันปิดโปรเจกต์อย่างสมบูรณ์!
