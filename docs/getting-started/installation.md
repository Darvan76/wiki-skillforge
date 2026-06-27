# Instalación

Sigue estos pasos para instalar **Skillforge** en tu servidor de Garry's Mod.

---

## Requisitos previos

Antes de instalar, asegúrate de cumplir con los requisitos en la [página de requisitos](requirements.md).

---

## Método 1: GModStore (recomendado)

1. Compra el addon en [GModStore](https://www.gmodstore.com/market/skillforge)
2. Ve a tu panel de control del servidor
3. Abre la sección **Addons** o **Workshop**
4. Busca "Skillforge" o ingresa el Workshop ID
5. Actívalo y reinicia el servidor

---

## Método 2: Instalación manual

!!! note "Para servidores dedicados"
    Este método es para servidores que no usan auto-descarga de workshop.

1. Descarga el addon desde GModStore
2. Extrae el contenido en la carpeta de tu servidor:

```
garrysmod/
└── addons/
    └── skillforge/
        ├── addon.json
        ├── html/skillforge/     ← Interfaz HTML/DHTML
        ├── lua/
        │   ├── autorun/
        │   │   └── skillforge_loader.lua
        │   ├── skillforge/      ← Core del sistema
        │   │   ├── sh_config.lua
        │   │   ├── sh_effect_types.lua
        │   │   ├── sh_language.lua
        │   │   ├── sv_*.lua
        │   │   ├── cl_*.lua
        │   │   ├── shared/
        │   │   ├── server/
        │   │   ├── client/
        │   │   ├── integrations/
        │   │   └── default_trees/
        │   └── ulx/modules/sh/
        │       └── skillforge.lua
        └── materials/
            └── skilltree_nexus/icons/  ← 64 iconos PNG
```

3. Reinicia el servidor

---

## Verificar la instalación

Una vez instalado, abre Garry's Mod y únete a tu servidor. Luego:

### 1. Abre el menú de habilidades

Presiona **F6** (por defecto) o escribe `!skills` en el chat.

### 2. Verifica que el HUD aparece

Deberías ver el HUD de Skillforge en tu pantalla con nivel, XP y puntos de habilidad.

### 3. Cambia de trabajo

Al cambiar a un trabajo compatible (Police, Medic, etc.), tu árbol de habilidades debería cambiar automáticamente.

### 4. Consola de administración

Si eres administrador (`superadmin` o `admin`), ejecuta en la consola:

```
skilltree_admin
```

Esto abrirá el panel de administración HTML.

---

## Solución de problemas

| Síntoma | Causa probable | Solución |
|---------|---------------|----------|
| El menú no se abre | Falta dependencia DarkRP | Verifica que DarkRP esté instalado y cargado |
| No aparecen árboles | Los JSON no se desplegaron | Ejecuta `skilltree_reload_trees` |
| El HUD no se ve | `EnableHUD = false` en config | Cambia a `true` en `sh_config.lua` |
| Error "Unknown command" | Loader no se ejecutó | Verifica que `skillforge_loader.lua` esté en `autorun/` |

Si los problemas persisten, visita la página de [Troubleshooting](../troubleshooting.md).

---

## Siguientes pasos

- [Configuración básica](../configuration/index.md) — Aprende a personalizar el sistema
- [Quickstart](quickstart.md) — Crea tu primer árbol en 5 minutos
- [Árboles de habilidades](../skill-trees/index.md) — Entiende la estructura de los árboles
