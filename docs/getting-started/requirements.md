# Requisitos

## Requisitos mínimos

| Componente | Requisito |
|------------|-----------|
| **Garry's Mod** | Cualquier versión reciente (Steam) |
| **DarkRP** | Obligatorio (versión 2.7.0 o superior) |
| **SQLite** | Integrado en Garry's Mod |
| **Sistema operativo** | Windows Server, Linux (Ubuntu/Debian/CentOS) |

## Dependencias

### Obligatorias

| Dependencia | Versión | Propósito |
|-------------|---------|-----------|
| **DarkRP** | ≥ 2.7.0 | Hooks de arresto, salary, wallet, shop, healing, job change |

### Opcionales

| Dependencia | Propósito |
|-------------|-----------|
| **SAM** | Sistema de permisos alternativo |
| **ULX + ULib** | Comandos de administración avanzados (`!givexp`, `!setlevel`, etc.) |
| **CAM** | Common Admin Manager (soporte de permisos) |

!!! tip "Recomendación"
    Recomendamos instalar **ULX + ULib** para acceder a los 11 comandos administrativos predefinidos.

## Estructura del servidor recomendada

```
garrysmod/
├── addons/
│   ├── skillforge/          ← Skillforge
│   ├── darkrpmodification/  ← DarkRP
│   ├── sam/                 ← (opcional)
│   └── ulx/                 ← (opcional)
```

## Puertos y red

- No se requieren puertos adicionales
- El addon usa el sistema de red interno de Garry's Mod
- Si usas rate limiting estricto, puede afectar el re-sync de árboles grandes

## Almacenamiento

| Tipo | Tamaño estimado |
|------|----------------|
| Árboles JSON | ~5-10 KB cada uno |
| Base de datos SQLite | ~1-5 KB por jugador activo |
| Logs | ~1-5 MB (dependiendo de actividad) |

## Siguientes pasos

- [Instalación](installation.md) — Guía paso a paso
- [Quickstart](quickstart.md) — Primeros pasos rápidos
