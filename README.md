# Skill Overlap Suite

Plugin para **Claude** (Cowork / Claude Code). Tres skills que te ayudan a entender y navegar los **solapamientos** entre las skills que tienes instaladas: cuándo usar cuál, en qué se diferencian y cómo combinarlas.

## Skills incluidas

| Skill | Qué hace | Cuándo se activa |
|---|---|---|
| **skill-overlap-resolver** | Te orienta **en el momento**: ante una tarea concreta donde varias skills aplican, te dice cuál usar, en qué orden o si combinarlas. No ejecuta la tarea, solo orienta. | "¿Qué skill uso para X?", "¿en qué se diferencian A y B?", o cuando Claude detecta que 2+ skills aplican. |
| **skill-overlap-comparator** | Produce un **documento de referencia** comparando dos o más skills en profundidad (alcance, límites, outputs, casos de uso). Para guardar y consultar después. | "Documenta la diferencia entre A y B", "crea una guía de comparación", "quiero una referencia para consultar luego". |
| **skill-overlap-mapper** | Construye un **mapa personalizado** de solapamientos filtrado por tu contexto real (tu trabajo, proyectos, sector), no genérico. | "Mapea mis skills para mi contexto", "qué solapamientos me importan dado lo que hago". |

Las tres son complementarias: usas *resolver* en el día a día, formalizas con *comparator* cuando un solapamiento se repite, y *mapper* te da el panorama completo antes de empezar un proyecto.

## Instalación

En Claude Code o Cowork:

```
/plugin marketplace add ricardo-mv/skill-overlap-suite
/plugin install skill-overlap-suite@ricardomv-skills
```

Para actualizar más adelante:

```
/plugin marketplace update
```

## Idioma

Las tres skills se adaptan al idioma del usuario (español o inglés).

## Licencia

MIT — ver [LICENSE](LICENSE).

---

*Autor: RicardoMV · Versión 1.0.0*
