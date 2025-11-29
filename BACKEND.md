# ⚙️ Parte 2 — Backend con Spring Boot & JWT

**⏱️ Tiempo estimado: 2 horas**

**Objetivo:**  
Construir un backend funcional con Spring Boot, conectar a PostgreSQL, proteger los endpoints con JWT simple y documentar la API con Swagger.

---

## 1. Creación del Proyecto (10 minutos)

### Spring Initializr
Ve a [https://start.spring.io](https://start.spring.io) y configura:

**Project:** Maven  
**Language:** Java  
**Spring Boot:** La última estable 
**Packaging:** Jar  
**Java:** 25

**Dependencies a seleccionar:**
- ✅ Spring Web
- ✅ Spring Data JPA
- ✅ PostgreSQL Driver
- ✅ Spring Boot DevTools
- ✅ Lombok
- ✅ Spring Security

**Genera y descarga el proyecto.**

---

## 2. Dependencias Adicionales (5 minutos)

Abre `pom.xml` y añade estas dependencias después de las que ya vienen:

```xml
<!-- JWT -->
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-api</artifactId>
    <version>0.12.3</version>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-impl</artifactId>
    <version>0.12.3</version>
    <scope>runtime</scope>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-jackson</artifactId>
    <version>0.12.3</version>
    <scope>runtime</scope>
</dependency>

<!-- Swagger/OpenAPI -->
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.3.0</version>
</dependency>
```

---

## 3. Estructura del Proyecto (5 minutos)

Organiza el proyecto en paquetes por responsabilidades:

```
com.tuempresa.backend/
├── controller/     → endpoints REST
├── service/        → lógica de negocio
├── repository/     → interfaces JPA
├── model/          → entidades / DTOs
│   ├── entity/     → entidades JPA
│   └── dto/        → DTOs para requests/responses
├── config/         → configuraciones (CORS, seguridad, JWT)
│   ├── SecurityConfig.java
│   └── JwtConfig.java
└── resources/
    └── application.yml
```

---

## 4. Configuración `application.yml` (5 minutos)

Crea/edita `src/main/resources/application.yml`:

```yaml
server:
  port: 8080

spring:
  application:
    name: producto-api

  datasource:
    url: jdbc:postgresql://localhost:5432/productos_db
    username: postgres
    password: admin
    driver-class-name: org.postgresql.Driver

  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
    properties:
      hibernate:
        format_sql: true
        dialect: org.hibernate.dialect.PostgreSQLDialect
    database: postgresql

# JWT Configuration
jwt:
  secret: miClaveSecretaSuperSegura12345678901234567890
  expiration: 86400000  # 24 horas en milisegundos
```

**Importante:** Crea la base de datos `productos_db` en PostgreSQL antes de ejecutar.

---

## 5. Crear Base de Datos (5 minutos)

**Opción 1: Desde DBeaver**
1. Conéctate a PostgreSQL (localhost:5432, usuario: postgres, password: admin)
2. Crea una nueva base de datos llamada `productos_db`

**Opción 2: Desde línea de comandos**
```bash
psql -U postgres
CREATE DATABASE productos_db;
\q
```

---

## 6. Implementación Básica (60 minutos)

### 6.1. Entidad Producto (10 min)
- Crea `model/entity/Producto.java`
- Campos: `id`, `nombre`, `precio`, `descripcion`
- Anotaciones: `@Entity`, `@Table`, `@Id`, `@GeneratedValue`

### 6.2. Repository (5 min)
- Crea `repository/ProductoRepository.java`
- Extiende `JpaRepository<Producto, Long>`

### 6.3. Service (10 min)
- Crea `service/ProductoService.java`
- Métodos: `findAll()`, `findById()`, `save()`, `delete()`

### 6.4. Controller (10 min)
- Crea `controller/ProductoController.java`
- Endpoints: `GET /api/productos`, `GET /api/productos/{id}`, `POST /api/productos`, `DELETE /api/productos/{id}`
- Usa `@RestController`, `@RequestMapping("/api/productos")`

### 6.5. JWT - Configuración (15 min)
- Crea `config/JwtConfig.java` con:
  - Método para generar token
  - Método para validar token
  - Método para extraer username del token
- Usa la librería `jjwt`

### 6.6. JWT - Filtro de Seguridad (10 min)
- Crea `config/JwtAuthenticationFilter.java`
- Extiende `OncePerRequestFilter`
- Intercepta requests y valida el token JWT del header `Authorization: Bearer <token>`

### 6.7. SecurityConfig (10 min)
- Crea `config/SecurityConfig.java`
- Configura:
  - Endpoint `/api/auth/login` público (sin autenticación)
  - Endpoints `/api/productos/**` protegidos (requieren JWT)
  - Endpoints de Swagger públicos: `/swagger-ui/**`, `/v3/api-docs/**`
  - CORS habilitado para `http://localhost:4200`
  - Añade el filtro JWT a la cadena de seguridad

---

## 7. Endpoint de Login (10 minutos)

Crea `controller/AuthController.java`:
- Endpoint `POST /api/auth/login`
- Recibe `username` y `password` (por ahora hardcodeado, ej: admin/admin)
- Si las credenciales son correctas, genera un JWT y lo retorna
- Retorna: `{ "token": "..." }`

---

## 8. Pruebas con Postman (10 minutos)

### 8.1. Login
```
POST http://localhost:8080/api/auth/login
Content-Type: application/json

{
  "username": "admin",
  "password": "admin"
}
```

Copia el `token` de la respuesta.

### 8.2. Obtener Productos (protegido)
```
GET http://localhost:8080/api/productos
Authorization: Bearer <TU_TOKEN>
```

### 8.3. Crear Producto (protegido)
```
POST http://localhost:8080/api/productos
Authorization: Bearer <TU_TOKEN>
Content-Type: application/json

{
  "nombre": "Laptop",
  "precio": 999.99,
  "descripcion": "Laptop gaming"
}
```

---

## 9. Swagger (5 minutos)

Una vez que el proyecto esté corriendo, accede a:
- **Swagger UI:** http://localhost:8080/swagger-ui.html
- **OpenAPI JSON:** http://localhost:8080/v3/api-docs

Deberías ver todos tus endpoints documentados.

---

## 10. Errores Comunes y Soluciones

- **Error de conexión a PostgreSQL:** Verifica que el servicio esté corriendo y las credenciales en `application.yml`.
- **401 Unauthorized:** Verifica que el token JWT esté en el header `Authorization: Bearer <token>`.
- **CORS error:** Verifica que en `SecurityConfig` esté habilitado CORS para `http://localhost:4200`.
- **Swagger no carga:** Verifica que los endpoints `/swagger-ui/**` y `/v3/api-docs/**` estén públicos en `SecurityConfig`.

---

## 11. Checklist Final (5 minutos)

Antes de pasar al frontend, verifica:

- [ ] PostgreSQL corriendo y base de datos `productos_db` creada
- [ ] `application.yml` configurado correctamente
- [ ] Backend corriendo en `http://localhost:8080`
- [ ] Swagger accesible en `http://localhost:8080/swagger-ui.html`
- [ ] Login funciona y retorna token JWT
- [ ] Endpoints protegidos funcionan con token JWT
- [ ] CORS configurado para `http://localhost:4200`

---

## 12. Recursos Útiles

- [Spring Initializr](https://start.spring.io)
- [Spring Security Docs](https://spring.io/guides/tutorials/spring-security-and-angular-js/)
- [JJWT Library](https://github.com/jwtk/jjwt)
- [Springdoc OpenAPI](https://springdoc.org)

---

**Resultado esperado:**  
Backend corriendo en `http://localhost:8080`, documentado por Swagger, conectado a PostgreSQL y protegido con JWT simple.