classDiagram
    class GameManager {
        -puntaje
        -puntosPorSancion
        -saludEcosistema
        -tiempoRestante
        -partidaActiva
        +iniciarNivel()
        +actualizar()
        +procesarToque()
        +crearAMP()
        +sumarPuntos()
        +actualizarSaludEcosistema()
        +evaluarVictoriaMRS()
        +finalizarNivel()
    }

    class SpawnerEmbarcaciones {
        -intervaloAparicion
        -temporizadorSpawn
        +actualizar()
        +generarBarco()
    }

    class Embarcacion {
        -id
        -esIlegal
        -posX
        -posY
        -velocidad
        +desplazar()
        +colisionaConPunto()
        +eliminar()
    }

    class Ruta {
        -totalPuntos
        +obtenerSiguientePunto()
    }

    class AreaMarinaProtegida {
        -id
        -cantidadPuntosTrazo
        -duracionRestante
        -activa
        +actualizar()
        +estaActiva()
        +expirar()
    }

    class ControladorTactil {
        -presionado
        -cantidadPuntosArrastre
        +onTouchDown()
        +onTouchMove()
        +onTouchUp()
    }

    class HUDController {
        +setPuntaje()
        +setBarraMRS()
        +setTiempoRestante()
        +mostrarPantallaVictoria()
        +adaptarUI()
    }

    GameManager "1" --> "1" SpawnerEmbarcaciones : coordina
    GameManager "1" --> "0..*" Embarcacion : administra
    GameManager "1" --> "0..*" AreaMarinaProtegida : gestiona
    GameManager "1" --> "1" HUDController : actualiza
    ControladorTactil "1" --> "1" GameManager : notifica gestos
    SpawnerEmbarcaciones "1" --> "1..*" Ruta : asigna
    Embarcacion "1" --> "1" Ruta : recorre
