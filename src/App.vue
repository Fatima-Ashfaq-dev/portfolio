<script setup>
import { Swiper, SwiperSlide } from "swiper/vue";
import { Navigation, Pagination, Autoplay, FreeMode } from "swiper/modules";
import "swiper/css";
import "swiper/css/navigation";
import "swiper/css/pagination";
import "swiper/css/autoplay";
import "swiper/css/free-mode";

import { ref, onMounted } from "vue";
import { Application } from "https://unpkg.com/@splinetool/runtime@1.0.95/build/runtime.js";
import AOS from "aos";
import "aos/dist/aos.css";

// ======================
// COUNTER SECTION
// ======================
const projects = ref(0);
const industries = ref(0);
const experience = ref(0);

const animateValue = (refVar, start, end, duration) => {
  let startTime = null;
  const step = (timestamp) => {
    if (!startTime) startTime = timestamp;
    const progress = Math.min((timestamp - startTime) / duration, 1);
    refVar.value = Math.floor(progress * (end - start) + start);
    if (progress < 1) {
      requestAnimationFrame(step);
    }
  };
  requestAnimationFrame(step);
};

// onMounted(() => {
//   // Animate only when stats section is visible
//   const statsSection = document.querySelector(".stats");
//   let triggered = false;

//   const observer = new IntersectionObserver((entries) => {
//     if (entries[0].isIntersecting && !triggered) {
//       triggered = true;
//       animateValue(projects, 0, 200, 2000);
//       animateValue(industries, 0, 10, 2000);
//       animateValue(experience, 0, 7, 2000);
//     }
//   }, { threshold: 0.5 });

//   if (statsSection) observer.observe(statsSection);
// });

// ======================
// AOS INIT
// ======================
// onMounted(() => {
//   AOS.init({
//     duration: 1000,
//     once: true,
//     easing: "ease-in-out",
//   });
// });

  // store swiper instance
  const projectSwiper = ref(null);

  // onMounted(() => {
  //   if (projectSwiper.value) {
  //     const swiper = projectSwiper.value.swiper;

  //     document.querySelectorAll(".project-card").forEach(card => {
  //       card.addEventListener("mouseenter", () => {
  //         swiper.autoplay.stop();
  //       });
  //       card.addEventListener("mouseleave", () => {
  //         swiper.autoplay.start();
  //       });
  //     });
  //   }
  // });


  // onMounted(() => {
  //   const canvases = document.querySelectorAll(".canvas3d");

  //   canvases.forEach((canvas) => {
  //     const app = new Application(canvas);
  //     app.load("https://prod.spline.design/wMUjxT0aovzV5Dra/scene.splinecode").then(() => {
  //       // Disable zoom/scroll wheel
  //       if (app.controls) {
  //         app.controls.enableZoom = false; // turn off zoom
  //         app.controls.enablePan = true;   // keep panning if you want
  //         app.controls.enableRotate = true; // keep rotation
  //       }
  //     });

  //     // Extra safety: prevent wheel event on canvas
  //     canvas.addEventListener("wheel", (e) => e.preventDefault(), { passive: false });
  //   });
  // });
  // Row 1 Tools
  onMounted(() => {
  // Animate counters
  const statsSection = document.querySelector(".stats");
  let triggered = false;
  const observer = new IntersectionObserver((entries) => {
    if (entries[0].isIntersecting && !triggered) {
      triggered = true;
      animateValue(projects, 0, 200, 2000);
      animateValue(industries, 0, 10, 2000);
      animateValue(experience, 0, 7, 2000);
    }
  }, { threshold: 0.5 });
  if (statsSection) observer.observe(statsSection);

  // AOS init
  AOS.init({
    duration: 1000,
    once: true,
    easing: "ease-in-out",
  });

  // Swiper autoplay pause on hover
  if (projectSwiper.value) {
    const swiper = projectSwiper.value.swiper;
    document.querySelectorAll(".project-card").forEach(card => {
      card.addEventListener("mouseenter", () => swiper.autoplay.stop());
      card.addEventListener("mouseleave", () => swiper.autoplay.start());
    });
  }

  // Spline setup
  const canvases = document.querySelectorAll(".canvas3d");
  canvases.forEach((canvas) => {
    const app = new Application(canvas);
    app.load("https://prod.spline.design/wMUjxT0aovzV5Dra/scene.splinecode").then(() => {
      if (app.controls) {
        app.controls.enableZoom = false;
        // app.controls.enablePan = true;
        // app.controls.enableRotate = true;
      }
    });
    // canvas.addEventListener("wheel", (e) => e.preventDefault(), { passive: false });
  });
});

  
  const toolsRow1 = [
   { name: "WordPress", icon: "/src/assets/wordpress.png" },
    { name: "WooCommerence", icon: "/src/assets/woo.png" },
    { name: "Elementor", icon: "/src/assets/element.png" },
    { name: "Laravel", icon: "/src/assets/laravel.png" },
    { name: "PHP", icon: "/src/assets/php.png" },
    { name: "HTML5", icon: "/src/assets/html.png" },
    { name: "CSS3", icon: "/src/assets/css.png" },
    { name: "Bootstrap 5", icon: "/src/assets/bootstrap.png" },
 


  ];

  // Row 2 Tools
  const toolsRow2 = [   
    { name: "Shopify", icon: "/src/assets/shopify.png" },
       { name: "JavaScript", icon: "/src/assets/js.png" },
    { name: "React.js", icon: "/src/assets/react.png" },
    { name: "Next.js", icon: "/src/assets/next.png" },    
    { name: "Vue.js", icon: "/src/assets/vue.png" },
    { name: "MySQL", icon: "/src/assets/mysql.png" },
     { name: "SQL Server", icon: "/src/assets/mssql.png" },
    { name: "GitHub", icon: "/src/assets/github.png" },
  { name: "PayPal", icon: "/src/assets/paypal.png" },
  ];
