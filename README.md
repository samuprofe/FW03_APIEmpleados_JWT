# 🔐 API REST de Empleados con JWT

API RESTful desarrollada con Spring Boot para la gestión de empleados, implementando autenticación y autorización mediante JSON Web Tokens (JWT).

## 📋 Descripción

Esta API proporciona un sistema completo de gestión de empleados y departamentos con seguridad basada en tokens JWT. Permite realizar operaciones CRUD sobre empleados y departamentos, con un sistema de autenticación robusto que garantiza el acceso seguro a los recursos.

## 🚀 Tecnologías Utilizadas

- **Java 17+**
- **Spring Boot 3.x**
- **Spring Security**
- **JWT (JSON Web Tokens)**
- **Spring Data JPA**
- **MySQL/H2 Database**
- **Maven**
- **Lombok**

## ✨ Características

- ✅ Autenticación con JWT
- ✅ Registro de usuarios
- ✅ Login seguro
- ✅ CRUD completo de empleados
- ✅ CRUD completo de departamentos
- ✅ Relación entre empleados y departamentos
- ✅ Validación de tokens
- ✅ Protección de endpoints con roles
- ✅ Gestión de excepciones personalizada
- ✅ Documentación de API

## 📦 Requisitos Previos

Antes de comenzar, asegúrate de tener instalado:

- Java JDK 17 o superior
- Maven 3.6+
- MySQL 8.0+ (o usa H2 en memoria)
- Un IDE como IntelliJ IDEA o Eclipse (opcional)

## 🔧 Instalación

1. **Clona el repositorio**

```bash
git clone https://github.com/samuprofe/FW03_APIEmpleados_JWT.git
cd FW03_APIEmpleados_JWT
```

2. **Configura la base de datos**

Edita el archivo `src/main/resources/application.properties`:

```properties
# Configuración de la base de datos
spring.datasource.url=jdbc:mysql://localhost:3306/empleados_db
spring.datasource.username=tu_usuario
spring.datasource.password=tu_contraseña
spring.jpa.hibernate.ddl-auto=update

# Configuración JWT
jwt.secret=tuClaveSecretaSuperSegura
jwt.expiration=86400000
```

3. **Instala las dependencias**

```bash
mvn clean install
```

4. **Ejecuta la aplicación**

```bash
mvn spring-boot:run
```

La API estará disponible en `http://localhost:8080`

## 🔑 Endpoints de la API

### Autenticación

| Método | Endpoint | Descripción | Autenticación |
|--------|----------|-------------|---------------|
| POST | `/api/auth/register` | Registrar nuevo usuario | No |
| POST | `/api/auth/login` | Iniciar sesión | No |

### Empleados

| Método | Endpoint | Descripción | Autenticación |
|--------|----------|-------------|---------------|
| GET | `/api/empleados` | Listar todos los empleados | Sí |
| GET | `/api/empleados/{id}` | Obtener empleado por ID | Sí |
| POST | `/api/empleados` | Crear nuevo empleado | Sí |
| PUT | `/api/empleados/{id}` | Actualizar empleado | Sí |
| DELETE | `/api/empleados/{id}` | Eliminar empleado | Sí |

### Departamentos

| Método | Endpoint | Descripción | Autenticación |
|--------|----------|-------------|---------------|
| GET | `/api/departamentos` | Listar todos los departamentos | Sí |
| GET | `/api/departamentos/{id}` | Obtener departamento por ID | Sí |
| POST | `/api/departamentos` | Crear nuevo departamento | Sí |
| PUT | `/api/departamentos/{id}` | Actualizar departamento | Sí |
| DELETE | `/api/departamentos/{id}` | Eliminar departamento | Sí |
| GET | `/api/departamentos/{id}/empleados` | Listar empleados de un departamento | Sí |

## 📝 Ejemplos de Uso

### Registro de Usuario

```bash
curl -X POST http://localhost:8080/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "username": "usuario",
    "email": "usuario@example.com",
    "password": "password123"
  }'
```

### Login

```bash
curl -X POST http://localhost:8080/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "username": "usuario",
    "password": "password123"
  }'
```

**Respuesta:**
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "type": "Bearer",
  "username": "usuario"
}
```

### Crear Empleado

```bash
curl -X POST http://localhost:8080/api/empleados \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer {tu_token}" \
  -d '{
    "nombre": "Juan",
    "apellidos": "Pérez García",
    "email": "juan.perez@empresa.com",
    "departamento": "IT",
    "salario": 35000
  }'
```

### Listar Empleados

```bash
curl -X GET http://localhost:8080/api/empleados \
  -H "Authorization: Bearer {tu_token}"
```

### Crear Departamento

```bash
curl -X POST http://localhost:8080/api/departamentos \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer {tu_token}" \
  -d '{
    "nombre": "Recursos Humanos",
    "descripcion": "Gestión del personal y relaciones laborales",
    "ubicacion": "Edificio A - Planta 2"
  }'
```

### Listar Departamentos

```bash
curl -X GET http://localhost:8080/api/departamentos \
  -H "Authorization: Bearer {tu_token}"
```

### Obtener Empleados de un Departamento

```bash
curl -X GET http://localhost:8080/api/departamentos/1/empleados \
  -H "Authorization: Bearer {tu_token}"
```

## 📁 Estructura del Proyecto

```
FW03_APIEmpleados_JWT/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/empresa/empleados/
│   │   │       ├── config/          # Configuración de seguridad
│   │   │       ├── controller/      # Controladores REST
│   │   │       ├── dto/             # Data Transfer Objects
│   │   │       ├── entity/          # Entidades JPA
│   │   │       ├── repository/      # Repositorios
│   │   │       ├── security/        # Filtros y utilidades JWT
│   │   │       ├── service/         # Lógica de negocio
│   │   │       └── exception/       # Manejo de excepciones
│   │   └── resources/
│   │       └── application.properties
│   └── test/
├── pom.xml
└── README.md
```

## 🔒 Seguridad

- Las contraseñas se almacenan encriptadas usando BCrypt
- Los tokens JWT expiran después de 24 horas (configurable)
- Los endpoints protegidos requieren un token válido en el header `Authorization: Bearer {token}`
- Validación de roles para diferentes operaciones

## 🛠️ Configuración Adicional

### Cambiar el puerto del servidor

```properties
server.port=8090
```

### Configurar tiempo de expiración del token (en milisegundos)

```properties
jwt.expiration=3600000  # 1 hora
```

### Usar H2 en memoria (para desarrollo)

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.h2.console.enabled=true
```

## 🧪 Testing

Ejecuta las pruebas con:

```bash
mvn test
```

## 🤝 Contribución

Las contribuciones son bienvenidas. Para contribuir:

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para más detalles.

## 👨‍💻 Autor

**Samuel** - [samuprofe](https://github.com/samuprofe)

## 📞 Contacto

Si tienes alguna pregunta o sugerencia, no dudes en contactar.

---

⭐ Si este proyecto te ha sido útil, considera darle una estrella en GitHub
