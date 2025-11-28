# 🌐 Parte 3: Frontend con Angular e Integración con el Backend

**⏱️ Tiempo estimado: 1.5 horas**

## 🎯 Objetivo
Construir una interfaz web moderna con Angular que consuma la API REST del backend, manejando autenticación con JWT y mostrando datos de forma dinámica.

---

## 1. Creación del Proyecto Angular (10 minutos)

### Verificar Angular CLI
```bash
ng version
```

### Crear proyecto
```bash
ng new frontend-app
# ¿Agregar routing? → Sí
# ¿Qué estilo? → CSS (o el que prefieras)
cd frontend-app
```

### Iniciar servidor de desarrollo
```bash
ng serve
```

Verifica en [http://localhost:4200](http://localhost:4200) que la aplicación esté corriendo.

---

## 2. Estructura del Proyecto (5 minutos)

Explicación rápida de la estructura:
- **`src/app/`** → Código de la aplicación
- **`src/app/components/`** → Componentes (secciones visuales)
- **`src/app/services/`** → Servicios (comunicación con backend)
- **`src/app/models/`** → Modelos/Interfaces TypeScript
- **`src/app/guards/`** → Guards para proteger rutas
- **`src/app/interceptors/`** → Interceptores HTTP

---

## 3. Configuración Básica (10 minutos)

### 3.1. Instalar dependencias necesarias
```bash
npm install
```

### 3.2. Configurar HttpClient
En `app.config.ts` (o `app.module.ts` si usas módulos), asegúrate de tener:
- `provideHttpClient()` (o `HttpClientModule` en módulos)

### 3.3. Crear modelo Producto
Crea `src/app/models/producto.model.ts`:
- Interface con: `id`, `nombre`, `precio`, `descripcion`

---

## 4. Servicio de Autenticación (20 minutos)

### 4.1. Crear AuthService
Crea `src/app/services/auth.service.ts`:
- Método `login(username: string, password: string)`
- Hace POST a `http://localhost:8080/api/auth/login`
- Guarda el token en `localStorage`
- Método `getToken()` para obtener el token
- Método `isAuthenticated()` para verificar si hay token
- Método `logout()` para limpiar el token

### 4.2. Crear componente Login
```bash
ng generate component components/login
```

En `login.component.ts`:
- Formulario con `username` y `password`
- Método `onSubmit()` que llama a `authService.login()`
- Redirige a la página principal si el login es exitoso
- Muestra error si falla

---

## 5. HTTP Interceptor para JWT (15 minutos)

### 5.1. Crear JWT Interceptor
Crea `src/app/interceptors/jwt.interceptor.ts`:
- Intercepta todas las peticiones HTTP
- Obtiene el token del `localStorage`
- Agrega el header `Authorization: Bearer <token>` a cada petición
- Si no hay token, deja pasar la petición (para login)

### 5.2. Registrar el Interceptor
En `app.config.ts` (o `app.module.ts`):
- Registra el interceptor usando `provideHttpClientInterceptors()`

---

## 6. Servicio de Productos (15 minutos)

Crea `src/app/services/producto.service.ts`:
- Método `getAll()` → GET `http://localhost:8080/api/productos`
- Método `getById(id: number)` → GET `http://localhost:8080/api/productos/{id}`
- Método `create(producto: Producto)` → POST `http://localhost:8080/api/productos`
- Método `delete(id: number)` → DELETE `http://localhost:8080/api/productos/{id}`

**Importante:** Usa `HttpClient` y el interceptor agregará automáticamente el token.

---

## 7. Componente de Listado de Productos (20 minutos)

### 7.1. Crear componente
```bash
ng generate component components/producto-list
```

### 7.2. Implementar listado
En `producto-list.component.ts`:
- Inyecta `ProductoService`
- En `ngOnInit()`, llama a `productoService.getAll()`
- Guarda los productos en una variable `productos: Producto[]`

En `producto-list.component.html`:
- Usa `*ngFor` para mostrar la lista de productos
- Muestra: nombre, precio, descripción
- Botón para eliminar cada producto

---

## 8. Componente de Formulario (15 minutos)

### 8.1. Crear componente
```bash
ng generate component components/producto-form
```

### 8.2. Implementar formulario
En `producto-form.component.ts`:
- Usa `FormBuilder` o `FormGroup` para crear el formulario
- Campos: `nombre`, `precio`, `descripcion`
- Método `onSubmit()` que llama a `productoService.create()`
- Después de crear, redirige al listado o recarga la lista

En `producto-form.component.html`:
- Formulario reactivo con los campos
- Botón de envío

---

## 9. Protección de Rutas con Guards (10 minutos)

### 9.1. Crear AuthGuard
Crea `src/app/guards/auth.guard.ts`:
- Implementa `CanActivate`
- Verifica si el usuario está autenticado usando `authService.isAuthenticated()`
- Si no está autenticado, redirige a `/login`
- Si está autenticado, permite el acceso

### 9.2. Configurar rutas
En `app.routes.ts` (o donde tengas las rutas):
- Ruta `/login` → componente Login (pública)
- Ruta `/productos` → componente ProductoList (protegida con `canActivate: [AuthGuard]`)
- Ruta `/productos/nuevo` → componente ProductoForm (protegida con `canActivate: [AuthGuard]`)

---

## 10. Navegación y Layout (10 minutos)

### 10.1. Crear componente Navbar
```bash
ng generate component components/navbar
```

En `navbar.component.html`:
- Link a "Productos"
- Link a "Nuevo Producto"
- Botón "Cerrar Sesión" que llama a `authService.logout()`
- Muestra el nombre de usuario si está autenticado

### 10.2. Añadir navbar al layout
En `app.component.html`:
- Incluye el componente navbar
- `<router-outlet>` para las rutas

---

## 11. Manejo de Errores (5 minutos)

En los servicios:
- Captura errores HTTP
- Si es 401 (Unauthorized), redirige a login
- Muestra mensajes de error al usuario

---

## 12. Pruebas Finales (10 minutos)

Verifica:
- [ ] Login funciona y guarda el token
- [ ] Al hacer login, redirige a la lista de productos
- [ ] La lista de productos carga correctamente
- [ ] El formulario crea productos correctamente
- [ ] El botón eliminar funciona
- [ ] Si no hay token, redirige a login
- [ ] El botón "Cerrar Sesión" limpia el token y redirige a login
- [ ] CORS funciona correctamente (sin errores en consola)

---

## 13. Errores Comunes

- **CORS error:** Verifica que el backend tenga CORS habilitado para `http://localhost:4200`
- **401 Unauthorized:** Verifica que el token se esté enviando en el header
- **Token no se guarda:** Verifica que uses `localStorage.setItem()` correctamente
- **Interceptor no funciona:** Verifica que esté registrado en `app.config.ts`

---

## ✅ Resultado Esperado
Una aplicación Angular funcional en `http://localhost:4200`, conectada al backend, con autenticación JWT, capaz de listar y crear productos de forma segura.