</script>

<template>
  <header class="custom-navbar py-2" >
    <div data-aos="fade-down" class="container sticky-section  d-flex align-items-center justify-content-between rounded-pill px-4 py-2 navbar-box">

      <!-- Brand -->
      <a class="navbar-brand text-white fw-semibold" href="#">
        Fatima Ashfaq
      </a>

      <!-- Desktop menu -->
      <div class="d-none d-lg-flex gap-4">
        <a class="nav-link text-white" href="#home">Home</a>
        <a class="nav-link text-white" href="#services">Services</a>
        <a class="nav-link text-white" href="#about">About</a>
        <a class="nav-link text-white" href="#tools">Tools</a>
        <a class="nav-link text-white" href="#projects">Projects</a>
        <!-- <a class="nav-link text-white" href="#testimonials">Testimonials</a> -->
      </div>

      <!-- Contact Button -->
      <a href="#contact" class=" btn-contact ms-3 d-none  rounded-pill fw-semibold d-lg-inline-block">
        Contact
      </a>

      <!-- Hamburger (only mobile) -->
        <button class="navbar-toggler border-0 d-lg-none" type="button"
        data-bs-toggle="collapse" data-bs-target="#navbarNav"
        aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
  <!-- Inline SVG -->
  <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" fill="white" viewBox="0 0 30 30">
    <path stroke="white" stroke-width="2" stroke-linecap="round" d="M4 7h22M4 15h22M4 23h22"/>
  </svg>
</button>
      <!-- <button class="navbar-toggler border-0 text-white d-lg-none" type="button" data-bs-toggle="collapse"
        data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon text-white"></span>
      </button> -->
    </div>

    <!-- Mobile Menu -->
    <div class="collapse navbar-collapse d-lg-none text-center mt-3" id="navbarNav">
      <ul class="navbar-nav gap-3">
        <li class="nav-item"><a class="nav-link text-white" href="#home">Home</a></li>
        <li class="nav-item"><a class="nav-link text-white" href="#services">Services</a></li>
        <li class="nav-item"><a class="nav-link text-white" href="#about">About</a></li>
        <li class="nav-item"><a class="nav-link text-white" href="#tools">Tools</a></li>
        <li class="nav-item"><a class="nav-link text-white" href="#projects">Projects</a></li>
        <!-- <li class="nav-item"><a class="nav-link text-white" href="#testimonials">Testimonials</a></li> -->
      </ul>
    </div>
  </header>

<div class="social-icons">
  <a href="https://www.linkedin.com/in/fatima-as/" target="_blank"><i class="fab fa-linkedin"></i></a>
  <a href="https://www.upwork.com/freelancers/~010daa211030285506" target="_blank"><img src="/src/assets/upwork.svg" alt=""></a>
  <a href="https://github.com/Fatima-Ashfaq-dev" target="_blank"><i class="fab fa-github"></i></a>
