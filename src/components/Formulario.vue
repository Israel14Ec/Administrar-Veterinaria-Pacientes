<template>
    
    <div class="md:w-1/2">
        <h2 class="font-bold text-3xl text-center">Seguimiento Pacientes</h2>
        
        <p class="text-lg mt-5 text-center mb-10">
            Añade Pacientes y
            <span class="text-indigo-600 font-bold">Adminístralos</span>
        </p>

        <Alerta
            v-if="alerta.mensaje"
            :alerta="alerta"
        />

        <form 
            class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
            @submit.prevent = "validar"
        >
            <div class="mb-5">
                <label 
                    for="mascota"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Nombre Mascota:
                </label>

                <input 
                    type="text"
                    id="mascota"
                    placeholder="Nombre de la mascota"
                    class="border-2 w-full p-1 mt-2 placeholder-gray-400 rounded-md"
                    :value="nombre"
                    @input= "$emit('update:nombre', $event.target.value)"
                >
            </div>


            <div class="mb-5">
                <label 
                    for="Cuidador"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Nombre del cuidador:
                </label>

                <input 
                    type="text"
                    id="Cuidador"
                    placeholder="Nombre del cuidador"
                    class="border-2 w-full p-1 mt-2 placeholder-gray-400 rounded-md"
                    :value="cuidador"
                    @input= "$emit('update:cuidador', $event.target.value)"
                    
                >
            </div>

            <div class="mb-5">
                <label 
                    for="email"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Email:
                </label>

                <input 
                    type="email"
                    id="email"
                    placeholder="email de contacto"
                    class="border-2 w-full p-1 mt-2 placeholder-gray-400 rounded-md"
                    :value="email"
                    @input= "$emit('update:email', $event.target.value)"
                   
                >
            </div>


            <div class="mb-5">
                <label 
                    for="Alta"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Alta:
                </label>

                <input 
                    type="date"
                    id="Alta"
                    placeholder="Alta"
                    class="border-2 w-full p-1 mt-2 placeholder-gray-400 rounded-md"
                    :value="alta"
                    @input= "$emit('update:alta', $event.target.value)"
                >
            </div>


            <div class="mb-5">
                <label 
                    for="Sintomas"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Sintomas:
                </label>

            <textarea 
                id="sintomas"
                placeholder="Describe los sintomas" 
                class="border-2 w-full p-1 mt-2 placeholder-gray-400 rounded-md h-20"
                :value="sintomas"
                @input= "$emit('update:sintomas', $event.target.value)"
            >
            </textarea>
            </div>

            <input 
                type="submit"
                class="bg-indigo-600 w-full p-3 
                text-white uppercase 
                font-bold 
                hover:bg-indigo-700 
                cursor-pointer 
                transition-colors"
                :value="[editando ? 'Guardar Cambios' : 'Registrar Paciente']"
            >

        </form>
    </div>
</template>


<script setup>

    import Alerta from './Alerta.vue'
    import {reactive, computed} from 'vue'

    const alerta = reactive ({
        tipo: '',
        mensaje: ''
    })

    const validar = () => {
        if(Object.values(props).includes('')) {
            alerta.mensaje = 'Todos los campos son obligatorios'
            alerta.tipo = 'error'
            return
        }

        emit('guardar-paciente')
        alerta.mensaje = ''
        alerta.tipo = 'exito'

        setTimeout(() => {
            Object.assign(alerta, {
                tipo: '',
                mensaje: ''
            })
        }, 3000)   
    }

    const emit = defineEmits(['update:nombre', 'update:cuidador', 'update:email', 'update:alta', 'update:sintomas', 'guardar-paciente'])

    const props = defineProps({

        id: {
            type: [String, null],
            required: true
        },
        nombre: {
            type: String,
            required: true
        },
        cuidador: {
            type: String,
            required: true
        },
        email: {
            type: String,
            required: true
        },
        alta: {
            type: String,
            required: true
        },
        sintomas: {
            type: String,
            required: true
        }
    })

    const editando = computed(() => {
        return props.id
    })

</script>