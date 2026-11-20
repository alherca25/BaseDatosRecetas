<div align="center">

# BaseDatosRecetas

**Recetario en JSON para la app [Cocina Rápida](https://github.com/alherca25/CocinaArguinyano).**

![Recetas](https://img.shields.io/badge/recetas-95-C8553D)
![Categorías](https://img.shields.io/badge/categorías-11-3B2F25)
![Formato](https://img.shields.io/badge/formato-JSON-black?logo=json)

</div>

---

Este repositorio **solo contiene datos**: no tiene código. Las apps de [CocinaArguinyano](https://github.com/alherca25/CocinaArguinyano) leen y editan el archivo [`CocinaArguinyano.json`](CocinaArguinyano.json).

## Índice

- [Cómo se usa](#cómo-se-usa)
- [Formato de los datos](#formato-de-los-datos)
- [Categorías](#categorías)
- [Editar recetas](#editar-recetas)

## Cómo se usa

| App | Acceso | Cómo |
|---|---|---|
| **Recetario** (pública) | Lectura | Descarga el archivo desde `raw.githubusercontent.com` y guarda una copia en el móvil por si no hay conexión. |
| **Gestor de Recetas**, móvil | Escritura | Hace un commit en `main` con la API de GitHub cada vez que guardas. |
| **Gestor de Recetas**, escritorio | Escritura | Edita un clon local de este repositorio, que luego se sube con `git push`. |

URL de lectura:

```
https://raw.githubusercontent.com/alherca25/BaseDatosRecetas/main/CocinaArguinyano.json
```

> [!WARNING]
> Todo lo que se sube a `main` llega a los usuarios la próxima vez que abren la app. Guarda siempre un JSON válido.

## Formato de los datos

El archivo es un objeto. Cada clave es una categoría y su valor es una lista de recetas:

```json
{
  "Sopas": [
    {
      "nombre": "Salmorejo con guindillas fritas",
      "pagina": "185",
      "elaboracion": "Lava los tomates...\n\nAgrega la miga de pan...",
      "filtros": { "vegetariano": false, "gluten_free": false },
      "ingredientes": [
        { "nombre": "Tomate pera", "cantidad": "1000", "unidad": "g" },
        { "nombre": "Diente de ajo", "cantidad": "1", "unidad": "uds" }
      ]
    }
  ]
}
```

| Campo | Tipo | Descripción |
|---|---|---|
| `nombre` | texto | Nombre de la receta. No puede repetirse en todo el recetario. |
| `pagina` | texto | Página del libro. Las recetas importadas del Excel la guardan como `"185.0"`. |
| `elaboracion` | texto | Los pasos, separados por una línea en blanco (`\n\n`). |
| `filtros.vegetariano` | booleano | Si es `true`, la receta aparece con el filtro «Vegetariano». |
| `filtros.gluten_free` | booleano | Si es `true`, la receta aparece con el filtro «Sin gluten». |
| `ingredientes[].nombre` | texto | Nombre del ingrediente. La lista de la compra suma los ingredientes que tienen el mismo nombre. |
| `ingredientes[].cantidad` | texto | La cantidad, escrita como texto (por ejemplo `"1000"` o `"0.5"`). |
| `ingredientes[].unidad` | texto | `uds` (unidades), `g` (gramos), `mL` (mililitros) o `cuch` (cucharadas). |

## Categorías

| Categoría | Recetas |
|---|---:|
| Sopas | 3 |
| Cremas | 2 |
| Verduras | 4 |
| Legumbres | 9 |
| Huevos | 4 |
| Arroces | 12 |
| Pastas | 12 |
| Carnes | 14 |
| Pescados | 15 |
| Postres | 14 |
| Panes | 6 |
| **Total** | **95** |

Para crear una categoría nueva basta con añadir una clave al JSON. Las apps la muestran sin cambiar su código.

## Editar recetas

- **Recomendado:** usa el **Gestor de Recetas**. Valida los datos y nunca sobrescribe los cambios de otra persona.
- **A mano:** edita el JSON, comprueba que sigue siendo válido (por ejemplo con `python -m json.tool CocinaArguinyano.json`) y haz *push* a `main`.
- **¿Quieres proponer una receta?** Abre un [issue](../../issues) con el nombre, la página, los ingredientes y la elaboración.

Para escribir en el repositorio hace falta permiso de *push*. El Gestor móvil usa un token *fine-grained* con permiso `Contents: Read and write` limitado a este repositorio. El token se queda en el móvil y nunca se sube.
