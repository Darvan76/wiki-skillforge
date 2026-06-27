# Quickstart

Aprende a usar **Skillforge** en menos de 5 minutos.

---

## Para jugadores

### 1. Abre el menú

- Presiona **F6** (tecla por defecto)
- O escribe `!skills` en el chat

### 2. Explora el árbol

Verás un árbol con ramas y nodos. Cada nodo es una habilidad que puedes desbloquear.

- Los nodos **grises** están bloqueados
- Los nodos **azules** están disponibles para desbloquear
- Los nodos **morados** ya los tienes
- Los nodos **dorados** están al máximo nivel

### 3. Gana XP

Realiza acciones propias de tu trabajo:

- **Police**: Arresta criminales, confisca armas
- **Medic**: Cura y revive jugadores
- **Criminal**: Lockpickea puertas, roba impresoras
- **Garbage**: Recoge y recicla basura
- **Cualquiera**: Mata NPCs, juega tiempo, gana dinero

### 4. Desbloquea habilidades

Cuando tengas suficientes puntos de habilidad, haz clic en un nodo disponible y presiona **Unlock**.

---

## Para administradores

### Comandos básicos

```lua title="Consola del servidor"
skilltree_admin          -- Abre el panel de administración
skilltree_givexp "Player Name" 100  -- Da XP
skilltree_setlevel "Player Name" 10  -- Establece nivel
skilltree_resetskills "Player Name"  -- Reinicia habilidades
```

### ULX (si está instalado)

```
!givexp @me 500         -- Te da 500 XP
!setlevel @me 25        -- Te pone nivel 25
!resetskills @me        -- Reinicia tus habilidades
```

---

## Para desarrolladores

### Configurar XP por acción

```lua title="lua/autorun/my_xp_config.lua"
hook.Add("Initialize", "MyXP_Setup", function()
    SkillTree.Config.XP.PlayerKill.Amount = 100
    SkillTree.Config.XP.Arrest.Amount = 75
end)
```

### Añadir XP desde un addon externo

```lua
-- Cuando ocurre una acción personalizada
hook.Add("MyAddon_CustomAction", "GiveXP", function(ply)
    SkillTree.AddXP(ply, 50, "Acción personalizada")
end)
```

---

## Siguientes pasos

- [Configuración general](../configuration/general.md) — Ajusta comandos, teclas y más
- [Progression Modes](../job-system/progression-modes.md) — Elige cómo progresan los jugadores
- [Job-Tree Mapping](../job-system/job-tree-mapping.md) — Asigna árboles a trabajos
- [API Reference](../developer/api-reference.md) — Documentación completa para desarrolladores
