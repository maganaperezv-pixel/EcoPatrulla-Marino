### Archivo 2: `clases.md`

```markdown
# Diagrama de Clases — EcoPatrulla-Marino

**Proyecto:** EcoPatrulla-Marino  
**Equipo:** Matheo Jaramillo Cardenas - Victor Manuel Magaña Perez  
**Versión:** 1.0  
**Fecha:** Noviembre 2026  

```mermaid
classDiagram
    class GameManager {
        -int puntaje
        -float saludEcosistema
        -float tiempoRestante
        -bool partidaActiva
        +iniciarNivel(nivelId: int)
        +actualizar(deltaTime: float)
        +procesarToque(posicion: Vector2)
        +crearAMP(trazo: ListVector2)
        +sumarPuntos(puntos: int)
        +actualizarSaludEcosistema(delta: float)
        +evaluarVictoriaMRS() bool
        +finalizarNivel(victoria: bool)
    }

    class SpawnerEmbarcaciones {
        -float intervaloAparicion
        -float temporizadorSpawn
        -ListRuta rutas
        +actualizar(deltaTime: float)
        +generarBarco(esIlegal: bool) Embarcacion
    }

    class Embarcacion {
        -string id
        -bool esIlegal
        -Vector2 posicion
        -float velocidad
        -Ruta ruta
        +desplazar(deltaTime: float)
        +colisionaConPunto(punto: Vector2) bool
        +eliminar()
    }

    class Ruta {
        -ListVector2 puntos
        +obtenerSiguientePunto(indice: int) Vector2
    }

    class AreaMarinaProtegida {
        -string id
        -ListVector2 zona
        -float duracionRestante
        -bool activa
        +actualizar(deltaTime: float)
        +estaActiva() bool
        +expirar()
    }

    class ControladorTactil {
        -bool presionado
        -ListVector2 puntosArrastre
        +onTouchDown(pos: Vector2)
        +onTouchMove(pos: Vector2)
        +onTouchUp(pos: Vector2)
    }

    class HUDController {
        +setPuntaje(valor: int)
        +setBarraMRS(porcentaje: float)
        +setTiempoRestante(segundos: float)
        +mostrarPantallaVictoria()
        +adaptarUI(aspectRatio: float)
    }

    GameManager "1" --> "1" SpawnerEmbarcaciones : coordina
    GameManager "1" --> "0..*" Embarcacion : administra
    GameManager "1" --> "0..*" AreaMarinaProtegida : gestiona
    GameManager "1" --> "1" HUDController : actualiza
    ControladorTactil "1" --> "1" GameManager : notifica gestos
    SpawnerEmbarcaciones "1" --> "1..*" Ruta : asigna
    Embarcacion "1" --> "1" Ruta : recorre
