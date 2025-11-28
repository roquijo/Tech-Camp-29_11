# 🚀 Tech-Camp  
## **Construcción de Aplicaciones Fullstack con Spring Boot, Angular y JWT**

---

### 🧭 Descripción del Curso

Este **Tech-Camp** es una experiencia práctica intensiva de **5 horas** para construir una **aplicación web completa** de punta a punta, utilizando **Spring Boot (Backend)**, **Angular (Frontend)** y **JWT** para autenticación.  

El enfoque será **100% práctico**: construirás una aplicación funcional desde cero, con backend protegido y frontend integrado.

---

## ⏱️ Distribución del Tiempo (5 horas totales)

- **30 minutos**: Instalación y verificación del entorno
- **2 horas**: Backend con Spring Boot + JWT + PostgreSQL
- **30 minutos**: Descanso ☕
- **1.5 horas**: Frontend con Angular + Integración
- **30 minutos**: Demo final y cierre

**Total efectivo: 4.5 horas de práctica**

---

## 🎯 Objetivo General

Desarrollar una aplicación web moderna y segura con **Spring Boot, Angular y JWT**, implementando autenticación desde cero sin servicios externos.

---

## 🧩 Estructura del Curso

### [🧱 Parte 1: Preparación del Entorno (30 min)](INSTALACION.md)

**🎯 Objetivo:**  
Verificar que el entorno de desarrollo esté listo para trabajar.

**Temas Clave:**
- Verificación rápida de:
  - **Java 21** y **Maven**
  - **Node.js** y **Angular CLI**
  - **PostgreSQL** (instalación local)
  
**Resultado esperado:**  
Entorno verificado y funcionando

---

### [⚙️ Parte 2: Backend con Spring Boot y JWT (2 horas)](BACKEND.md)

**🎯 Objetivo:**  
Construir un backend funcional con **Spring Boot**, API REST conectada a PostgreSQL y protegida con **JWT simple**.

**Temas Clave:**
- Creación del proyecto con Spring Initializr
- Estructura básica (controladores, servicios, repositorios)
- Conexión con **PostgreSQL local**
- **API REST básica** (CRUD simple - ejemplo: Productos)
- **JWT con Spring Security**:
  - Generación de tokens JWT
  - Endpoint de login
  - Protección de endpoints con filtros JWT
- Prueba rápida con Postman

**Resultado esperado:**  
Backend corriendo en `http://localhost:8080`, con endpoints protegidos por JWT

---

### [💻 Parte 3: Frontend con Angular (1.5 horas)](FRONTEND.md)

**🎯 Objetivo:**  
Construir una interfaz en **Angular** que consuma el backend y maneje autenticación con **JWT**.

**Temas Clave:**
- Creación del proyecto Angular
- Estructura básica (componentes, servicios)
- Consumo de **APIs REST** con `HttpClient`
- **Autenticación JWT**:
  - Servicio de autenticación
  - Login y almacenamiento de token
  - HTTP Interceptor para agregar token automáticamente
  - Guards para proteger rutas
- Componente de listado y formulario básico
- Configuración de **CORS** en el backend

**Resultado esperado:**  
Frontend funcionando en `http://localhost:4200`, conectado al backend con autenticación JWT

---

## 🧠 Tecnologías Clave

| Categoría | Herramientas |
|------------|---------------|
| Backend | Java 21, Spring Boot, Spring Security, JPA, PostgreSQL |
| Frontend | Angular, TypeScript |
| Seguridad | JWT (JJWT library) |
| Base de Datos | PostgreSQL (instalación local) |
| Herramientas | Maven, Node.js, Angular CLI |

---

## ✨ Autor y Créditos

**Instructor:** Jorge Eliecer Rojas  
**Nivel:** Introductorio - Intermedio  