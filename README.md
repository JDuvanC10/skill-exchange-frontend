# Skills Exchange — Frontend

Aplicación web frontend para la plataforma **Skills Exchange**, construida con **Next.js 14**, **React** y **Tailwind CSS**. Consume la API REST desplegada en producción con autenticación JWT.

> **API Base:** `https://apiskills.danidev.co/api/`  
> **Docs Swagger:** `https://apiskills.danidev.co/api/docs/`

---

## 🚀 Primeros pasos

### Requisitos

- Node.js 18 o superior
- npm

### Instalación y ejecución

```bash
# 1. Clona el repositorio 
git clone https://github.com/JDuvanC10/skill-exchange-frontend.git
cd skill-exchange-frontend

# 2. Instala las dependencias
npm install

# 3. Crea el archivo de variables de entorno
echo "NEXT_PUBLIC_API_BASE_URL=https://apiskills.danidev.co/api" > .env.local

# 4. Inicia el servidor de desarrollo
npm run dev
```

Abre [http://localhost:3000](http://localhost:3000) en tu navegador.

---

## 📄 Páginas implementadas

| Ruta | Descripción |
|------|-------------|
| `/` | Landing page — presentación de la plataforma |
| `/login` | Formulario de autenticación con JWT |
| `/dashboard` | Bienvenida con nombre y email del usuario |
| `/dashboard/skills` | Catálogo con filtros por categoría, búsqueda, ordenamiento y paginación |
| `/dashboard/skills/[id]` | Detalle completo de una skill |
| `/dashboard/users` | Directorio de usuarios con paginación |
| `/dashboard/goals` | Metas de aprendizaje con barra de progreso y botón "Alcanzar" |

---

## 📁 Estructura del proyecto

```
src/
├── app/
│   ├── (auth)/
│   │   └── login/page.jsx              # Formulario de login JWT
│   ├── (dashboard)/
│   │   └── dashboard/
│   │       ├── layout.jsx              # Navbar + protección de ruta
│   │       ├── page.jsx                # Bienvenida con datos del usuario
│   │       ├── skills/
│   │       │   ├── page.jsx            # Listado con filtros y paginación
│   │       │   └── [id]/page.jsx       # Detalle de skill
│   │       ├── users/page.jsx          # Listado de usuarios
│   │       └── goals/page.jsx          # Metas de aprendizaje
│   ├── page.jsx                        # Landing page (/)
│   └── globals.css
├── components/
│   ├── ui/
│   │   ├── Navbar.jsx                  # Barra de navegación principal
│   │   ├── HamburgerMenu.jsx           # Menú colapsable para mobile
│   │   ├── Pagination.jsx              # Paginación reutilizable
│   │   ├── LoadingState.jsx            # Indicador de carga
│   │   ├── ErrorMessage.jsx            # Mensaje de error de API
│   │   └── EmptyState.jsx              # Lista vacía
│   └── skills/
│       ├── SkillCard.jsx               # Tarjeta de habilidad
│       ├── CategoryFilter.jsx          # Filtros por categoría
│       └── OrderSelector.jsx           # Dropdown de ordenamiento
└── lib/
    └── api.js                          # Axios centralizado con interceptor JWT
```

---

## 🏗️ Decisiones de arquitectura

### API centralizada en `lib/api.js`
Toda la comunicación con el backend pasa por un único módulo configurado con Axios. Un interceptor de solicitudes agrega automáticamente el token JWT desde `localStorage` en cada petición, evitando repetir esa lógica en cada componente o página.

### Componente `Pagination` genérico desde el inicio
Se construyó como un componente reutilizable que recibe `count`, `page`, `pageSize` y `onPageChange`. Se usa sin modificaciones en las páginas de **Skills**, **Usuarios** y **Metas**, cumpliendo el requisito de reutilización en al menos tres vistas.

### Protección de rutas en `dashboard/layout.jsx`
El layout del dashboard verifica la presencia del token JWT en `localStorage` antes de renderizar cualquier página protegida. Si no existe token, redirige automáticamente a `/login`. Esto centraliza la lógica de autenticación en un solo lugar.

### Filtros y búsqueda como parámetros de URL
Los filtros de categoría, búsqueda (`search`) y ordenamiento (`ordering`) se traducen directamente en query params hacia el API (`?category=technical&ordering=name`). Esto permite que las URLs con filtros activos sean compartibles y recargables sin perder el estado.

### Componentes de estado de UI desacoplados
`LoadingState`, `ErrorMessage` y `EmptyState` son componentes independientes que se reutilizan en todas las páginas. Esto garantiza consistencia visual y evita duplicar el código de manejo de estados en cada vista.

---

## 🔗 Parámetros de filtrado disponibles

| Parámetro | Valores | Ejemplo |
|-----------|---------|---------|
| `category` | `technical`, `creative`, `communication`, `leadership`, `business`, `personal_development`, `other` | `?category=technical` |
| `level` | `beginner`, `intermediate`, `advanced`, `expert` | `?level=advanced` |
| `ordering` | `name`, `-name`, `created_at`, `-created_at` | `?ordering=-name` |
| `search` | texto libre | `?search=python` |
| `page` | número entero | `?page=2` |

---

## 📸 Capturas

- `capturas/postman/` — Evidencia de los endpoints explorados en Bruno/Postman
- `capturas/app/` — Capturas de cada página de la aplicación en desktop y mobile

---

## 🛠️ Tecnologías utilizadas

- [Next.js 14](https://nextjs.org/) — Framework React con App Router
- [React](https://react.dev/) — Biblioteca de UI
- [Tailwind CSS](https://tailwindcss.com/) — Estilos utilitarios
- [Axios](https://axios-http.com/) — Cliente HTTP con interceptores JWT

---

## 👤 Autor

**Duvan Carvajal** — [@JDuvanC10](https://github.com/JDuvanC10)  
Fork de [andresstbn/skill-exchange-frontend](https://github.com/andresstbn/skill-exchange-frontend)