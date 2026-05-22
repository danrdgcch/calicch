# 📚 Dashboard de Calificaciones CCH

Consulta de calificaciones por número de cuenta para alumnos del CCH.
Hospedado en GitHub Pages · Los datos vienen de archivos Excel por grupo.

---

## ✏️ Cambio de grupos — lo único que hay que tocar

### Línea 389 de `index.html`

```js
const GRUPOS = [
  '0276',
  '0284',
  '0227',
  '0458',
  '0470',
  '0480'
];
```

- Para **agregar** un grupo: agrega el número entre comillas y coma, dentro de los corchetes.
- Para **quitar** un grupo: borra esa línea.
- El nombre debe coincidir **exactamente** con el nombre del archivo `.xlsx` en GitHub (sin extensión).

**Ejemplo** — agregar el grupo 0999 y quitar 0227:

```js
const GRUPOS = [
  '0276',
  '0284',
  '0458',
  '0470',
  '0480',
  '0999'   // ← nuevo
];
```

Después de editar, sube el `index.html` a GitHub y listo. No hay que tocar nada más.

---

## 📁 Archivos Excel por grupo

Cada grupo necesita su propio archivo `.xlsx` con el nombre exacto del grupo, en la raíz del repositorio:

```
0276.xlsx
0284.xlsx
0227.xlsx
...
```

---

## 📋 Nombres de columnas en el Excel

El programa lee columnas con dos métodos:

- **Columnas fijas** — el nombre debe ser exactamente igual (mayúsculas/minúsculas importan).
- **Columnas flexibles** — el programa las detecta automáticamente por palabras clave; admiten variaciones.

---

### Columnas fijas (nombre exacto)

| Columna en Excel | ¿Para qué sirve? | Notas |
|---|---|---|
| `No.` | Número de cuenta del alumno | Con punto al final. Puede tener espacio: `No. ` |
| `NOMBRE` | Apellidos y nombre completo | Se muestra en el encabezado del card |
| `NOMBRE DE PILA` | Solo el primer nombre | Para el saludo personalizado ("Hola, Ana") |
| `Final DGAE` | Calificación oficial entera | La que va al sistema. Puede estar vacía durante el semestre |
| `Final provisional` | Calificación calculada con decimales | Se muestra mientras no haya Final DGAE |
| `Asistencia` | Porcentaje de asistencia (decimal) | Ej: `0.87` para 87%. Se muestra en el hero con color |
| `Total de firmas` | Número total de firmas del alumno | Se muestra grande en la sección Firmas |
| `Khan Academy` | Calificación de Khan Academy | Dentro de la sección de Tareas |
| `Promedio tareas` | Promedio de tareas | Dentro de la sección de Tareas |

---

### Columnas flexibles (detección automática por palabras clave)

Estas columnas pueden tener nombres distintos entre grupos; el programa las busca por patrón.

#### Exámenes
El programa detecta **todas** las columnas que sigan este formato:

```
Examen 1     Examen U1     Examen u2     Examen 3
```

> Patrón: empieza con `Examen`, seguido opcionalmente de `U` o `u`, luego un número.  
> Admite texto adicional después del número: `Examen U1 Algebra` también funciona.

---

#### Proyectos
El programa detecta todas las columnas con este formato:

```
Proyecto 1     Proyecto 2     Proyecto 3
```

> También detecta nombres especiales heredados: `Linea del tiempo`, `Papiroflexia`

---

#### Porcentaje de exámenes
Columna con el puntaje total de exámenes (máximo 5 pts):

```
Porcentaje 50     Porcentaje50     porcentaje 50%
```

> Debe contener la palabra `porcentaje` y el número `50`.

---

#### Porcentaje de firmas
Columna con el puntaje obtenido en el rubro de firmas. El número del porcentaje define el máximo:

```
Porcentaje firmas 20%    →  máximo 2.0 pts
Porcentaje Firmas 15%    →  máximo 1.5 pts
Porcentaje de Firmas 20% →  máximo 2.0 pts
```

> Debe contener `porcentaje` y `firmas` (en cualquier orden).

---

#### Porcentaje de tareas
Columna con el puntaje del rubro de tareas/trabajo de clase:

```
Porcentaje tareas 15%    →  máximo 1.5 pts
Porcentaje Tareas 20%    →  máximo 2.0 pts
```

> Debe contener `porcentaje` y `tareas`.

---

#### Porcentaje de proyectos
Columna con el puntaje del rubro de proyectos:

```
Porcentaje proyectos 20%    →  máximo 2.0 pts
Porcentaje Proyectos 15%    →  máximo 1.5 pts
```

> Debe contener `porcentaje` y `proyectos`.

---

#### Puntos extra
Columna para puntos extra opcionales:

```
Extra     extra     EXTRA     Extra puntos
```

> Debe **empezar** con la palabra `extra` (sin importar mayúsculas).

---

## 🎨 Colores de asistencia

El porcentaje de asistencia aparece en el hero del alumno con estos colores:

| Rango | Color | Significado |
|---|---|---|
| 90% – 100% | 🟢 Verde | Excelente asistencia |
| 80% – 89% | 🟡 Amarillo | Asistencia regular |
| Menos de 80% | 🔴 Rojo | Asistencia baja |

---

## 🔢 Escala de colores en badges

Los puntajes de cada rubro (exámenes, firmas, tareas, proyectos) se colorean así:

| Puntaje vs máximo | Color |
|---|---|
| 80% o más del máximo | 🟢 Verde |
| 50% – 79% del máximo | 🟡 Amarillo |
| Menos del 50% | 🔴 Rojo |

---

## ✅ Checklist para agregar un grupo nuevo

1. [ ] Editar línea 389 de `index.html` — agregar el número del grupo a `GRUPOS`
2. [ ] Crear el archivo Excel con el nombre exacto del grupo (`0999.xlsx`)
3. [ ] Verificar que las columnas fijas tengan los nombres correctos (ver tabla arriba)
4. [ ] Agregar las columnas de porcentaje con el formato `Porcentaje [rubro] [número]%`
5. [ ] Subir ambos archivos (`index.html` y `0999.xlsx`) al repositorio en GitHub
6. [ ] Esperar ~1 minuto y verificar en `danrdgcch.github.io/0276`

---

## 🌐 URL del sitio

```
https://danrdgcch.github.io/0276
```
