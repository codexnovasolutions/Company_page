<script setup lang="ts">
import { Head } from '@inertiajs/vue3';
import PrincipalLayout from '@/layouts/PrincipalLayout.vue';
import { onMounted } from 'vue';

onMounted(() => {
    const script = document.createElement('script');
    script.type = 'module';
    script.src = 'https://unpkg.com/@splinetool/viewer@1.10.38/build/spline-viewer.js';
    document.head.appendChild(script);
    script.onload = () => {
        setTimeout(() => {
            const viewer = document.querySelector('spline-viewer') as any;
            const shadowRoot = viewer.shadowRoot;
            if (shadowRoot) {
                const logo = shadowRoot.querySelector('#logo');
                if (logo) {
                    logo.style.display = 'none';
                }
            }
            const canvas = shadowRoot.querySelector('canvas');
            if (canvas) {
                canvas.addEventListener('wheel', (e: WheelEvent) => {
                    e.preventDefault();
                    window.scrollBy(0, e.deltaY); // Fuerza el scroll del body
                }, { passive: false });
            }
        }, 1000);

    }
});

</script>

<template>

    <Head title="Home" />

    <PrincipalLayout>
        <!-- Hero 3D con Spline -->
        <section id="inicio" class="relative h-[600px] w-full overflow-hidden">
            <spline-viewer url="https://prod.spline.design/jeZSFimUFxN4C9zM/scene.splinecode" />
        </section>

        <!-- Mensaje Principal -->
        <section class="container mx-auto px-6 py-16 text-center ">
            <h1 class="text-4xl font-bold text-[#0F4C81] mb-4">Innovación que impulsa tu crecimiento digital</h1>
            <p class="text-lg text-[#6C757D] mb-6">
                En CodexNova Solutions brindamos software a medida, soluciones empresariales y herramientas inteligentes
                que transforman tu negocio.
            </p>
            <a href="#servicios" class="px-6 py-2 bg-[#0F4C81] text-white rounded-lg hover:bg-[#0A3D62] transition">
                Conoce nuestros servicios
            </a>
        </section>

        <!-- Nuestros Servicios -->
        <section id="servicios" class="bg-gray-100 py-16">
            <div class="container mx-auto px-6 text-center">
                <h2 class="text-3xl font-bold text-[#0F4C81] mb-8">Nuestros Servicios</h2>
                <div class="grid md:grid-cols-2 gap-10 text-left text-gray-700">
                    <div>
                        <h3 class="text-xl font-semibold mb-2">Desarrollo a Medida</h3>
                        <p>Creamos soluciones únicas y personalizadas adaptadas a tus necesidades.</p>
                    </div>
                    <div>
                        <h3 class="text-xl font-semibold mb-2">Diseño UX/UI</h3>
                        <p>Interfaces intuitivas y atractivas que garantizan una experiencia excepcional.</p>
                    </div>
                    <div>
                        <h3 class="text-xl font-semibold mb-2">Consultoría Tecnológica</h3>
                        <p>Asesoramiento experto para optimizar procesos y escalar tu negocio.</p>
                    </div>
                    <div>
                        <h3 class="text-xl font-semibold mb-2">Optimización y Mantenimiento</h3>
                        <p>Rendimiento óptimo con soporte continuo y mejoras constantes.</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Sobre Nosotros -->
        <section id="nosotros" class="py-16">
            <div class="container mx-auto px-6 text-center text-gray-700">
                <h2 class="text-3xl font-bold text-[#0F4C81] mb-8">Sobre Nosotros</h2>
                <div class="grid md:grid-cols-2 gap-10 text-left">
                    <div>
                        <h3 class="font-bold text-xl mb-2">Misión</h3>
                        <p>
                            Ofrecer soluciones tecnológicas innovadoras y de alta calidad que impulsen la transformación
                            digital, con un servicio cercano y adaptado a cada cliente.
                        </p>
                    </div>
                    <div>
                        <h3 class="font-bold text-xl mb-2">Visión</h3>
                        <p>
                            Ser líderes en desarrollo de software en Perú y LATAM, impulsando herramientas digitales
                            eficientes para un crecimiento sostenible.
                        </p>
                    </div>
                    <div>
                        <h3 class="font-bold text-xl mb-2">Innovación Constante</h3>
                        <p>Siempre a la vanguardia de las últimas tecnologías.</p>
                    </div>
                    <div>
                        <h3 class="font-bold text-xl mb-2">Colaboración Transparente</h3>
                        <p>Trabajamos contigo en cada paso del camino.</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Portafolio -->
        <section id="productos" class="bg-gray-100 py-16">
            <div class="container mx-auto px-6 text-center">
                <h2 class="text-3xl font-bold text-[#0F4C81] mb-8">Nuestro Portafolio</h2>
                <div class="grid md:grid-cols-2 gap-8">
                    <!-- Proyecto 1 (copia este bloque para más) -->
                    <div class="bg-white rounded-lg shadow-md p-6">
                        <img src="" alt="Proyecto 1" class="mb-4 w-full h-48 object-cover rounded-md" />
                        <h3 class="text-xl font-semibold mb-2">Sistema de Gestión ERP</h3>
                        <p class="text-gray-600 mb-2">Una solución integral para controlar inventarios, ventas y
                            reportes financieros.</p>
                        <div class="flex gap-2 justify-center mt-2">
                            <img src="" alt="Vue" class="h-6" />
                            <img src="" alt="Laravel" class="h-6" />
                            <img src="" alt="MySQL" class="h-6" />
                        </div>
                        <a href="" target="_blank" class="mt-4 inline-block text-sm text-[#0F4C81] hover:underline">
                            Ver Demo →
                        </a>
                    </div>
                </div>
            </div>
        </section>

        <!-- Contacto -->
        <section id="contacto" class="bg-[#0F4C81] text-white py-16 text-center">
            <h2 class="text-3xl font-bold mb-4">Contáctanos Hoy</h2>
            <p class="text-sm">Desarrollo de soluciones tecnológicas a tu alcance.</p>
        </section>
    </PrincipalLayout>
</template>
