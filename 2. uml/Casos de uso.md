# 3. Diseño UML (`/2-uml`)

**Proyecto:** EcoPatrulla-Marino 
**Equipo:** Matheo Jaramillo Cardenas - Victor Manuel Magaña Perez  
**Versión:** 1.0  
**Fecha:** Noviembre 2026  

---

## 3.1 Diagrama de casos de uso

### Actores
- **Jugador:** Usuario final que interactúa en dispositivos Android mediante gestos táctiles (`tap` para sancionar embarcaciones ilegales y `drag` para delimitar Áreas Marinas Protegidas).
- **Motor / Temporizador de nivel:** Gestiona el ciclo de vida de la partida, el tiempo restante del nivel, la generación periódica de embarcaciones y la evaluación del estado del ecosistema.

### Casos de uso
- **CU-01: Sancionar y eliminar barco ilegal (`RF-01`)** — Detecta el toque sobre una embarcación ilegal (resaltada en rojo), la elimina de la escena e incrementa el marcador de puntos.
- **CU-02: Trazar Área Marina Protegida - AMP (`RF-02`)** — Permite mantener presionado y arrastrar sobre el mapa marítimo para activar una zona protegida de duración temporal.
- **CU-03: Actualizar ecosistema y evaluar victoria MRS (`RF-03`, `RF-05`)** — Incrementa o decrementa la barra de salud del ecosistema según AMP activas y barcos ilegales sin sancionar; declara la victoria al llegar al 100% con tiempo restante mayor a 0 segundos.
- **CU-04: Generar y desplazar embarcaciones (`RF-04`)** — Crea barcos legales e ilegales periódicamente en los bordes del mapa y los desplaza por rutas predefinidas.

```mermaid
flowchart LR
    subgraph Sistema["Tap Tap Marisco (Android 2D)"]
        UC1(["CU-01: Sancionar y eliminar barco ilegal (RF-01)"])
        UC2(["CU-02: Trazar Área Marina Protegida - AMP (RF-02)"])
        UC3(["CU-03: Actualizar ecosistema y evaluar victoria MRS (RF-03, RF-05)"])
        UC4(["CU-04: Generar y desplazar embarcaciones (RF-04)"])
    end

    Jugador(["Jugador"])
    Motor(["Motor / Temporizador de nivel"])

    Jugador --> UC1
    Jugador --> UC2
    UC1 -.->|"<<include>>"| UC3
    UC2 -.->|"<<include>>"| UC3
    Motor --> UC3
    Motor --> UC4
