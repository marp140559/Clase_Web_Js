<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Proyecto 2</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="min-h-screen flex items-center justify-center">
    <div class="w-full max-w-md mx-auto bg-white rounded-xl shadow-md overflow-hidden md:max-w-2xl">
        <div class="">
            <div class="full p-4">
                <h1 class="text-2xl font-bold text-center mb-6">Lista de Tareas</h1>
                <div class="mb-4 flex">
                    <input type="text" id="nueva_tarea" value="" class="flex-1 p-2 border border-gray-300 rounded-l-lg ">
                    <button onclick="agregarNuevo()" class="bg-blue-500 text-white p-2 rounded-r-lg">Agregar</button>
                </div>
                <ul id="lista_tareas" class="list-none p-0">
                    <li>Valor por defecto</li>
                </ul>

            </div>

        </div>

    </div>

    

    <script>
        var listado_tareas = [];

        function agregarNuevo(){
            // alert("AGREGANDO...")
            const nuevaTarea = document.getElementById("nueva_tarea").value;
            if(nuevaTarea){
                listado_tareas.push(nuevaTarea);
                localStorage.setItem("Mis-tareas", JSON.stringify(listado_tareas))
                listarTareas()
            }

        }

        function listarTareas(){
            listado_tareas = JSON.parse(localStorage.getItem("Mis-tareas"));

            const listaT = document.getElementById('lista_tareas');
            listaT.innerHTML = ""
            listado_tareas.forEach((tarea, posicion) => {
                listaT.innerHTML = listaT.innerHTML + `
                    <li class="flex justify-between items-center bg-gray-100 rounded-lg shadow-md p-2 mb-2"> ${tarea} <button onClick="eliminarTarea(${posicion})" class="bg-red-500 text-white p-1 rounded-lg">X</button> </li>
                `
            });
        }

        function eliminarTarea(pos){
            listado_tareas.splice(pos, 1);
            localStorage.setItem("Mis-tareas", JSON.stringify(listado_tareas))

            listarTareas()
        }
        listarTareas()
    </script>

</body>
</html>