</div>
  <!-- Hero Section -->

  <section id="home" class="section d-flex" >
    <div class="container">
      <div class="row ">

        <!-- Left Content -->
        <div class="col-lg-6 text-white  text-lg-start" data-aos="fade-down">
          <h5 class="text-orange mt-5 mb-3">Hello! I’m</h5>
          <h1 class="title">
            FATIMA <br />
            ASHFAQ
          </h1>
          <p class="text mt-4 mb-5">
            Every project I build starts with a simple goal — turning complex ideas into digital solutions that feel
            effortless to use. I combine clean code with thoughtful design to create websites, APIs, dashboards, and
            payment systems that are secure, scalable, and future-ready.
          </p>
          <a href="#contact" class=" btn-hire mt-5 mb-5 rounded-pill fw-semibold">
            Hire Me
          </a>
        </div>

        <!-- Right Spline (responsive) -->
        <div class="col-lg-6 " data-aos="fade-up">
          <div class="spline-wrapper">
            <!-- <img src="/src/assets/cube.png" alt=""> -->
            <canvas class="canvas3d"></canvas>
          </div>
        </div>
      </div>
    </div>
  </section>
  <!-- Services Section -->
  <section id="services" class="services-section py-5 ">
    <div class="container">
      <h5 class="text-orange mb-2" data-aos="fade-down">Services</h5>
      <h2 class="title mb-5" data-aos="fade-up">I Offer</h2>
      <div class="container-height">
        <!-- Swiper -->
        <Swiper :modules="[Navigation, Pagination, Autoplay]" :autoplay="{ delay: 3000, disableOnInteraction: false }"
          :slides-per-view="'auto'" :space-between="20" :breakpoints="{
    768: { slidesPerView: 2 },
    1024: { slidesPerView: 3 }
  }" :navigation="{ nextEl: '.custom-next', prevEl: '.custom-prev' }" loop class="mySwiper">
          <!-- Card 1 -->
          <div class="custom-prev">
            <img src="/src/assets/rarrow.svg" alt="">
          </div>

          <div class="custom-next">
            <img src="/src/assets/rarrow.svg" alt="">

          </div>
  <SwiperSlide >
            <div class="service-card">
              <div class="icon"><img src="/src/assets/lar.png" alt=""></div>
              <h5>Laravel </h5>
             <p>I create dynamic, high-performance applications using Laravel for robust backends and Vue.js for fast, interactive frontends.</p>
            </div>
          </SwiperSlide>
   <SwiperSlide >
            <div class="service-card">
              <div class="icon"><img  src="/src/assets/ph.png" alt=""></div>
              <h5>PHP Development</h5>
              <p>I build robust, server-side applications using PHP for custom functionality. My solutions are secure, scalable, and designed to handle complex requirements.</p>
            </div>
          </SwiperSlide>
            <SwiperSlide >
            <div class="service-card">
              <div class="icon"><img height="50" width="50" src="/src/assets/word.png" alt=""></div>
              <h5>WordPress Website Development</h5>
              <p>I build professional WordPress websites that are easy to manage, SEO-optimized, and tailored to your business needs.</p>
            </div>
          </SwiperSlide>
            <SwiperSlide >
            <div class="service-card">
              <div class="icon"><img height="50" width="50" src="/src/assets/wooo.png" alt=""></div>
              <h5>WooCommerce Development</h5>
              <p>I develop online stores with WooCommerce that are user-friendly and optimized for sales. From product pages to checkout, everything is built for performance.</p>
            </div>
          </SwiperSlide>
            <SwiperSlide >
            <div class="service-card">
              <div class="icon"><img src="/src/assets/shop.png" alt=""></div>
              <h5>Shopify Theme & App Development</h5>
              <p>I design and customize Shopify themes and apps, creating seamless online shopping experiences for your customers.</p>
            </div>
          </SwiperSlide>
          <SwiperSlide >
            <div class="service-card">
              <div class="icon"><img src="/src/assets/world.png" alt=""></div>
              <h5>Custom Web Development</h5>
              <p>I develop tailored web solutions to meet your unique requirements, ensuring scalability, performance, and long-term growth.</p>
            </div>
          </SwiperSlide>
    <!-- Card 3 -->
          <SwiperSlide >
            <div class="service-card">
              <div class="icon"><img src="/src/assets/ele.png" alt=""></div>
              <h5>Elementor Website Design</h5>
              <p>I build modern, responsive websites using Elementor’s powerful design tools. This makes your site flexible, customizable, and easy to update.</p>
            </div>
          </SwiperSlide>
          <!-- Card 2 -->
          <SwiperSlide >
            <div class="service-card">
              <div class="icon"><img src="/src/assets/link.png" alt=""></div>
              <h5>API Development & Integration</h5>
             <p>I design and integrate APIs that connect your applications, automate workflows, and improve system efficiency.</p>
            </div>
          </SwiperSlide>

          <!-- Card 3 -->
          <SwiperSlide >
            <div class="service-card">
              <div class="icon"><img src="/src/assets/db.png" alt=""></div>
              <h5>Database Design & Optimization</h5>
              <p>I design, structure, and optimize databases to handle complex queries, improve speed, and support business growth.</p>
            </div>
          </SwiperSlide>
          <!-- Card 4 -->
          <SwiperSlide >
            <div class="service-card">
              <div class="icon"><img src="/src/assets/store.png" alt=""></div>
              <h5>Ecommerce Website
                Development</h5>
              <p>I create secure, user-friendly eCommerce platforms with smooth checkout experiences to boost sales and customer trust.</p>
            </div>
          </SwiperSlide>
          <!-- Card 5 -->
          <SwiperSlide >
            <div class="service-card">
              <div class="icon"><img src="/src/assets/bar.png" alt=""></div>
              <h5>Admin Dashboards &
                Reporting Systems</h5>
              <p>I build intuitive dashboards with real-time analytics and reporting, helping you track performance and make data-driven decisions.</p>
            </div>
          </SwiperSlide>
          <!-- Card 6 -->
          <SwiperSlide >
            <div class="service-card">
              <div class="icon"><img src="/src/assets/smobile.png" alt=""></div>
              <h5>Responsive & Mobile
                Friendly UI</h5>
             <p>I design responsive, mobile-friendly interfaces that provide a consistent and engaging experience across all devices.</p>
            </div>
          </SwiperSlide>

        </Swiper>
      </div>


    </div>
  </section>
  <!-- About Section -->
  <section id="about" class="section d-flex align-items-center" >
    <div class="container  text-center">
      <div class="row align-items-center">

        <!-- Left Content -->
        <div class="col-lg-6 text-center " data-aos="fade-down">
          <div class="spline-wrapper">
            <!-- <img src="/src/assets/cube.png" alt=""> -->
            <canvas class="canvas3d"></canvas>
          </div>
        </div>


        <!-- Right (responsive) -->
        <div class="col-lg-6 text-white text-center text-lg-start" data-aos="fade-up">
          <h2 class=" font-bold mb-6">About Me</h2>
          <h5 class="text-orange title mb-2 uppercase ">WHO IS FATIMA?</h5>

          <p class="text mt-4">
            I’m a web developer who loves turning ideas into digital solutions that are both functional and
            user-friendly. With experience in building websites, APIs, databases, dashboards, and payment systems, I
            focus on creating secure, scalable, and responsive projects that help businesses grow. My goal is to make
            technology simple, reliable, and human-centered.
          </p>
          <div class="stats">
    <div class="stat">
      <h2>{{ projects }}+</h2>
      <p>Project Completed</p>
    </div>
    <div class="stat">
      <h2>{{ industries }}+</h2>
      <p>Industry Covered</p>
    </div>
    <div class="stat">
      <h2>{{ experience }}+</h2>
      <p>Years of Experience</p>
    </div>

   
  </div>
   <div class="col-12 d-flex align-items-center ">
      
    <a href="/src/assets/fatima.pdf" download class="submit-btn d-flex align-items-center">
  Download CV
 
