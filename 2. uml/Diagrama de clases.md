classDiagram
    class GameManager {
        -int puntaje
        -int puntosPorSancion
        -float saludEcosistema
        -float tiempoRestante
        -bool partidaActiva
        +iniciarNivel(int nivelId) void
        +actualizar(float deltaTime) void
        +procesarToque(float x, float y) void
        +crearAMP() void
        +sumarPuntos(int puntos) void
        +actualizarSaludEcosistema(float delta) void
        +evaluarVictoriaMRS() bool
        +finalizarNivel(bool victoria) void
    }

    class SpawnerEmbarcaciones {
        -float intervaloAparicion
        -float temporizadorSpawn
        +actualizar(float deltaTime) void
        +generarBarco(bool esIlegal) Embarcacion
    }

    class Embarcacion {
        -string id
        -bool esIlegal
        -float posX
        -float posY
        -float velocidad
        +desplazar(float deltaTime) void
        +colisionaConPunto(float x, float y) bool
        +eliminar() void
    }

    class Ruta {
        -int totalPuntos
        +obtenerSiguientePunto(int indice) void
    }

    class AreaMarinaProtegida {
        -string id
        -int cantidadPuntosTrazo
        -float duracionRestante
        -bool activa
        +actualizar(float deltaTime) void
        +estaActiva() bool
        +expirar() void
    }

    class ControladorTactil {
        -bool presionado
        -int cantidadPuntosArrastre
        +onTouchDown(float x, float y) void
        +onTouchMove(float x, float y) void
        +onTouchUp(float x, float y) void
    }

    class HUDController {
        +setPuntaje(int valor) void
        +setBarraMRS(float porcentaje) void
        +setTiempoRestante(float segundos) void
        +mostrarPantallaVictoria() void
        +adaptarUI(float aspectRatio) void
    }

    GameManager "1" --> "1" SpawnerEmbarcaciones : coordina
    GameManager "1" --> "0..*" Embarcacion : administra
    GameManager "1" --> "0..*" AreaMarinaProtegida : gestiona
    GameManager "1" --> "1" HUDController : actualiza
    ControladorTactil "1" --> "1" GameManager : notifica gestos
    SpawnerEmbarcaciones "1" --> "1..*" Ruta : asigna
    Embarcacion "1" --> "1" Ruta : recorre
