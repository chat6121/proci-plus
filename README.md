# PORCIPLUS 🐷 - Sistema de Control de Mortalidad de Cerdas & RBAC

Sistema profesional para el registro operativo, análisis epidemiológico, auditoría de bajas y control sanitario de cerdas reproductoras en granjas porcinas, con sincronización nativa en tiempo real con **Google Sheets**.

---

## 🌟 Características Principales

- **Base de Datos en Google Sheets**: Todos los registros operativos, bajas zootécnicas, usuarios y permisos se guardan y sincronizan automáticamente en tu hoja de cálculo en Google Drive.
- **Seguridad y Control de Accesos (RBAC)**:
  - Roles: `Administrador`, `Médico Veterinario` y `Operador`.
  - Matriz granular de permisos (ver dashboard, ver cuadrícula, editar tabla, ver analítica, ver alertas).
  - Bloqueo de cuentas temporal (con contador regresivo) o permanente.
- **Cuadrícula Tipo Excel Interactiva**:
  - Edición en celda con navegación por teclado (`Enter`, `Tab`, flechas direccionales).
  - Inserción masiva de filas vacías y limpieza automática de registros en blanco.
  - Duplicación rápida de filas.
  - **Botón Importar**: Carga masiva de datos desde archivos `.csv`, `.txt` o `.json` con detección automática de delimitadores (`;`, `,`, tabulaciones) y normalización de fechas.
  - **Botón Exportar**: Descarga directa en formato CSV compatible con Microsoft Excel (codificación UTF-8 con BOM `\uFEFF` y delimitador `;`), preservando tildes y caracteres especiales.
- **Analítica y Reportes Gráficos**:
  - Distribución de mortalidad por estatus reproductivo (`GESTANTE`, `LACTANTE`, `DESTETADA`, `LECHONA`, `DESCARTE`).
  - Tendencias semanales (semana zootécnica ISO-8601) y por día de la semana.
  - Descarga de reportes gráficos en **PNG de alta resolución**.
- **Centro de Alertas Sanitarias**:
  - Detección de patrones críticos veterinarios (síndrome cardiorrespiratorio, pericarditis, prolapsos, torsiones mesentéricas, sospecha de micotoxinas/zearalenona).
  - Protocolos de acción técnica recomendados.

---

## 📁 Estructura del Repositorio

```text
├── Index.html          # Aplicación web completa (React 19 + Tailwind CSS) lista para navegador o Apps Script
├── Code.gs             # Código fuente de Google Apps Script para ejecutar el backend en Google Sheets
├── appsscript.json     # Manifiesto de configuración de Google Apps Script (zona horaria y permisos)
├── .gitignore          # Exclusiones estándar para git (archivos temporales y backups)
└── README.md           # Documentación completa y guía de despliegue paso a paso
```

---

## 🚀 Despliegue con Google Sheets (Paso a Paso)

Para que todos los datos se sincronicen y guarden en tu Google Drive:

### 1. Crear la Hoja de Cálculo
1. Entra a [Google Sheets](https://sheets.new) y crea una nueva hoja de cálculo en blanco.
2. Nómbrala, por ejemplo: `PORCIPLUS - Base de Datos`.

### 2. Configurar el Editor de Apps Script
1. En la hoja de cálculo, ve al menú superior: **Extensiones** > **Apps Script**.
2. Verás un archivo llamado `Código.gs` (o `Code.gs`). Borra su contenido y pega todo el código del archivo [`Code.gs`](./Code.gs) de este repositorio.
3. Haz clic en el botón **+ (Añadir un archivo)** > selecciona **HTML**.
4. Nómbralo exactamente `Index` (sin escribir `.html`, el editor lo añade automáticamente).
5. Abre el archivo [`Index.html`](./Index.html) de este repositorio, copia todo su contenido y pégalo dentro del archivo `Index` en Apps Script.
6. Guarda los cambios haciendo clic en el ícono de disco 💾 o con `Ctrl + S`.

### 3. Inicializar la Estructura de la Hoja
1. Vuelve a la pestaña de tu Hoja de Cálculo y recárgala (`F5`).
2. En el menú superior aparecerá un nuevo menú llamado **🐷 PORCIPLUS**:
   - Haz clic en **Inicializar Estructura de Hojas** (autoriza los permisos si Google lo solicita).
   - Haz clic en **Crear Usuario Admin por Defecto**.
3. Se generarán automáticamente dos pestañas:
   - **`Mortalidad`**: Con 14 columnas (`ID`, `FECHA`, `ID_ANIMAL`, `REGISTRADO_POR`, `ROL`, `USUARIO`, `GENETICA`, `ESTATUS`, `CAUSA`, `LUGAR`, `PARIDAD`, `SEMANA`, `DIA`, `OBSERVACIONES`).
   - **`Usuarios`**: Con las cuentas, contraseñas y permisos RBAC.

### 4. Publicar como Aplicación Web
1. En el editor de Apps Script, haz clic en el botón azul superior **Implementar** > **Nueva implementación**.
2. En el engranaje ⚙️ (Seleccionar tipo), elige **Aplicación web**.
3. Configuración:
   - **Descripción**: `PORCIPLUS v1.0`
   - **Ejecutar como**: `Yo (tu correo de Google)`
   - **Quién tiene acceso**: `Cualquiera` (o los usuarios de tu organización).
4. Haz clic en **Implementar**.
5. Copia la **URL de la aplicación web**. ¡Listo! Al abrir esa URL en cualquier navegador o celular tendrás el sistema funcionando y guardando todos los datos directamente en Google Sheets.

---

## 🔑 Credenciales Iniciales por Defecto

- **Usuario**: `admin`
- **Contraseña**: `admin`

*(Puedes cambiar la contraseña o crear nuevos usuarios desde el módulo **Gestión de Usuarios**).*

---

## ☁️ Conexión Alternativa desde Index.html Local

Si abres directamente el archivo `Index.html` en tu navegador de forma local:
1. Funciona de manera autónoma guardando en la memoria local (`localStorage`).
2. En la pestaña **Sincronización en la Nube**, puedes pegar el ID o URL de tu hoja de cálculo para vincularla y subir/descargar datos cuando lo desees.
3. Cuenta con los botones **📥 Importar** y **📤 Exportar** en la cuadrícula de datos para respaldos directos en Excel.

