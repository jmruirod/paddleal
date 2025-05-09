# PaddleAl 🏓

## Descripción del Proyecto

Este proyecto es una aplicación web demo desarrollada con Vue.js que simula una tienda de palas de padel con un carrito de compras funcional. La aplicación permite a los usuarios explorar productos y añadirlos al carrito.

## ✨ Características Principales

- **Catálogo de Productos** 🛒: Navega por una selección cuidada de palas de pádel profesionales con información detallada
- **Carrito de Compras** 🛍️: Añade productos al carrito, ajusta cantidades y elimina artículos
- **Diseño Responsive** 📱: Diseño completamente adaptable que funciona tanto en escritorio como en dispositivos móviles
- **Almacenamiento Local** 💾: Los datos del carrito persisten entre sesiones

## 🔧 Tecnologías Utilizadas

- **Vue.js 3**: Con Composition API y TypeScript
- **TailwindCSS**: Para un diseño UI responsive y elegante
- **SweetAlert2**: Alertas y confirmaciones amigables para el usuario
- **Vite**: Herramientas de construcción rápidas y experiencia de desarrollo mejorada

## 🚀 Empezando

### Requisitos Previos

- Node.js (v16 o superior)
- pnpm

### Instalación

1. Clona el repositorio:

   ```bash
   git clone https://github.com/tuusuario/paddleal.git
   ```

2. Navega al directorio del proyecto:

   ```bash
   cd paddleal
   ```

3. Instala las dependencias:

   ```bash
   pnpm install
   ```

4. Inicia el servidor de desarrollo:

   ```bash
   pnpm dev
   ```

5. Abre tu navegador y visita `http://localhost:5173`

## 📁 Estructura del Proyecto

```
└── paddleal/
    ├── public/             # Activos estáticos
    │   └── img/            # Imágenes de productos e iconos
    ├── src/
    │   ├── components/     # Componentes Vue
    │   ├── data/           # Datos de productos simulados
    │   ├── model/          # Interfaces TypeScript
    │   ├── assets/         # Activos compilados
    │   ├── App.vue         # Componente principal de la aplicación
    │   └── main.ts         # Punto de entrada de la aplicación
    └── ...archivos de configuración
```

## 🏗️ Compilar para Producción

```bash
pnpm build
```

## 📄 Licencia

Este proyecto está disponible bajo la Licencia MIT. Consulta el archivo LICENSE para más información.

## 🙏 Agradecimientos

Este proyecto fue construido como parte del curso [Vue.js 3 - La Guía Completa](https://www.udemy.com/share/108Onc3@s0QRLqcVSwtbJ28vy0q3x4OgBYqn8OtqJ3tnD8YcMzwBtBWOqfnP7LTzefA5ZFvhnQ==/) de [Juan Pablo De la Torre Valdez](https://codigoconjuan.com/).