</a> <span class="submit-icon">
    <img src="/src/assets/oarrow.svg" alt="arrow" />
  </span>

       
      </div>

    
        </div>


      </div>

    </div>
  </section>

  <!-- Tools Section -->
  <section id="tools" class="tools-section py-10 mt-5 mb-5">
    <div class="container mx-auto mt-5 pt-5">
      <h5 class="text-orange mb-2 uppercase tracking-wide" data-aos="fade-down">What I Use</h5>
      <h2 class="title font-bold mb-10" data-aos="fade-up">Tools Behind <br> My Work</h2>
      <div class="container-height mb-10" data-aos="slide-up">
        <!-- Row 1: Left to Right -->
        <Swiper 
         :slides-per-view="'auto'" :space-between="10" :breakpoints="{

          425: { slidesPerView: 2 },
    768: { slidesPerView: 3 },
    1024: { slidesPerView: 5 }
  }" :loop="true" :free-mode="true" :speed="4000"
          :autoplay="{ delay: 0, disableOnInteraction: false }" :modules="[Autoplay, FreeMode]" class="mySwiper  mb-6">
          <SwiperSlide v-for="tool in toolsRow1" :key="tool.name" >
            <div class="tool-card " >
              <div class="icon-circle">
    <img :src="tool.icon" :alt="tool.name" />
  </div>
              
              <p>{{ tool.name }}</p>
            </div>
          </SwiperSlide>
        </Swiper>
        <br>
        <!-- Row 2: Right to Left -->
        <Swiper 
        :slides-per-view="'auto'" :space-between="20" :breakpoints="{
          
          425: { slidesPerView: 2 },
    768: { slidesPerView: 3 },
    1024: { slidesPerView: 5 }
  }" 
         :loop="true" :free-mode="true" :speed="4000"
          :autoplay="{ delay: 0, reverseDirection: true, disableOnInteraction: false }" :modules="[Autoplay, FreeMode]"
          class="mySwiper">
          <SwiperSlide v-for="tool in toolsRow2" :key="tool.name" >
            <div class="tool-card">
                <div class="icon-circle">
    <img :src="tool.icon" :alt="tool.name" />
  </div>
              
              <p>{{ tool.name }}</p>
            </div>
          </SwiperSlide>
        </Swiper>

      </div>


    </div>
  </section>
  <!-- Projects Section -->
  <section id="projects" class="projects-section py-5">
    <div class="container">
      <h5 class="text-orange mb-2" data-aos="fade-down">My Portfolio</h5>
      <h2 class="title mb-5" data-aos="fade-up">My Latest <br> Projects</h2>
      <div class="container-project">
        <!-- Swiper Projects -->
        <Swiper ref="projectSwiper" :modules="[Navigation, Pagination, Autoplay]" :autoplay="{ delay: 3000, disableOnInteraction: false, pauseOnMouseEnter: true
           }" :slides-per-view="'auto'" :space-between="40"
          :breakpoints="{ 768: { slidesPerView: 2 }, 1024: { slidesPerView: 3 } }"
          :navigation="{ nextEl: '.custom-next', prevEl: '.custom-prev' }" loop class="mySwiper">
          <div class="custom-prev">
            <img src="/src/assets/rarrow.svg" alt="">
          </div>

          <div class="custom-next">
            <img src="/src/assets/rarrow.svg" alt="">

          </div>



          <!-- Card 1 -->
          <SwiperSlide>
            <div class="project-card">
              <div class="project-image-wrapper">
                <img src="/src/assets/xchange.png" alt="Project 1" class="project-image" />
                 <!-- Overlay with Eye Icon -->
                <div class="project-overlay">
                  <a href="https://xchangeofamerica.com/" target="_blank">
                    <i class="fas fa-eye eye-icon"></i>
                  </a>
                </div>
              </div>
              <div class="tags mt-3">
                <span class="tag">Laravel</span>
                <span class="tag">PHP</span>
                <span class="tag">JQuery</span>
                <span class="tag">MySQL</span>
                 <span class="tag">API Integration</span>

              </div>
              <h5 class="mt-3 project-title">
                Xchange Of America
              </h5>
            </div>
          </SwiperSlide>

          <!-- Card 2 -->
          <SwiperSlide>
            <div class="project-card">
              <div class="project-image-wrapper">
                <img src="/src/assets/health.png" alt="Project 1" class="project-image" />
                 <!-- Overlay with Eye Icon -->
                <div class="project-overlay">
                  <a href="https://www.healthmug.com/" target="_blank">
                    <i class="fas fa-eye eye-icon"></i>
                  </a>
                </div>
              </div>
              <div class="tags mt-3">
                <span class="tag">Laravel</span>
                <span class="tag">PHP</span>
                <span class="tag">MySQL</span>
                 <span class="tag">API Integration</span>
                 <span class="tag">Ecommerce</span>
                 <span class="tag">Payment Gateway</span>
              </div>
              <h5 class="mt-3 project-title">
                Healthcare Website - Online Pharmacy
              </h5>
            </div>

          </SwiperSlide>
          <!-- Card 3 -->
          <SwiperSlide>
            <div class="project-card">
              <div class="project-image-wrapper">
                <img src="/src/assets/bigdream.png" alt="Project 1" class="project-image" />
                 <!-- Overlay with Eye Icon -->
                <div class="project-overlay">
                  <a href="https://dream-big-digital.co.uk/" target="_blank">
                    <i class="fas fa-eye eye-icon"></i>
                  </a>
                </div>
              </div>
              <div class="tags mt-3">
                 <span class="tag">React</span>
                <span class="tag">Next.js</span>
                <span class="tag">JQuery</span>
                 <span class="tag">API Integration</span>
              </div>
              <h5 class="mt-3 project-title">
                Dream Big Digital
              </h5>
            </div>
          </SwiperSlide>

          <!-- Card 4 -->
          <SwiperSlide>
            <div class="project-card">
              <div class="project-image-wrapper">
                <img src="/src/assets/love.png" alt="Project 1" class="project-image" />
                 <!-- Overlay with Eye Icon -->
                <div class="project-overlay">
                  <a href="https://loveused.co.uk/" target="_blank">
                    <i class="fas fa-eye eye-icon"></i>
                  </a>
                </div>
              </div>
              <div class="tags mt-3">
                <span class="tag">React</span>
                <span class="tag">React Router</span>
                <span class="tag">Tailwind CSS</span>
                 <span class="tag">API Integration</span>
                 <span class="tag">Payment Gateway</span>
              </div>
              <h5 class="mt-3 project-title">
                Love Used - Ecommerce Website
              </h5>
            </div>

          </SwiperSlide>

            <!-- Card 5 -->
          <SwiperSlide>
            <div class="project-card">
              <div class="project-image-wrapper">
                <img src="/src/assets/africanclimate.png" alt="Project 1" class="project-image" />
                 <!-- Overlay with Eye Icon -->
                <div class="project-overlay">
                  <a href="https://africanclimateactionpartnership.org/" target="_blank">
                    <i class="fas fa-eye eye-icon"></i>
                  </a>
                </div>
              </div>
              <div class="tags mt-3">
                 <span class="tag">WordPress</span>
                <span class="tag">WooCommerce</span>
                <span class="tag">wpBakery</span>
                 <span class="tag">Contact Form 7</span>
                 <span class="tag">PHP</span>
