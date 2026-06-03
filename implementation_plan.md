# Plan de Implementación: Transición de Video Programática con Remotion

Este plan detalla el proceso para inicializar un nuevo proyecto de **Remotion** en React/TypeScript, importar los dos videos de origen desde la carpeta de descargas, y construir una composición con la transición **Lens Block** (bloqueo de lente con producto) descrita en la guía de grabación de Truss.

---

## 🎯 Objetivo
Hacer una transición limpia entre:
1. **Video 1 (Origen)**: `20260601_131224.mp4` (localizado en `Downloads`).
2. **Video 2 (Destino)**: `IMG_7225.MOV` (localizado en `Downloads`).

La transición emulará el movimiento **Lens Block** (donde el producto bloquea completamente la lente de la cámara al final del primer clip y se retira al inicio del segundo clip para revelar el "Después").

---

## 🏗️ Propuesta de Arquitectura

Crearemos un nuevo proyecto de Remotion en una carpeta dedicada dentro del scratch del usuario:
`C:\Users\franc\.gemini\antigravity\scratch\truss-video-transition`

El proyecto tendrá la siguiente estructura modular:
```
truss-video-transition/
├── public/
│   ├── video1.mp4              # Copia de 20260601_131224.mp4
│   └── video2.mov              # Copia de IMG_7225.MOV
├── src/
│   ├── transitions/
│   │   └── LensBlockTransition.tsx  # Componente principal de la transición
│   ├── Root.tsx                # Registro de composiciones
│   └── index.ts
├── package.json
└── remotion.config.ts
```

### Funcionamiento de la Transición (Lens Block)
El componente `LensBlockTransition.tsx` utilizará el componente `<Video>` de Remotion para secuenciar ambos clips con parámetros de tiempo ajustables para sintonizar el corte exacto:
* **Video 1 (Salida)**: Se reproducirá desde el inicio hasta el fotograma de bloqueo (donde el envase de Truss cubre la lente).
* **Video 2 (Entrada)**: Empezará a reproducirse desde el fotograma exacto donde el envase cubre la lente y comienza a alejarse.

Para facilitar la edición fina sin adivinar los tiempos, expondremos estas variables como **remotion schema properties** para que puedas cambiarlas visualmente con barras deslizadoras en el panel de control de Remotion Studio.

---

## 🚀 Cambios Propuestos

### 1. Inicialización del Proyecto
Crearemos la carpeta del proyecto y correremos la inicialización no interactiva usando:
```powershell
npx create-video --yes --blank C:\Users\franc\.gemini\antigravity\scratch\truss-video-transition
```

### 2. Copia de Recursos (Assets)
Copiaremos los dos videos de la carpeta `Downloads` a la carpeta `public/` del proyecto de Remotion:
* `C:\Users\franc\Downloads\20260601_131224.mp4` ➡️ `public/video1.mp4`
* `C:\Users\franc\Downloads\IMG_7225.MOV` ➡️ `public/video2.mov`

### 3. Implementación del Código React
Escribiremos el componente `LensBlockTransition.tsx` que:
* Mide los tiempos de corte en segundos/fotogramas.
* Realiza la transición de manera limpia en el fotograma exacto.
* Proporciona un visor para que puedas encontrar fácilmente los puntos de corte en el estudio visual.

---

## 🧪 Plan de Verificación

### Verificación Visual (Remotion Studio)
1. Iniciaremos el servidor de desarrollo de Remotion:
   ```bash
   npm run dev
   ```
2. Te proporcionaremos el enlace local (`http://localhost:3000`) para que abras el **Remotion Studio** en tu navegador.
3. Desde la interfaz web podrás ver el video, pausarlo, moverte cuadro por cuadro, y ajustar los tiempos del deslizamiento con total precisión.

### Renderizado de Producción
1. Una vez que encuentres los tiempos exactos, correremos el comando de renderizado:
   ```bash
   npx remotion render LensBlockTransition output.mp4
   ```
2. Abriremos el video final de inmediato en tu pantalla usando `Start-Process` para que valides el resultado.

---

> [!NOTE]
> Para trabajar de la manera más cómoda, una vez aprobado este plan, te recomendaremos establecer `C:\Users\franc\.gemini\antigravity\scratch\truss-video-transition` como tu espacio de trabajo activo.
