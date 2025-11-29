# 🚀 Guía de Instalación y Entorno — Java Spring Boot + Angular + PostgreSQL
---

## 📋 Contenido
- Verificación rápida del entorno
- Instalación mínima necesaria (solo si falta algo)
- Variables de entorno críticas
- Comandos de verificación rápida

---

## 🧰 Verificación Rápida del Entorno

**⏱️ Tiempo estimado: 5 minutos**

Ejecuta estos comandos para verificar qué tienes instalado:

```bash
java -version
mvn -version
node -v
npm -v
ng version
psql --version
```

Si todos responden correctamente, **¡estás listo!** Si falta algo, sigue las instrucciones abajo.

---

## ☕ 1. Java JDK 25 (Temurin / Adoptium) - **SI FALTA**

**Descarga:** https://adoptium.net

### Pasos rápidos
1. Descarga e instala Temurin JDK 25 (Windows x64 Installer).
2. Durante la instalación, marca `Set JAVA_HOME`.
3. Si no aparece, crea manualmente:
   - `JAVA_HOME` = `C:\Program Files\Eclipse Adoptium\jdk-25`
   - Añadir al `Path`: `%JAVA_HOME%\bin`

### Verificar
```bash
java -version
javac -version
```

---

## ⚙️ 2. Apache Maven - **SI FALTA**

**Descarga:** https://maven.apache.org/download.cgi

### Pasos rápidos
1. Descarga el zip binario (apache-maven-3.9.x-bin.zip).
2. Descomprime en `C:\Program Files\Apache\Maven\apache-maven-3.9.x`.
3. Variables de entorno:
   - `M2_HOME` = `C:\Program Files\Apache\Maven\apache-maven-3.9.x`
   - Añadir al `Path`: `%M2_HOME%\bin`

### Verificar
```bash
mvn -version
```

---

## 🧑‍💻 3. IDE (Recomendado)

**Elige uno:**
- **IntelliJ IDEA Community:** https://www.jetbrains.com/idea/download (recomendado)
- **Spring Tools Suite (STS):** https://spring.io/tools
- **VS Code + extensiones Java:** https://code.visualstudio.com
- **Cursor:** https://cursor.com/download

---

## 🐘 4. PostgreSQL (Instalación Local) - **SI FALTA**

**Descarga:** https://www.postgresql.org/download/windows/

### Pasos rápidos
1. Descarga el instalador de PostgreSQL para Windows.
2. Durante la instalación:
   - Puerto: `5432` (por defecto)
   - Password para usuario `postgres`: `admin` (o el que prefieras, recuérdalo)
   - Deja marcado "Stack Builder" si quieres, pero no es necesario
3. Verifica que el servicio de PostgreSQL esté corriendo (Services → PostgreSQL).

### Verificar
```bash
psql --version
# O desde pgAdmin (incluido en la instalación)
```

**Alternativa rápida (si tienes problemas):** Usa DBeaver para conectarte y crear la base de datos.

---

## 🌐 5. Node.js & Angular CLI - **SI FALTA**

**Node.js:** https://nodejs.org (descarga LTS)

### Pasos rápidos
1. Instala Node.js (marca "Add to PATH" durante la instalación).
2. Instala Angular CLI globalmente:
```bash
npm install -g @angular/cli
```

### Verificar
```bash
node -v
npm -v
ng version
```

---

## 🐼 6. DBeaver (Opcional pero recomendado)

**Descarga:** https://dbeaver.io/download

Útil para visualizar y gestionar la base de datos PostgreSQL de forma gráfica.

---

## 🔧 Variables de Entorno (Windows)

Si necesitas configurarlas manualmente, ve a **Sistema → Configuración avanzada → Variables de entorno**:

- `JAVA_HOME` = `C:\Program Files\Eclipse Adoptium\jdk-25`
- `M2_HOME` = `C:\Program Files\Apache\Maven\apache-maven-3.9.x`
- `PATH` añadir:
  - `%JAVA_HOME%\bin`
  - `%M2_HOME%\bin`

---

## ✅ Checklist Final (5 minutos)

Ejecuta estos comandos y verifica que todos respondan:

```bash
java -version          # Debe mostrar Java 25
mvn -version           # Debe mostrar Maven 3.9.x
node -v                # Debe mostrar v18.x o superior
npm -v                 # Debe mostrar 9.x o superior
ng version             # Debe mostrar Angular CLI
psql --version         # Debe mostrar PostgreSQL 12.x o superior
```

**Si todos responden correctamente, tu entorno está listo para la clase.**

---

## 🛠 Troubleshooting Rápido

### Java no se reconoce
- Verifica que `JAVA_HOME` esté configurado.
- Reinicia la terminal después de configurar variables.

### Maven no se reconoce
- Verifica que `M2_HOME` esté en el `PATH`.
- Reinicia la terminal.

### PostgreSQL no inicia
- Ve a Services (servicios de Windows) y busca "PostgreSQL".
- Inicia el servicio manualmente si está detenido.

### Angular CLI no funciona
- Reinstala ejecutando estos comandos por separado:
```bash
npm uninstall -g @angular/cli
npm install -g @angular/cli
```

---

## 📎 Recursos Útiles

- **Adoptium Temurin JDK:** https://adoptium.net  
- **Maven:** https://maven.apache.org
- **PostgreSQL:** https://www.postgresql.org/download/
- **Node.js:** https://nodejs.org
- **Angular CLI:** https://angular.io/cli