<span class="tag">MySQL</span>
              </div>
              <h5 class="mt-3 project-title">
                African Climate Action Partnership
              </h5>
            </div>
          </SwiperSlide>

             <!-- Card 6 -->
          <SwiperSlide>
            <div class="project-card">
              <div class="project-image-wrapper">
                <img src="/src/assets/cbgfood.png" alt="Project 1" class="project-image" />
                 <!-- Overlay with Eye Icon -->
                <div class="project-overlay">
                  <a href="https://cbgfood.com.au/" target="_blank">
                    <i class="fas fa-eye eye-icon"></i>
                  </a>
                </div>
              </div>
              <div class="tags mt-3">
                 <span class="tag">WordPress</span>
                <span class="tag">WooCommerce</span>
                <span class="tag">Elmentor</span>
                 <span class="tag">WPForms</span>
                 <span class="tag">PHP</span>
<span class="tag">MySQL</span>
              </div>
              <h5 class="mt-3 project-title">
               CBG Food Service
              </h5>
            </div>
          </SwiperSlide>

            <!-- Card 7 -->
          <SwiperSlide>
            <div class="project-card">
              <div class="project-image-wrapper">
                <img src="/src/assets/aaenterprises.png" alt="Project 1" class="project-image" />
                 <!-- Overlay with Eye Icon -->
                <div class="project-overlay">
                  <a href="https://aaenterprises.com.pk/" target="_blank">
                    <i class="fas fa-eye eye-icon"></i>
                  </a>
                </div>
              </div>
              <div class="tags mt-3">
                 <span class="tag">WordPress</span>
                <span class="tag">WooCommerce</span>
                <span class="tag">wpBakery</span>
                 <span class="tag">Contact Form 7</span>
                 <span class="tag">PHP</span>
