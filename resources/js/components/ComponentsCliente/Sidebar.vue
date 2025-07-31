<script setup>
import { usePage } from '@inertiajs/vue3';
import { ref, watch, computed } from 'vue';

const page = usePage();
const permisos = page.props.auth.permisos;

const open = ref({
    gestion: false,
    pendientes: false,
    tramitados: false,
    admin: false
});

const toggle = (key) => {
    open.value[key] = !open.value[key]
}

// Abrir automáticamente si estamos en esa sección
watch(() => page.url, (newUrl) => {
    open.value.gestion = ['/nuevo', '/atendidos', '/busqueda', '/enviados', '/porrecibir', '/recibidos', '/reportesEstandar'].includes(newUrl),
        open.value.pendientes = ['/porrecibir', '/recibidos'].includes(newUrl),
        open.value.tramitados = ['/enviados', '/atendidos'].includes(newUrl),
        open.value.admin = ['/usuario', '/accesos'].includes(newUrl)
}, { immediate: true });

</script>

<template>
    <input type="checkbox" name="" id="sidebar-toggle">
    <div class="sidebar h-screen overflow-y-auto">

        <div class="sidebar-brand">
            <div class="brand-flex">
                <img src="../../../img/logo.webp" alt="logo" class="imagen">
            </div>
        </div>

        <hr class="my-4 border-t border-gray-300">

        <div class="sidebar-main">

            <div class="sidebar-menu">
                <ul>
                    <li>
                        <a :href="route('inicio')"
                            :class="{ 'bg-cyan-500 active': $page.component === 'Contenido/Inicio' }">
                            <i class="fa-solid fa-house"></i>Inicio
                        </a>
                    </li>

                    <li>
                        <button @click="toggle('gestion')"
                            class="flex items-center w-full p-2 rounded hover:bg-gray-700">
                            <i class="fa-solid fa-folder mr-2"></i>
                            <span>Gestión Documentaria</span>
                            <i :class="open.gestion ? 'fa-chevron-up' : 'fa-chevron-down'" class="ml-auto fa-solid"></i>
                        </button>
                        <ul v-show="open.gestion" class="ulcajones">
                            <li v-if="permisos.nuevo">
                                <a :href="route('nuevo')" class="block p-2 rounded hover:bg-gray-700"
                                    :class="{ 'bg-cyan-500 active': $page.component === 'Contenido/Nuevo' }">
                                    <i class="fa-solid fa-file-circle-plus"></i>
                                    <span>Nuevo</span>
                                </a>
                            </li>
                            <li>
                                <button @click="toggle('pendientes')"
                                    class="flex items-center w-full p-2 rounded hover:bg-gray-700">
                                    <span><i class="fa-solid fa-clock"></i>Pendientes</span>
                                    <i :class="open.pendientes ? 'fa-chevron-up' : 'fa-chevron-down'"
                                        class="ml-auto fa-solid"></i>
                                </button>
                                <ul v-show="open.pendientes" class="ulcajones">
                                    <li v-if="permisos.porrecibir">
                                        <a :href="route('porrecibir')" class="bock p-2 rounded hover:bg-gray-700"
                                            :class="{ 'bg-cyan-500 active': $page.component === 'Contenido/PorRecibir' }">
                                            <i class="fa-solid fa-hand-holding"></i>Por Recibir</a>
                                    </li>
                                    <li v-if="permisos.recibidos"><a :href="route('recibidos')"
                                            class="block p-2 rounded hover:bg-gray-700"
                                            :class="{ 'bg-cyan-500 active': $page.component === 'Contenido/Recibidos' }">
                                            <i class="fa-solid fa-hand-holding-medical"></i>Recibidos</a>
                                    </li>
                                </ul>
                            </li>

                            <li>
                                <button @click="toggle('tramitados')"
                                    class="flex items-center w-full p-2 rounded hover:bg-gray-700">
                                    <span><i class="fa-solid fa-file-circle-plus"></i>Tramitados</span>
                                    <i :class="open.tramitados ? 'fa-chevron-up' : 'fa-chevron-down'"
                                        class="ml-auto fa-solid"></i>
                                </button>
                                <ul v-show="open.tramitados" class="ulcajones">
                                    <li v-if="permisos.enviados">
                                        <a :href="route('enviados')" class="bock p-2 rounded hover:bg-gray-700"
                                            :class="{ 'bg-cyan-500 active': $page.component === 'Contenido/Enviados' }">
                                            <i class="fa-regular fa-envelope"></i>Enviados</a>
                                    </li>
                                    <li v-if="permisos.atendidos"><a :href="route('atendidos')"
                                            class="block p-2 rounded hover:bg-gray-700"
                                            :class="{ 'bg-cyan-500 active': $page.component === 'Contenido/Atendidos' }">
                                            <i class="fa-solid fa-envelope-open-text"></i>Atendidos</a>
                                    </li>
                                </ul>
                            </li>
                            <li v-if="permisos.busqueda">
                                <a :href="route('busqueda')" class="block p-2 rounded hover:bg-gray-700"
                                    :class="{ 'bg-cyan-500 active': $page.component === 'Contenido/Busqueda' }">
                                    <i class="fa-solid fa-magnifying-glass"></i>Búsqueda</a>
                            </li>
                            <li v-if="permisos.busqueda">
                                <a :href="route('reportesEstandar')" class="block p-2 rounded hover:bg-gray-700"
                                    :class="{ 'bg-cyan-500 active': $page.component === 'Contenido/ReporteEstandar' }">
                                    <i class="fa-solid fa-file-export"></i>Reportes Estandar</a>
                            </li>
                        </ul>
                    </li>

                    <li v-if="permisos.usuario || permisos.accesos">
                        <button @click="toggle('admin')" class="flex items-center w-full p-2 rounded hover:bg-gray-700">
                            <i class="fa-solid fa-user-shield mr-2"></i>
                            <span>Administrador</span>
                            <i :class="open.admin ? 'fa-chevron-up' : 'fa-chevron-down'" class="ml-auto fa-solid"></i>
                        </button>
                        <ul v-show="open.admin" class="ulcajones">
                            <li v-if="permisos.usuario">
                                <a :href="route('usuario')" class="block p-2 rounded hover:bg-gray-700"
                                    :class="{ 'bg-cyan-500 active': $page.component === 'Contenido/Usuario' }">
                                    <i class="fa-solid fa-user-group"></i>Usuario</a>
                            </li>
                            <li v-if="permisos.accesos">

                                <a :href="route('accesos')" class="block p-2 rounded hover:bg-gray-700"
                                    :class="{ 'bg-cyan-500 active': $page.component === 'Contenido/Accesos' }">
                                    <i class="fa-solid fa-right-to-bracket"></i>Accesos</a>
                            </li>
                        </ul>
                    </li>
                </ul>
                <!--
                    <ul>
                        <li>
                            <a :href="route('perfil')" 
                            :class="{ 'active': $page.component === 'Principal/Perfil' }"
                            >
                                <i class="fa-solid fa-house"></i>
                                <p class="title-menu"> Perfil</p>
                            </a>
                        </li>
                    </ul>
                -->
                <hr class="my-4 border-t border-gray-300">
                <ul>
                    <li>
                        <Link :href="route('salir')" method="post" class="boton-salir">
                        <i class="fa-solid fa-reply-all"></i>
                        <p class="title-menu"> Salir</p>
                        </Link>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>