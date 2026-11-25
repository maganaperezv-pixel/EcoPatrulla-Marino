# Diagrama de Secuencia — EcoPatrulla-Marino

**Proyecto:** EcoPatrulla-Marino  
**Equipo:** Matheo Jaramillo Cardenas - Victor Manuel Magaña Perez  
**Versión:** 1.0  
**Fecha:** Noviembre 2026  

## Escenario principal
Flujo de sanción y eliminación de un barco ilegal (`RF-01`), actualización dinámica de la barra de salud del ecosistema (`RF-05`) y evaluación de la condición de victoria al alcanzar el 100% de Máximo Rendimiento Sostenible con tiempo restante (`RF-03`).

```mermaid
sequenceDiagram
    autonumber
    actor Jugador
    participant Input as ControladorTactil
    participant GM as GameManager
    participant Barco as Embarcacion
    participant HUD as HUDController

    Jugador->>Input: onTouchDown(x, y)
    Input->>GM: procesarToque(x, y)
    GM->>Barco: colisionaConPunto(x, y)
    Barco-->>GM: true (esIlegal = true)

    GM->>Barco: eliminar()
    GM->>GM: sumarPuntos(puntosPorSancion)
    GM->>GM: actualizarSaludEcosistema(incrementoMRS)

    GM->>HUD: setPuntaje(puntaje)
    GM->>HUD: setBarraMRS(saludEcosistema)

    GM->>GM: evaluarVictoriaMRS()
    alt saludEcosistema >= 100 y tiempoRestante > 0
        GM->>GM: finalizarNivel(true)
        GM->>HUD: mostrarPantallaVictoria()
    else nivel en curso
        GM-->>Jugador: continúa partida
    end
```