<span class="tag">MySQL</span>
              </div>
              <h5 class="mt-3 project-title">
                AA Enterprises
              </h5>
            </div>
          </SwiperSlide>

            <!-- Card 8 -->
          <SwiperSlide>
            <div class="project-card">
              <div class="project-image-wrapper">
                <img src="/src/assets/akenterprises.png" alt="Project 1" class="project-image" />
                 <!-- Overlay with Eye Icon -->
                <div class="project-overlay">
                  <a href="https://akenterprisesgroup.com/" target="_blank">
                    <i class="fas fa-eye eye-icon"></i>
                  </a>
                </div>
              </div>
              <div class="tags mt-3">
                 <span class="tag">WordPress</span>
                <span class="tag">Yoast SEO</span>
                <span class="tag">WhatsApp Chat</span>
                 <span class="tag">Contact Form 7</span>
                 <span class="tag">PHP</span>
<span class="tag">MySQL</span>
              </div>
              <h5 class="mt-3 project-title">
                AK Enterprises
              </h5>
            </div>
          </SwiperSlide>
        </Swiper>
      </div>
    </div>

  </section>
  <!-- Contact Section -->
  <section id="contact" class="contact-section py-5" >
    <div class="container contact-container">
      <div class="row mb-5">
        <div class="col-lg-6 text-white text-center text-lg-start">
          <!-- Left Side -->
          <div class="contact-left" data-aos="fade-down">
            <h5 class="text-orange mb-2">Contact</h5>
            <h2 class="title mb-4">Let's Create <br> Together</h2>
            <!-- <p class="mb-4">
              Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et
              dolore magna aliqua.
              Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
              consequat.
            </p> -->

            <!-- Contact Info -->
            <div class="contact-info" data-aos="fade-up">
              <!-- <p><span class="circle"><img src="/src/assets/phone.svg" alt="phone" /></span> +92 123 4567890</p> -->
              <p><span class="circle"><img src="/src/assets/email.svg" alt="phone" /></span> fatima@softtech.ae</p>
              <!-- <p><span class="circle"><img src="/src/assets/location.svg" alt="phone" /></span> Office 1301, 13th Floor, Al Saqr Business Tower, Sheikh Zayed
                Road Dubai UAE</p> -->
            </div>
          </div>
        </div>
        <div class="col-lg-6">
          <!-- Right Side Form -->
         <div class="contact-right" data-aos="fade-down">
  <form class="contact-form" 
  name="contact" 
  method="POST" 
  data-netlify="true" 
  netlify-honeypot="bot-field">
    <div class="row g-3" data-aos="fade-up">
    
 

  <!-- Name -->
  <div class="col-md-6">
    <label for="name" class="form-label">Your Name*</label>
    <input type="text" class="form-control custom-input" id="name" name="name" placeholder="Ex. John Doe" required>
  </div>

  <!-- Email -->
  <div class="col-md-6">
    <label for="email" class="form-label">Email*</label>
    <input type="email" class="form-control custom-input" id="email" name="email" placeholder="example@gmail.com" required>
  </div>

  <!-- Phone -->
  <!-- <div class="col-md-6">
    <label for="phone" class="form-label">Phone*</label>
    <input type="text" class="form-control custom-input" id="phone" name="phone" placeholder="Enter Phone Number" required>
  </div>

  <div class="col-md-6">
    <label for="country" class="form-label">Country*</label>
    <select id="country" name="country" class="form-select custom-input" required>
      <option value="">Select Country</option>
      <option>UAE</option>
      <option>Pakistan</option>
      <option>India</option>
    </select>
  </div> -->

  <!-- Message -->
  <div class="col-12">
    <label for="message" class="form-label">Your Message*</label>
    <textarea class="form-control custom-input" id="message" name="message" placeholder="Enter here.." required></textarea>
  </div>

  <!-- Submit -->
  <div class="col-12 d-flex align-items-center">
    <button type="submit" class="submit-btn">Submit</button>
    <span class="submit-icon">
      <img src="/src/assets/oarrow.svg" alt="arrow" />
    </span>
  </div>

    </div>
  </form>
</div>


        </div>

      </div>



    </div>
  </section>


</template>
