# AlfredoDaily02.github.io
Código de web para ejercicios, aqui el puede practicar preguntas del día a día 
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Estimulación Cognitiva Diaria</title>
    <style>
        :root {
            --bg: #f5f2eb;
            --primary: #2c5e4e;
            --accent: #e6a532;
            --text: #2b2b2b;
            --white: #ffffff;
            --blue-btn: #1E90FF;
            --green-btn: #2ecc71;
            --success: #5cb85c;
            --danger: #d9534f;
        }
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: var(--bg);
            color: var(--text);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
            font-size: 22px;
        }
        .screen {
            max-width: 850px;
            width: 100%;
            background: var(--white);
            border-radius: 35px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            padding: 40px 30px;
            text-align: center;
        }
        .hidden { display: none !important; }

        .welcome-title { font-size: 34px; color: var(--primary); margin-bottom: 20px; }
        .welcome-text { font-size: 24px; margin-bottom: 30px; line-height: 1.5; }
        .btn-start {
            background: var(--green-btn);
            color: white;
            font-size: 28px;
            padding: 18px 45px;
            border: none;
            border-radius: 60px;
            cursor: pointer;
            font-weight: bold;
            box-shadow: 0 8px 20px rgba(46,204,113,0.5);
            transition: 0.2s;
            margin-top: 15px;
        }
        .btn-start:hover { transform: scale(1.05); filter: brightness(1.1); }
        .table-container { margin-top: 30px; text-align: left; }
        table { width: 100%; border-collapse: collapse; font-size: 20px; margin-top: 10px; }
        th { background: var(--primary); color: white; padding: 12px; border-radius: 10px 10px 0 0; text-align: center; }
        td { padding: 10px; border-bottom: 1px solid #ccc; background: #fafafa; text-align: center; }
        .msg-low { color: #c0392b; font-weight: bold; }
        .msg-mid { color: #e67e22; font-weight: bold; }
        .msg-high { color: #2ecc71; font-weight: bold; }

        .top-buttons { display: flex; justify-content: space-between; margin-bottom: 25px; }
        .btn-back, .btn-results {
            background: var(--blue-btn);
            color: white;
            border: none;
            border-radius: 30px;
            padding: 12px 25px;
            font-size: 20px;
            font-weight: bold;
            cursor: pointer;
            box-shadow: 0 4px 12px rgba(30,144,255,0.4);
            transition: 0.2s;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .btn-back:hover, .btn-results:hover { transform: scale(1.05); filter: brightness(1.1); }
        .progress-bar { width: 100%; height: 14px; background: #ddd; border-radius: 10px; margin-bottom: 20px; overflow: hidden; }
        .progress-fill { width: 0%; height: 100%; background: var(--primary); transition: width 0.4s ease; }
        .step-title { font-size: 26px; font-weight: bold; color: var(--primary); margin-bottom: 15px; }
        .question { font-size: 28px; margin-bottom: 30px; line-height: 1.5; min-height: 100px; }
        .input-area { display: flex; flex-direction: column; align-items: center; gap: 20px; margin-bottom: 25px; }
        input[type="text"] {
            width: 80%; max-width: 500px; padding: 15px 20px; font-size: 24px;
            border: 3px solid var(--primary); border-radius: 15px; text-align: center; outline: none;
        }
        .options-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; justify-content: center; margin: 10px 0; }
        .option-btn {
            background: #f9f9f9; border: 2px solid var(--primary); border-radius: 15px;
            padding: 15px; font-size: 22px; cursor: pointer; transition: 0.2s; font-weight: bold; color: var(--text);
        }
        .option-btn:hover { background: #e6f0ec; border-color: var(--accent); }
        .option-btn.selected { background: var(--primary); color: white; border-color: var(--primary); }
        .buttons { display: flex; flex-wrap: wrap; justify-content: center; gap: 15px; margin-top: 10px; }
        button {
            font-size: 22px; padding: 14px 35px; border: none; border-radius: 50px;
            cursor: pointer; font-weight: bold; transition: all 0.2s; box-shadow: 0 5px 10px rgba(0,0,0,0.1);
            background: var(--primary); color: white; min-width: 160px;
        }
        button:hover { filter: brightness(1.15); transform: translateY(-2px); }
        button:active { transform: translateY(0); }
        .hint-btn { background: var(--accent); }
        .image-link-btn {
            background: #3498db; color: white; text-decoration: none;
            font-size: 20px; padding: 10px 25px; border-radius: 30px; display: inline-block; margin-top: 15px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }
        .feedback { font-size: 26px; margin: 20px 0; min-height: 40px; font-weight: bold; color: var(--primary); }
        .message-box {
            font-size: 24px; background: #e0f2e9; padding: 15px; border-radius: 15px; margin: 20px 0; color: #1a4d3a;
        }
        .modal {
            position: fixed; top: 0; left: 0; right: 0; bottom: 0;
            background: rgba(0,0,0,0.6); display: flex; justify-content: center; align-items: center; z-index: 1000;
        }
        .modal-content {
            background: white; border-radius: 30px; padding: 40px; text-align: center; max-width: 600px;
            width: 90%; box-shadow: 0 20px 40px rgba(0,0,0,0.3); animation: fadeIn 0.3s ease;
        }
        @keyframes fadeIn { from {opacity:0; transform:translateY(-20px);} to {opacity:1; transform:translateY(0);} }
        .celebration-emojis { font-size: 60px; margin: 20px 0; animation: bounce 0.6s infinite alternate; }
        @keyframes bounce { from {transform: scale(1);} to {transform: scale(1.2);} }
        .modal h2 { font-size: 34px; color: var(--primary); margin-bottom: 15px; }
        .modal p { font-size: 26px; margin: 15px 0; }
        .modal button { margin-top: 20px; background: var(--primary); font-size: 24px; }
        @media (max-width: 600px) {
            .screen { padding: 25px 15px; }
            .question { font-size: 24px; }
            button { font-size: 20px; padding: 12px 25px; }
            input[type="text"] { font-size: 22px; }
            .options-grid { grid-template-columns: 1fr; }
            .top-buttons { flex-direction: column; gap: 10px; }
        }
    </style>
</head>
<body>

<!-- PANTALLA PRINCIPAL -->
<div id="pantallaPrincipal" class="screen">
    <h1 class="welcome-title">🧠 Bienvenido, <span id="nombreUsuario">Alfredo</span></h1>
    <p class="welcome-text">Tu espacio diario de estimulación cognitiva.<br>Cada día 25 ejercicios nuevos. ¡Tú puedes!</p>
    <button class="btn-start" onclick="iniciarCuestionario()">▶ Comenzar</button>
    <div class="table-container" id="tablaInicio">
        <h2 style="color:var(--primary); margin-top:20px;">📋 Tus últimos 15 días</h2>
        <div id="tablaContainer"></div>
    </div>
</div>

<!-- PANTALLA DE PREGUNTAS -->
<div id="pantallaPreguntas" class="screen hidden">
    <div class="top-buttons">
        <button class="btn-back" onclick="regresarInicio()">↩ Regresar</button>
        <button class="btn-results" onclick="mostrarResultados()">📊 Ver Resultados</button>
    </div>
    <div class="progress-bar"><div id="progressFill" class="progress-fill"></div></div>
    <div class="step-title" id="stepTitle"></div>
    <div class="question" id="questionBox"></div>
    <div class="input-area" id="inputArea"></div>
    <div class="feedback" id="feedbackBox"></div>
    <div class="message-box hidden" id="extraMessage"></div>
</div>

<!-- MODALES -->
<div class="modal hidden" id="modalFelicitacion">
    <div class="modal-content">
        <h2>🎉 ¡Felicidades, vas muy bien!</h2><p>Sigue así, cada día mejoras.</p>
        <button onclick="cerrarModal('modalFelicitacion')">Continuar</button>
    </div>
</div>
<div class="modal hidden" id="modalCelebracion">
    <div class="modal-content">
        <h2>🏆 ¡Excelente, eres el mejor en esto!</h2>
        <div class="celebration-emojis">🎉🏆⚽💪🧠</div><p>¡Qué racha tan impresionante!</p>
        <button onclick="cerrarModal('modalCelebracion')">Continuar</button>
    </div>
</div>
<div class="modal hidden" id="modalResultados">
    <div class="modal-content" style="max-width:700px; max-height:80vh; overflow-y:auto;">
        <h2>📋 Resultados de los últimos 15 días</h2>
        <div id="tablaResultadoContainer"></div>
        <button onclick="cerrarModal('modalResultados')">Cerrar</button>
    </div>
</div>

<script>
    // ================== CONFIGURACIÓN ==================
    const CONFIG = {
        nombre: "Alfredo",
        ciudad: "San Nicolas",
        equipo: "Rayados",
        coloresEquipo: "azul y blanco",
        jugadores: ["Javier Quintero","Magdaleno Cano","Guarací Barbosa","Alfredo Jiménez","Ubirajara Chagas","Pepe Ledesma","Juan González","Paco Solís","Francisco Bertocchi","Luis Montoya","Nilo Acuña","Milton Carlos","Rubén Romeo Corbo","Pedro Damián Álvarez","Roberto Gasparini","Eduardo Cisneros","Héctor Castro","Rafael Puente","Vilson Tadei","Mario Mota de Souza Bahía","Reinaldo Güeldini","Francisco Javier Abuelo Cruz","Guillermo Muñoz","Germán Martellotto","Carlos Jara Saguier","Felipe de Jesús Muro","Antonio de Nigris","Jesús Arellano","Missael Espinoza","Luis Miguel Salvador","Sinha","Hugo Castillo","Guillermo Franco","Walter Erviti","Luis Pérez","Aldo de Nigris","Jonathan Orozco","Humberto Suazo","Severo Meza","Jesús Zavala","Hiram Mier","Jesús Manuel Corona","César Montes","Jonathan González","Carlos Rodríguez","Dorlan Pabón","Rogelio Funes Mori","Stefan Medina","Celso Ortiz","Vincent Janssen","Maxi Meza","Jesús Gallardo","Esteban Andrada","Germán Berterame","Sergio Canales","Héctor Moreno","Erick Aguirre","Víctor Guzmán","Rodrigo Aguirre","Alfonso González","Jordi Cortizo","Joao Rojas","Omar Govea","Luis Cárdenas","César Garza","Alex Fernandes","Gastón Obledo","Gerardo Arteaga","Gerardo Flores","Gerardo Galindo","Gerardo Jiménez","Gerardo Moreno","Guillermo Rojas","Francisco Avilán","Félix Ayala","Juan Manuel Azuara","Claudio Lostaunau","Ángel Lama","Raúl Chávez","Carlos Alanís","Lucas Albertengo","Sebastián Abreu","José Abundis","Daniel Aceves","Gael Acosta","César Adame","André Aguilar","Daniel Aguirre","Sebastián Vegas","Nicolas Sanchez","Alberto García","Ruben Ruiz Diaz","Felipe Baloy","Diego Ordaz","Oscar Dautt","Ricardo Martínez","Omar Ortiz","Horacio Casarín","Claudio Lostanau","Francisco Bertocchi","Juan Ahuntchaín","Roberto Gomez Junco","Mike Getchell","Carlos González","Aníbal González","Edson Gutiérrez","Fabián Guevara","Marcelo Gracia","Leandro Gracián","Axel Grijalva","Walter Gargano","Jair García","Miguel García","Javier García","Pablo Barrera","Neri Cardozo","Lucas Silva","Efraín Juárez","Omar Bravo","Darío Carreño","Jared Borgetti","Sergio Santana","Jesús Corona","Francisco Torres","Duilio Davino","Sebastián Méndez","Walter Ayoví","Juan Carlos Medina","José María Basanta","Severo Meza","Carlos Sánchez","Edwin Cardona","Yimmi Chará","Avilés Hurtado","Alfonso Alvarado","Edson Resendez","Hugo González","Arturo González","Rodolfo Pizarro","Miguel Layún","Nicolás Sánchez","Adam Bareiro","Leonel Vangioni","Matías Kranevitter","Stefan Medina","Jesús Zavala"],
        otrosEquipos: ["Tigres","América","Chivas","Cruz Azul","Pachuca","Atlas"]
    };
    document.getElementById("nombreUsuario").textContent = CONFIG.nombre;

    // ================== TRADUCCIONES PARA GOOGLE IMAGES ==================
    const traducciones = {
        "cama":"bed","estufa":"stove","refrigerador":"refrigerator","jabón":"soap","toalla":"towel",
        "lámpara":"lamp","almohada":"pillow","mesa":"table","silla":"chair","sofá":"sofa",
        "televisión":"television","microondas":"microwave","licuadora":"blender","lavadora":"washing machine",
        "espejo":"mirror","cortina":"curtain","alfombra":"rug","cuadro":"painting","plato":"plate",
        "vaso":"glass","tenedor":"fork","cuchillo":"knife","cuchara":"spoon","sartén":"frying pan",
        "olla":"pot","escoba":"broom","trapeador":"mop","plancha":"iron","ventilador":"fan",
        "reloj de pared":"wall clock","perchero":"coat rack","bote de basura":"trash can",
        "cafetera":"coffee maker","taza":"mug","librero":"bookshelf","alacena":"pantry",
        "burro de planchar":"ironing board","secadora":"dryer",
        "Torre Eiffel":"Eiffel Tower","Chichén Itzá":"Chichen Itza","Taj Mahal":"Taj Mahal",
        "Coliseo Romano":"Colosseum","Gran Muralla China":"Great Wall of China",
        "Cristo Redentor":"Christ the Redeemer","Machu Picchu":"Machu Picchu","Petra":"Petra"
    };

    const TOTAL_PREGUNTAS_DIA = 25;
    const TOTAL_BANCO = 750;
    let bancoPreguntas = [];
    let preguntasDelDia = [];
    let indicePreguntaActual = 0;
    let aciertosHoy = 0, erroresHoy = 0, rachaAciertos = 0, totalRespondidas = 0;
    let diaCompletado = false, sesionIniciada = false;
    let preguntaYaRespondida = false;   // nueva bandera

    // ================== NAVEGACIÓN ==================
    function mostrarPantalla(idMostrar, idOcultar) {
        document.getElementById(idOcultar).classList.add("hidden");
        document.getElementById(idMostrar).classList.remove("hidden");
    }
    function regresarInicio() {
        guardarProgresoActual();
        mostrarPantalla("pantallaPrincipal","pantallaPreguntas");
        mostrarTablaInicio();
    }
    function iniciarCuestionario() {
        const fechaHoy = new Date().toISOString().split("T")[0];
        const progresoGuardado = JSON.parse(localStorage.getItem("progresoActual") || "{}");
        if (progresoGuardado.fecha === fechaHoy && progresoGuardado.completado) {
            if (confirm("Hoy ya completaste tu sesión. ¿Quieres repetirla? (Se borrará el resultado de hoy)")) {
                localStorage.removeItem("progresoActual"); localStorage.removeItem("ultimoDiaCompletado");
                let historial = JSON.parse(localStorage.getItem("historialCognitivo") || "[]");
                historial = historial.filter(h => h.fecha !== fechaHoy);
                localStorage.setItem("historialCognitivo", JSON.stringify(historial));
            } else return;
        }
        if (progresoGuardado.fecha === fechaHoy && !progresoGuardado.completado) {
            indicePreguntaActual = progresoGuardado.indice || 0;
            aciertosHoy = progresoGuardado.aciertos || 0; erroresHoy = progresoGuardado.errores || 0;
            rachaAciertos = progresoGuardado.racha || 0; totalRespondidas = progresoGuardado.totalRespondidas || 0;
            sesionIniciada = true;
        } else {
            indicePreguntaActual = 0; aciertosHoy = 0; erroresHoy = 0; rachaAciertos = 0; totalRespondidas = 0;
            sesionIniciada = true;
            bancoPreguntas = generarBancoPreguntas();
            cargarPreguntasDelDia();
            localStorage.removeItem("progresoActual");
        }
        mostrarPantalla("pantallaPreguntas","pantallaPrincipal");
        mostrarPregunta();
    }
    function guardarProgresoActual() {
        if (!sesionIniciada || diaCompletado) return;
        const progreso = {
            fecha: new Date().toISOString().split("T")[0], indice: indicePreguntaActual,
            aciertos: aciertosHoy, errores: erroresHoy, racha: rachaAciertos,
            totalRespondidas: totalRespondidas, completado: false
        };
        localStorage.setItem("progresoActual", JSON.stringify(progreso));
    }

    // ================== GENERACIÓN DEL BANCO (750 PREGUNTAS ÚNICAS) ==================
    function generarBancoPreguntas() {
        let banco = [];
        let textosUsados = new Set();
        function agregarPregunta(obj) {
            if (textosUsados.has(obj.pregunta)) return false;
            textosUsados.add(obj.pregunta);
            banco.push(obj);
            return true;
        }

        // Matemáticas: triples sumas (80), combinadas (90), series (50)
        for (let i=0; i<80; i++) {
            let a = Math.floor(Math.random()*7)+2, b = Math.floor(Math.random()*7)+2, c = Math.floor(Math.random()*7)+2;
            let res = a+b+c;
            agregarPregunta({
                tipo:"matematica", pregunta:`¿Cuánto es ${a} + ${b} + ${c}?`, respuesta:[String(res)],
                pista:"Suma los tres números.", opciones:[String(res-2),String(res),String(res+1),String(res+2)].sort(()=>Math.random()-0.5)
            });
        }
        for (let i=0; i<90; i++) {
            let a = Math.floor(Math.random()*5)+3, b = Math.floor(Math.random()*5)+2;
            let mul = [2,3,4][Math.floor(Math.random()*3)];
            let res = (a+b)*mul;
            agregarPregunta({
                tipo:"matematica", pregunta:`¿Cuánto es (${a} + ${b}) × ${mul}?`, respuesta:[String(res)],
                pista:`Primero suma ${a}+${b}=${a+b}, luego multiplica por ${mul}.`,
                opciones:[String(res-2),String(res),String(res+2),String(res+4)].sort(()=>Math.random()-0.5)
            });
        }
        for (let i=0; i<50; i++) {
            let inicio = Math.floor(Math.random()*3)+1;
            let paso = [2,3][Math.floor(Math.random()*2)];
            let serie = [inicio, inicio+paso, inicio+paso*2, inicio+paso*3, inicio+paso*4];
            let pos = Math.floor(Math.random()*3)+2;
            agregarPregunta({
                tipo:"matematica", pregunta:`Completa: ${serie.slice(0,pos).join(", ")} , __`,
                respuesta:[String(serie[pos])], pista:`Suma ${paso} cada vez.`,
                opciones:[String(serie[pos]-1),String(serie[pos]),String(serie[pos]+1),String(serie[pos]+2)].sort(()=>Math.random()-0.5)
            });
        }

        // Objetos del hogar (38 objetos, 10 preg cada uno = 380)
        const objetosHogar = [
            {nombre:"cama",pista:"Mueble para dormir."},{nombre:"estufa",pista:"Sirve para cocinar."},
            {nombre:"refrigerador",pista:"Mantiene fríos los alimentos."},{nombre:"jabón",pista:"Se usa en el baño para lavarse."},
            {nombre:"toalla",pista:"Para secarse después del baño."},{nombre:"lámpara",pista:"Da luz en la habitación."},
            {nombre:"almohada",pista:"Apoyas la cabeza al dormir."},{nombre:"mesa",pista:"Mueble para comer o apoyar cosas."},
            {nombre:"silla",pista:"Mueble para sentarse."},{nombre:"sofá",pista:"Asiento cómodo para varias personas."},
            {nombre:"televisión",pista:"Aparato para ver programas y películas."},{nombre:"microondas",pista:"Calienta la comida rápidamente."},
            {nombre:"licuadora",pista:"Sirve para batir y triturar alimentos."},{nombre:"lavadora",pista:"Limpia la ropa sucia."},
            {nombre:"espejo",pista:"Refleja tu imagen."},{nombre:"cortina",pista:"Cubre las ventanas para dar privacidad."},
            {nombre:"alfombra",pista:"Cubre el suelo para dar calidez."},{nombre:"cuadro",pista:"Decoración para las paredes."},
            {nombre:"plato",pista:"Recipiente para servir comida."},{nombre:"vaso",pista:"Recipiente para beber líquidos."},
            {nombre:"tenedor",pista:"Utensilio para pinchar comida."},{nombre:"cuchillo",pista:"Sirve para cortar alimentos."},
            {nombre:"cuchara",pista:"Para comer sopas o alimentos líquidos."},{nombre:"sartén",pista:"Recipiente para freír alimentos."},
            {nombre:"olla",pista:"Recipiente profundo para cocer alimentos."},{nombre:"escoba",pista:"Sirve para barrer el suelo."},
            {nombre:"trapeador",pista:"Se usa para limpiar el suelo mojado."},{nombre:"plancha",pista:"Quita las arrugas de la ropa."},
            {nombre:"ventilador",pista:"Mueve el aire para refrescar."},{nombre:"reloj de pared",pista:"Indica la hora en la casa."},
            {nombre:"perchero",pista:"Lugar para colgar abrigos o bolsos."},{nombre:"bote de basura",pista:"Donde se arrojan los desperdicios."},
            {nombre:"cafetera",pista:"Máquina para preparar café."},{nombre:"taza",pista:"Recipiente con asa para bebidas calientes."},
            {nombre:"librero",pista:"Mueble para organizar libros."},{nombre:"alacena",pista:"Armario para guardar víveres."},
            {nombre:"burro de planchar",pista:"Soporte para planchar la ropa."},{nombre:"secadora",pista:"Elimina la humedad de la ropa."}
        ];
        objetosHogar.forEach(obj => {
            for (let i=0; i<10; i++) {
                let opciones = [obj.nombre, objetosHogar[Math.floor(Math.random()*objetosHogar.length)].nombre, objetosHogar[Math.floor(Math.random()*objetosHogar.length)].nombre].sort(()=>Math.random()-0.5);
                agregarPregunta({
                    tipo:"imagen", pregunta:"¿Qué objeto es este?", objeto: obj.nombre, eng: traducciones[obj.nombre] || obj.nombre,
                    respuesta:[obj.nombre], pista:obj.pista, opciones: opciones
                });
            }
        });

        // Lugares del mundo (8 lugares, 10 preg c/u = 80)
        const lugares = [
            {nombre:"Torre Eiffel",pista:"Está en París."},{nombre:"Chichén Itzá",pista:"Pirámide maya en México."},
            {nombre:"Taj Mahal",pista:"Mausoleo en India."},{nombre:"Coliseo Romano",pista:"Anfiteatro antiguo en Italia."},
            {nombre:"Gran Muralla China",pista:"Enorme muralla en Asia."},{nombre:"Cristo Redentor",pista:"Estatua en Río de Janeiro."},
            {nombre:"Machu Picchu",pista:"Ciudadela inca en Perú."},{nombre:"Petra",pista:"Ciudad tallada en roca en Jordania."}
        ];
        lugares.forEach(lugar => {
            for (let i=0; i<10; i++) {
                let opciones = [lugar.nombre, lugares[Math.floor(Math.random()*lugares.length)].nombre, lugares[Math.floor(Math.random()*lugares.length)].nombre].sort(()=>Math.random()-0.5);
                agregarPregunta({
                    tipo:"imagen", pregunta:"¿Qué lugar famoso es este?", objeto: lugar.nombre, eng: traducciones[lugar.nombre] || lugar.nombre,
                    respuesta:[lugar.nombre], pista:lugar.pista, opciones: opciones
                });
            }
        });

        // Memoria verbal (70)
        const triosMemoria = [
            ["cama","estufa","jabón"],["gol","estadio","Rayados"],["cocina","baño","recámara"],
            ["pelota","portería","árbitro"],["leche","pan","huevo"],["sol","luna","estrella"],
            ["martillo","clavo","serrucho"],["perro","gato","conejo"],["lápiz","goma","cuaderno"],
            ["manzana","pera","plátano"],["rojo","azul","amarillo"],["guitarra","piano","trompeta"],
            ["avión","carro","barco"],["ratón","teclado","monitor"],["nube","lluvia","trueno"],
            ["camisa","suéter","pantalón"]
        ];
        for (let i=0; i<70; i++) {
            let trio = triosMemoria[Math.floor(Math.random()*triosMemoria.length)];
            agregarPregunta({
                tipo:"memoria", pregunta:`Repite estas 3 palabras: <strong>${trio.join(", ")}</strong>. Escríbelas separadas por comas.`,
                palabras:trio, respuesta:trio, pista:`La primera es "${trio[0]}".`
            });
        }

        // Fútbol (100)
        for (let i=0; i<25; i++) {
            let jugador = CONFIG.jugadores[Math.floor(Math.random()*CONFIG.jugadores.length)];
            agregarPregunta({
                tipo:"futbol", pregunta:`Nombra un jugador de ${CONFIG.equipo}.`,
                respuesta: CONFIG.jugadores.slice(0,50), pista:`Uno empieza con ${jugador.charAt(0)}...`
            });
        }
        for (let i=0; i<25; i++) {
            agregarPregunta({
                tipo:"futbol", pregunta:"¿De qué color es la camiseta de Rayados?",
                respuesta:["azul y blanco a rayas","rayada"], pista:"Tiene rayas como un tigre pero invertidas."
            });
        }
        for (let i=0; i<25; i++) {
            let equipo = CONFIG.otrosEquipos[Math.floor(Math.random()*CONFIG.otrosEquipos.length)];
            agregarPregunta({
                tipo:"futbol", pregunta:"Nombra otro equipo del fútbol mexicano.",
                respuesta: CONFIG.otrosEquipos, pista:`Uno es ${equipo}.`
            });
        }
        for (let i=0; i<25; i++) {
            agregarPregunta({
                tipo:"futbol", pregunta:"¿Qué sucede cuando un equipo mete un gol?",
                respuesta:["grito","celebra","abrazo","salta","gol"], pista:"La gente se pone feliz y grita."
            });
        }

        // Opción múltiple variada (resto hasta 750)
        while (banco.length < TOTAL_BANCO) {
            let tipoAleatorio = Math.floor(Math.random()*3);
            if (tipoAleatorio === 0) {
                let a = Math.floor(Math.random()*8)+2, b = Math.floor(Math.random()*8)+2;
                let res = a*b;
                agregarPregunta({
                    tipo:"opcionMultiple", pregunta:`¿Cuánto es ${a} × ${b}?`,
                    respuesta:[String(res)], opciones:[String(res-1),String(res),String(res+1),String(res+2)].sort(()=>Math.random()-0.5),
                    pista:"Multiplica."
                });
            } else if (tipoAleatorio === 1) {
                const dias = ["lunes","martes","miércoles","jueves","viernes","sábado","domingo"];
                let indice = Math.floor(Math.random()*7);
                let diaPregunta = dias[indice], diaRespuesta = dias[(indice+1)%7];
                agregarPregunta({
                    tipo:"orientacion", pregunta:`¿Qué día viene después del ${diaPregunta}?`,
                    respuesta:[diaRespuesta], pista:"La semana tiene 7 días."
                });
            } else {
                agregarPregunta({
                    tipo:"orientacion", pregunta:`¿En qué ciudad vives?`,
                    respuesta:[CONFIG.ciudad], pista:"Empieza con San..."
                });
            }
        }

        // Barajar
        for (let i=banco.length-1; i>0; i--) {
            const j = Math.floor(Math.random()*(i+1));
            [banco[i], banco[j]] = [banco[j], banco[i]];
        }
        return banco;
    }

    function cargarPreguntasDelDia() {
        const diaAnio = getDayOfYear();
        const bloque = (diaAnio-1) % 30;
        // Tomamos 25 preguntas únicas de la sección correspondiente
        let inicio = bloque * TOTAL_PREGUNTAS_DIA;
        preguntasDelDia = bancoPreguntas.slice(inicio, inicio+TOTAL_PREGUNTAS_DIA);
        // Si por alguna razón hay menos (poco probable), rellenamos con otras aleatorias no usadas
        while (preguntasDelDia.length < TOTAL_PREGUNTAS_DIA) {
            let extra = bancoPreguntas.find(p => !preguntasDelDia.includes(p));
            if (extra) preguntasDelDia.push(extra); else break;
        }
        preguntasDelDia = preguntasDelDia.slice(0,TOTAL_PREGUNTAS_DIA);
    }

    function getDayOfYear() {
        const now = new Date();
        const start = new Date(now.getFullYear(),0,0);
        return Math.floor((now-start)/86400000);
    }
    function normalizar(str) {
        return str.normalize("NFD").replace(/[\u0300-\u036f]/g,"").toLowerCase().trim();
    }
    function esCorrecta(respuestaUsuario, respuestasEsperadas) {
        const norm = normalizar(respuestaUsuario);
        return respuestasEsperadas.some(r => normalizar(r) === norm);
    }

    // ================== MOSTRAR PREGUNTA ==================
    function actualizarProgreso() {
        const porcentaje = (totalRespondidas/TOTAL_PREGUNTAS_DIA)*100;
        progressFill.style.width = porcentaje+"%";
        stepTitle.textContent = `Pregunta ${totalRespondidas+1} de ${TOTAL_PREGUNTAS_DIA}`;
    }

    function mostrarPregunta() {
        if (indicePreguntaActual >= preguntasDelDia.length) { finalizarDia(); return; }
        preguntaYaRespondida = false;  // reiniciar bandera
        actualizarProgreso();
        const pregunta = preguntasDelDia[indicePreguntaActual];
        questionBox.innerHTML = pregunta.pregunta;
        // Si es pregunta con imagen (objeto/lugar), mostramos botón de enlace Google
        if (pregunta.tipo === "imagen" && pregunta.eng) {
            const engWord = pregunta.eng;
            questionBox.innerHTML += `<br><a class="image-link-btn" href="https://www.google.com/search?tbm=isch&q=${encodeURIComponent(engWord)}" target="_blank">🔍 Ver imagen</a>`;
        }
        inputArea.innerHTML = "";
        if (pregunta.opciones && pregunta.opciones.length > 1) {
            const optionsGrid = document.createElement("div");
            optionsGrid.className = "options-grid";
            pregunta.opciones.forEach(opt => {
                const btn = document.createElement("button");
                btn.className = "option-btn"; btn.textContent = opt;
                btn.addEventListener("click", () => {
                    if (preguntaYaRespondida) return;  // no hace nada si ya respondió
                    document.querySelectorAll(".option-btn").forEach(b => b.classList.remove("selected"));
                    btn.classList.add("selected");
                    verificarRespuesta(opt);
                });
                optionsGrid.appendChild(btn);
            });
            inputArea.appendChild(optionsGrid);
        } else {
            inputArea.innerHTML = `
                <input type="text" id="answerInput" placeholder="Escribe tu respuesta..." autocomplete="off">
                <div class="buttons">
                    <button id="submitBtn">✔ Revisar</button>
                    <button id="hintBtn" class="hint-btn">💡 Pista</button>
                </div>`;
            const answerInputEl = document.getElementById("answerInput");
            answerInputEl.focus();
            document.getElementById("submitBtn").addEventListener("click", () => {
                if (preguntaYaRespondida) return;
                verificarRespuesta(answerInputEl.value);
            });
            document.getElementById("hintBtn").addEventListener("click", () => {
                if (!preguntaYaRespondida) mostrarFeedback(`💡 ${pregunta.pista || "Piensa con calma."}`, "#e6a532");
            });
            answerInputEl.addEventListener("keypress", (e) => {
                if (e.key === "Enter" && !preguntaYaRespondida) verificarRespuesta(answerInputEl.value);
            });
        }
        document.getElementById("feedbackBox").textContent = "";
        document.getElementById("extraMessage").classList.add("hidden");
        const existingNext = document.getElementById("nextBtn");
        if (existingNext) existingNext.remove();
    }

    function verificarRespuesta(respuesta) {
        if (preguntaYaRespondida) return;  // Evita doble registro
        preguntaYaRespondida = true;
        const pregunta = preguntasDelDia[indicePreguntaActual];
        let correcta = false;
        if (pregunta.tipo === "memoria") {
            const palabrasUser = respuesta.split(/[, ]+/).filter(w => w.length>0).map(normalizar);
            const esperadas = pregunta.palabras.map(normalizar);
            const coincidencias = palabrasUser.filter(w => esperadas.includes(w)).length;
            correcta = coincidencias >= 2;
        } else {
            correcta = esCorrecta(respuesta, pregunta.respuesta);
        }
        if (correcta) {
            aciertosHoy++; rachaAciertos++; totalRespondidas++;
            mostrarFeedback("✅ ¡Correcto!", "var(--success)");
            if (aciertosHoy % 3 === 0 && aciertosHoy > 0) setTimeout(() => mostrarModal("modalFelicitacion"), 500);
            if (rachaAciertos % 5 === 0 && rachaAciertos > 0) setTimeout(() => mostrarModal("modalCelebracion"), 800);
        } else {
            erroresHoy++; rachaAciertos = 0; totalRespondidas++;
            mostrarFeedback("❌ No es correcto, pero no te preocupes.", "var(--danger)");
            document.getElementById("extraMessage").textContent = `La respuesta era: ${pregunta.respuesta.join(" o ")}`;
            document.getElementById("extraMessage").classList.remove("hidden");
        }
        actualizarProgreso();
        guardarProgresoActual();
        // Agregar botón siguiente
        const buttonsDiv = inputArea.querySelector(".buttons");
        if (!document.getElementById("nextBtn")) {
            const nextBtn = document.createElement("button");
            nextBtn.id = "nextBtn"; nextBtn.textContent = "▶ Siguiente";
            nextBtn.addEventListener("click", () => { indicePreguntaActual++; mostrarPregunta(); });
            if (buttonsDiv) buttonsDiv.appendChild(nextBtn);
            else inputArea.appendChild(nextBtn);
        }
        if (document.getElementById("answerInput")) document.getElementById("answerInput").disabled = true;
        if (document.getElementById("submitBtn")) document.getElementById("submitBtn").disabled = true;
        if (document.getElementById("hintBtn")) document.getElementById("hintBtn").disabled = true;
    }

    function mostrarFeedback(texto, color="var(--primary)") {
        const fb = document.getElementById("feedbackBox");
        fb.textContent = texto; fb.style.color = color;
    }

    function finalizarDia() {
        diaCompletado = true;
        const porcentaje = Math.round((aciertosHoy/TOTAL_PREGUNTAS_DIA)*100);
        let mensaje = porcentaje <= 70 ? "Vamos a mejorar, tú puedes" :
                      (porcentaje <= 80 ? "Es un buen resultado, felicidades" : "Felicidades, puedes con esto y más");
        guardarResultado(porcentaje, mensaje);
        questionBox.innerHTML = `<h2>🎯 ¡Sesión completada!</h2><p>Acertaste <strong>${aciertosHoy}</strong> de ${TOTAL_PREGUNTAS_DIA} (${porcentaje}%).</p><p>${mensaje}</p>`;
        inputArea.innerHTML = `<button onclick="iniciarCuestionario()" style="margin-top:20px;">Iniciar nueva sesión</button>`;
        progressFill.style.width = "100%"; stepTitle.textContent = "Resultado del día";
        document.getElementById("feedbackBox").textContent = "";
        document.getElementById("extraMessage").classList.add("hidden");
        let progreso = JSON.parse(localStorage.getItem("progresoActual")||"{}");
        progreso.completado = true;
        localStorage.setItem("progresoActual", JSON.stringify(progreso));
        localStorage.setItem("ultimoDiaCompletado", new Date().toISOString().split("T")[0]);
    }

    function guardarResultado(porcentaje, mensaje) {
        const fecha = new Date().toISOString().split("T")[0];
        const diasSemana = ["domingo","lunes","martes","miércoles","jueves","viernes","sábado"];
        const diaSemana = diasSemana[new Date().getDay()];
        let historial = JSON.parse(localStorage.getItem("historialCognitivo")||"[]");
        historial = historial.filter(h => h.fecha !== fecha);
        historial.push({fecha, diaSemana, porcentaje, mensaje, aciertos:aciertosHoy, total:TOTAL_PREGUNTAS_DIA});
        if (historial.length > 15) historial = historial.slice(-15);
        localStorage.setItem("historialCognitivo", JSON.stringify(historial));
        mostrarTablaInicio();
    }

    function mostrarTablaInicio() {
        const container = document.getElementById("tablaContainer");
        let historial = JSON.parse(localStorage.getItem("historialCognitivo")||"[]");
        if (historial.length===0) { container.innerHTML="<p>Aún no hay sesiones registradas.</p>"; return; }
        let html = `<table><tr><th>Fecha</th><th>Día</th><th>Calificación</th><th>Mensaje</th></tr>`;
        historial.slice().reverse().forEach(entry => {
            html += `<tr><td>${entry.fecha}</td><td>${entry.diaSemana}</td><td>${entry.porcentaje}%</td>
                     <td class="${entry.porcentaje <= 70 ? 'msg-low' : entry.porcentaje <= 80 ? 'msg-mid' : 'msg-high'}">${entry.mensaje}</td></tr>`;
        });
        html += "</table>"; container.innerHTML = html;
    }

    function mostrarResultados() {
        let historial = JSON.parse(localStorage.getItem("historialCognitivo")||"[]");
        const container = document.getElementById("tablaResultadoContainer");
        if (historial.length===0) { container.innerHTML="<p>Aún no hay sesiones registradas.</p>"; }
        else {
            let html = `<table><tr><th>Fecha</th><th>Día</th><th>Calificación</th><th>Mensaje</th></tr>`;
            historial.slice().reverse().forEach(entry => {
                html += `<tr><td>${entry.fecha}</td><td>${entry.diaSemana}</td><td>${entry.porcentaje}%</td>
                         <td class="${entry.porcentaje <= 70 ? 'msg-low' : entry.porcentaje <= 80 ? 'msg-mid' : 'msg-high'}">${entry.mensaje}</td></tr>`;
            });
            html += "</table>"; container.innerHTML = html;
        }
        mostrarModal("modalResultados");
    }

    function cerrarModal(id) { document.getElementById(id).classList.add("hidden"); }
    function mostrarModal(id) { document.getElementById(id).classList.remove("hidden"); }

    // ================== INICIALIZACIÓN ==================
    window.addEventListener("load", () => {
        mostrarTablaInicio();
        const progresoGuardado = JSON.parse(localStorage.getItem("progresoActual")||"{}");
        const fechaHoy = new Date().toISOString().split("T")[0];
        if (progresoGuardado.fecha === fechaHoy && !progresoGuardado.completado) {
            bancoPreguntas = generarBancoPreguntas();
            cargarPreguntasDelDia();
        } else if (!progresoGuardado.fecha || progresoGuardado.fecha !== fechaHoy) {
            bancoPreguntas = generarBancoPreguntas();
            cargarPreguntasDelDia();
        }
    });
    document.addEventListener("keydown", (e) => {
        if (e.key==="Escape") {
            cerrarModal("modalFelicitacion"); cerrarModal("modalCelebracion"); cerrarModal("modalResultados");
        }
    });
</script>
</body>
</html>
