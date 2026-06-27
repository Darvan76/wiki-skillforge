# Darvan's Skillforge

<p align="center">
  <strong>Sistema avanzado de Skill Trees para DarkRP</strong><br>
  28 efectos · 12 permisos · 5 integraciones · 7 árboles por defecto · 150+ puntos de personalización
</p>

<p align="center">
  <a href="getting-started/installation.md" class="md-button md-button--primary">⚡ Instalar ahora</a>
  <a href="configuration/index.md" class="md-button">⚙️ Configurar</a>
  <a href="developer/api-reference.md" class="md-button">📚 API Reference</a>
  <a href="faq.md" class="md-button">❓ FAQ</a>
</p>

---

## ¿Qué es Skillforge?

**Skillforge** es un sistema completo de árboles de habilidades para servidores de **Garry's Mod** con **DarkRP**. Permite que cada trabajo (Police, Medic, Criminal, Garbage, etc.) tenga su propio árbol de habilidades con ramas, nodos, niveles, experiencia (`XP`) y recompensas.

Cada jugador gana XP realizando acciones propias de su trabajo y gasta puntos de habilidad para desbloquear nodos dentro de su árbol. Los nodos otorgan efectos que van desde multiplicadores de velocidad hasta habilidades activas como escudos o curación instantánea.

---

## Características clave

<div class="grid cards" markdown>

-   :material-skilltree: **Árboles por trabajo**  
    Cada job de DarkRP puede tener su propio árbol único. Hasta 7 árboles incluidos por defecto.

-   :material-lightning-bolt: **28 tipos de efecto**  
    WalkSpeed, DamageMultiplier, PassiveRegen, ShopDiscount, SalaryBoost, LockpickSpeed y más.

-   :material-shield-account: **12 permisos granulares**  
    Compatible con SAM, ULX/ULib, CAM y fallback `IsAdmin()`.

-   :material-sword-cross: **5 integraciones DarkRP**  
    Police, Medic, Criminal, Economy, Garbage — todas con hooks automáticos.

-   :material-chart-timeline-variant: **3 modos de progresión**  
    Global (compartido), Separate (por trabajo), Hybrid (nivel global, XP por trabajo).

-   :material-currency-usd: **Sistema de prestigio**  
    10 niveles de prestigio con bonus de XP y reset de habilidades.

-   :material-shield-check: **Anti-exploit integrado**  
    Rate limiting, AFK detection, anti-farming por mismo objetivo, tope de XP por minuto.

-   :material-earth: **Multi-idioma**  
    Incluye EN, ES, FR. Sistema extensible para añadir más idiomas.

-   :material-application-edit: **Editor visual**  
    Interfaz HTML/DHTML para crear y modificar árboles sin tocar código.

-   :material-database: **Persistencia SQLite**  
    Datos de jugadores, progreso por trabajo, logs de administración y backups.

</div>

---

## Lo que dicen los números

| Métrica | Valor |
|---------|-------|
| Efectos diferentes | 28 pasivos + 5 activos |
| Árboles por defecto | 9 (incluyendo 7 por job + 1 RPG + 1 admin) |
| Comandos de consola | 20+ |
| Comandos ULX | 11 |
| Hooks personalizados | 11 |
| Canales de red | 17 |
| APIs públicas | 30+ |
| Variables configurables | ~150+ |
| Idiomas | 3 (EN, ES, FR) |

---

## Stack técnico

- **Motor**: Garry's Mod (GLua)
- **Interfaz**: HTML/DHTML + CSS/JS
- **Persistencia**: SQLite (bases de datos separadas por tabla)
- **Dependencias**: DarkRP (requerido), SAM/ULX (opcional)
- **Visualización**: Canvas/SVG para árboles, partículas para level-up

---

## ¿Listo para empezar?

Sigue la [guía de instalación](getting-started/installation.md) para instalar Skillforge en tu servidor, o explora la [documentación de configuración](configuration/index.md) para personalizar cada aspecto del sistema.

<p align="center">
  <a href="getting-started/installation.md" class="md-button md-button--primary">🚀 Comenzar</a>
  <a href="changelog.md" class="md-button">📋 Changelog</a>
  <a href="roadmap.md" class="md-button">🗺️ Roadmap</a>
</p>
