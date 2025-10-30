# 🏦 Sistema Bancario - Lógica y Solución de Problemas

## 📋 Información del Proyecto

**Institución:** Universidad EAFIT  
**Curso:** Lógica - Solución de Problemas  
**Entregable:** #3  
**Fecha de Entrega:** 30 de octubre de 2025  
**Repositorio:** [GitHub - Logica-SP](https://github.com/SamuW66/Logica-SP)

---

## 📘 Descripción General

Este proyecto implementa un **sistema bancario completo** utilizando Java y Spring Boot, diseñado con una arquitectura en capas que separa claramente las responsabilidades. El sistema permite gestionar clientes, cuentas bancarias (ahorros y corrientes), realizar operaciones financieras (depósitos, retiros, transferencias) y aplicar intereses.

### 🎯 Objetivos del Proyecto

- Implementar un sistema bancario funcional con arquitectura limpia
- Aplicar principios de diseño de software (SOLID, patrones de diseño)
- Crear una API REST documentada con Swagger
- Realizar pruebas exhaustivas de todos los endpoints
- Gestionar persistencia de datos mediante archivos JSON

---

## 🏗️ Arquitectura del Sistema

El proyecto sigue una arquitectura en capas con separación clara de responsabilidades:

### 📦 Estructura de Capas

```
src/main/java/com/logsoluprobl/appbank/
├── controller/          # Capa de presentación (API REST)
├── service/            # Lógica de negocio
├── model/              # Entidades del dominio
├── repository/         # Persistencia de datos
├── exception/          # Manejo de excepciones
└── util/              # Utilidades (JSON, archivos)
```

### 🔹 Controller (Controlador)

**Clase:** `BankController`

El controlador actúa como punto de entrada de la API REST. Recibe las peticiones HTTP, valida los datos básicos y delega la lógica de negocio al servicio correspondiente.

**Responsabilidades:**
- Mapear endpoints REST
- Validar datos de entrada
- Manejar respuestas HTTP
- Gestionar códigos de estado

### 🔹 Service (Servicio)

**Interfaz:** `BankService`  
**Implementación:** `BankServiceImpl`

La capa de servicio contiene toda la lógica de negocio del sistema bancario.

**Reglas de negocio implementadas:**
- Verificación de existencia de clientes y cuentas
- Validación de montos (positivos, suficientes)
- Comprobación de fondos antes de retiros
- Gestión de límites de sobregiro en cuentas corrientes
- Registro automático de transacciones
- Aplicación de intereses a cuentas de ahorro

### 🔹 Model (Modelo)

El modelo representa las entidades del dominio bancario:

| Clase | Descripción |
|-------|-------------|
| `Customer` | Datos personales del cliente (ID, nombre, email) |
| `Account` | Clase base abstracta para cuentas bancarias |
| `SavingsAccount` | Cuenta de ahorros con tasa de interés |
| `CheckingAccount` | Cuenta corriente con límite de sobregiro |
| `Transaction` | Registro de operaciones (DEP, WDR, TRF) |
| `Money` | Manejo preciso de cantidades monetarias |

**Jerarquía de cuentas:**
```
Account (abstracta)
├── SavingsAccount
└── CheckingAccount
```

### 🔹 Repository (Repositorio)

**Clase:** `JsonRepository`

Gestiona la persistencia de datos mediante archivos JSON.

**Componentes:**
- `FileManager`: Lectura/escritura de archivos
- `JsonUtil`: Serialización/deserialización JSON

**Ventajas:**
- ✅ No requiere base de datos externa
- ✅ Ideal para proyectos educativos
- ✅ Datos persistentes entre ejecuciones
- ✅ Fácil visualización y depuración

### 🔹 Strategy Pattern (Patrón Estrategia)

Implementación del patrón Strategy para cálculo de intereses:

```java
InterestStrategy
├── SimpleRateStrategy      // Tasa fija
└── TieredRateStrategy      // Tasa por escalas
```

**Beneficios:**
- Permite múltiples algoritmos de cálculo
- Extensible sin modificar código existente
- Aplicable a diferentes tipos de cuenta

---

## 🚀 Tecnologías Utilizadas

| Tecnología | Versión | Propósito |
|------------|---------|-----------|
| Java | 17+ | Lenguaje de programación |
| Spring Boot | 3.x | Framework web y REST |
| Swagger/OpenAPI | 3.0 | Documentación de API |
| Maven | 3.8+ | Gestión de dependencias |
| Jackson | 2.x | Procesamiento JSON |
| JUnit | 5.x | Pruebas unitarias |

---

## 📂 Estructura del Proyecto

```
Logica-SP/
├── src/
│   ├── main/
│   │   ├── java/com/logsoluprobl/appbank/
│   │   │   ├── controller/
│   │   │   │   └── BankController.java
│   │   │   ├── service/
│   │   │   │   ├── BankService.java
│   │   │   │   └── BankServiceImpl.java
│   │   │   ├── model/
│   │   │   │   ├── Customer.java
│   │   │   │   ├── Account.java
│   │   │   │   ├── SavingsAccount.java
│   │   │   │   ├── CheckingAccount.java
│   │   │   │   ├── Transaction.java
│   │   │   │   └── Money.java
│   │   │   ├── repository/
│   │   │   │   └── JsonRepository.java
│   │   │   ├── exception/
│   │   │   │   └── DomainException.java
│   │   │   └── util/
│   │   │       ├── FileManager.java
│   │   │       └── JsonUtil.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       └── java/
│           └── AppbankApplicationTests.java
├── screenshots/
│   ├── swagger/           # Capturas de Swagger UI
│   └── thunder/          # Capturas de Thunder Client
├── thunder-collection.json
├── pom.xml
└── README.md
```

---

## 🔧 Instalación y Configuración

### Requisitos Previos

- Java JDK 17 o superior
- Maven 3.8+
- IDE (IntelliJ IDEA, Eclipse, VS Code)
- Git

### Pasos de Instalación

1. **Clonar el repositorio**
```bash
git clone https://github.com/SamuW66/Logica-SP.git
cd Logica-SP
```

2. **Compilar el proyecto**
```bash
mvn clean install
```

3. **Ejecutar la aplicación**
```bash
mvn spring-boot:run
```

4. **Verificar que está funcionando**
- Aplicación: `http://localhost:8080`
- Swagger UI: `http://localhost:8080/swagger-ui.html`

---

## 📡 Endpoints de la API

### Base URL
```
http://localhost:8080/api/bank
```

### 👥 Gestión de Clientes

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/customers` | Crear nuevo cliente |
| GET | `/customers` | Listar todos los clientes |
| GET | `/customers/{customerId}` | Consultar cliente por ID |

### 💳 Gestión de Cuentas

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/customers/{customerId}/accounts` | Crear cuenta (ahorro/corriente) |
| GET | `/accounts/{accountId}` | Consultar cuenta por ID |
| GET | `/customers/{customerId}/accounts` | Listar cuentas de un cliente |

### 💰 Operaciones Bancarias

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/accounts/{accountId}/deposit` | Realizar depósito |
| POST | `/accounts/{accountId}/withdraw` | Realizar retiro |
| POST | `/accounts/{fromAccountId}/transfer` | Transferir entre cuentas |
| GET | `/accounts/{accountId}/transactions` | Consultar transacciones |
| POST | `/accounts/{accountId}/apply-interest` | Aplicar intereses |

---

## 📖 Ejemplos de Uso

### Crear Cliente

**Request:**
```http
POST /api/bank/customers
Content-Type: application/json

{
  "id": "C001",
  "name": "Lamine Yamal",
  "email": "yamallamine@gmail.com"
}
```

**Response:** `201 Created`
```json
{
  "id": "C001",
  "name": "Lamine Yamal",
  "email": "yamallamine@gmail.com",
  "accounts": null
}
```

### Crear Cuenta de Ahorros

**Request:**
```http
POST /api/bank/customers/C001/accounts
Content-Type: application/json

{
  "type": "SAVINGS",
  "accountId": "A001",
  "parameter": 3.5
}
```

**Response:** `201 Created`
```json
{
  "id": "A001",
  "owner": {
    "id": "C001",
    "name": "Lamine Yamal",
    "email": "yamallamine@gmail.com"
  },
  "balance": {
    "amount": 0,
    "currency": "USD"
  },
  "transactions": [],
  "interestRate": 3.5
}
```

### Realizar Depósito

**Request:**
```http
POST /api/bank/accounts/A001/deposit?amount=2000
```

**Response:** `201 Created`
```json
true
```

### Realizar Transferencia

**Request:**
```http
POST /api/bank/accounts/A001/transfer
Content-Type: application/json

{
  "toAccountId": "A002",
  "amount": 600
}
```

**Response:** `200 OK`
```json
true
```

---

## 🧪 Pruebas del Sistema

### ⚡ Thunder Client

Thunder Client es una extensión de VS Code utilizada para probar endpoints de API REST de forma integrada.

#### Configuración

1. Instalar extensión Thunder Client en VS Code
2. Importar colección: `thunder-collection.json`
3. Ejecutar requests en orden

#### Capturas de Thunder Client

![Vista General Thunder Client](screenshots/thunder/thunder-03-vista-general.png)
*Interfaz principal de Thunder Client mostrando las colecciones de pruebas*

![Ejemplo Request 1](screenshots/thunder/thunder-01-ejemplo-request.png)
*Ejemplo de petición POST para crear cliente*

![Ejemplo Request 2](screenshots/thunder/thunder-02-ejemplo-request.png)
*Ejemplo de petición GET para consultar información*

### 🟢 Swagger UI

Swagger proporciona documentación interactiva de la API y permite probar todos los endpoints desde el navegador.

**Acceso:** `http://localhost:8080/swagger-ui.html`

---

## 📸 Evidencias de Funcionamiento

Todas las pruebas fueron realizadas el **30 de octubre de 2025** entre las **06:38 y 07:01 GMT**.

### Pruebas Completas con Swagger UI

#### 1. Crear Cliente
![Crear Cliente](screenshots/swagger/01-crear-cliente-swagger.png)
**POST** `/api/bank/customers` → Response: `201 Created`

#### 2. Consultar Cliente por ID
![Consultar Cliente](screenshots/swagger/02-consultar-cliente-swagger.png)
**GET** `/api/bank/customers/{customerId}` → Response: `200 OK`

#### 3. Listar Todos los Clientes
![Listar Clientes](screenshots/swagger/03-listar-clientes-swagger.png)
**GET** `/api/bank/customers` → Response: `200 OK`

#### 4. Crear Cuenta de Ahorros
![Crear Cuenta Ahorros](screenshots/swagger/04-crear-cuenta-ahorros-swagger.png)
**POST** `/api/bank/customers/{customerId}/accounts` → Response: `201 Created`

#### 5. Crear Cuenta Corriente
![Crear Cuenta Corriente](screenshots/swagger/05-crear-cuenta-corriente-swagger.png)
**POST** `/api/bank/customers/{customerId}/accounts` → Response: `201 Created`

#### 6. Consultar Cuenta por ID
![Consultar Cuenta](screenshots/swagger/06-consultar-cuenta-swagger.png)
**GET** `/api/bank/accounts/{accountId}` → Response: `200 OK`

#### 7. Listar Cuentas de un Cliente
![Listar Cuentas](screenshots/swagger/07-listar-cuentas-swagger.png)
**GET** `/api/bank/customers/{customerId}/accounts` → Response: `200 OK`

#### 8. Realizar Depósito
![Depósito](screenshots/swagger/08-deposito-swagger.png)
**POST** `/api/bank/accounts/{accountId}/deposit` → Response: `201 Created`

#### 9. Realizar Retiro
![Retiro](screenshots/swagger/09-retiro-swagger.png)
**POST** `/api/bank/accounts/{accountId}/withdraw` → Response: `201 Created`

#### 10. Realizar Transferencia
![Transferencia](screenshots/swagger/10-transferencia-swagger.png)
**POST** `/api/bank/accounts/{fromAccountId}/transfer` → Response: `200 OK`

#### 11. Consultar Transacciones
![Transacciones](screenshots/swagger/11-transacciones-swagger.png)
**GET** `/api/bank/accounts/{accountId}/transactions` → Response: `200 OK`

#### 12. Aplicar Intereses
![Aplicar Intereses](screenshots/swagger/12-aplicar-intereses-swagger.png)
**POST** `/api/bank/accounts/{accountId}/apply-interest` → Response: `200 OK`

---

## 📦 Colección de Pruebas (Postman/Thunder Client)

El archivo **`thunder-collection.json`** contiene todas las pruebas de los endpoints realizadas durante el desarrollo y puede ser importado en:

- ✅ **Thunder Client** (VS Code)
- ✅ **Postman** (Desktop/Web)

### Importar en Thunder Client

1. Abrir Thunder Client en VS Code
2. Ir a la pestaña **Collections**
3. Clic en el menú (⋮) → **Import**
4. Seleccionar `thunder-collection.json`
5. Ejecutar los requests en orden

### Importar en Postman

1. Abrir Postman
2. Clic en **Import**
3. Seleccionar `thunder-collection.json`
4. La colección estará lista para usar

---

## ✅ Resumen de Validaciones

| Herramienta | Endpoints Probados | Estado | Fecha |
|-------------|-------------------|--------|-------|
| Thunder Client | 12 | ✅ Exitoso | 30/10/2025 |
| Swagger UI | 12 | ✅ Exitoso | 30/10/2025 |

### Operaciones Validadas

✅ Creación de clientes  
✅ Consulta de clientes por ID  
✅ Listado de todos los clientes  
✅ Creación de cuentas de ahorro  
✅ Creación de cuentas corrientes  
✅ Consulta de cuentas por ID  
✅ Listado de cuentas por cliente  
✅ Depósitos con validación de montos  
✅ Retiros con verificación de fondos  
✅ Transferencias entre cuentas  
✅ Historial de transacciones  
✅ Aplicación de intereses  

**Total:** 24 pruebas exitosas (12 Thunder Client + 12 Swagger)

Todas las capturas incluyen **fecha y hora de ejecución** como evidencia de las pruebas realizadas.

---

## 🧪 Testing

### Pruebas Unitarias

El proyecto incluye pruebas básicas en `src/test/`:

```bash
mvn test
```

### Cobertura Actual

- ✅ Inicialización de la aplicación
- ✅ Carga de componentes Spring
- 🔄 Pruebas de integración (en desarrollo)

---

## 🔐 Manejo de Errores

### Excepciones Personalizadas

**`DomainException`**: Excepción lanzada cuando se violan reglas de negocio.

**Casos de uso:**
- Cliente no encontrado
- Cuenta no encontrada
- Fondos insuficientes
- Monto inválido (negativo o cero)
- Tipo de cuenta no válido

### Códigos de Estado HTTP

| Código | Descripción |
|--------|-------------|
| 200 | Operación exitosa |
| 201 | Recurso creado exitosamente |
| 400 | Error en datos enviados |
| 404 | Recurso no encontrado |
| 500 | Error interno del servidor |

---

## 🚀 Características Principales

### ✨ Funcionalidades Implementadas

- [x] Gestión completa de clientes
- [x] Dos tipos de cuentas (ahorro y corriente)
- [x] Operaciones bancarias básicas (depósito, retiro, transferencia)
- [x] Registro automático de transacciones
- [x] Cálculo y aplicación de intereses
- [x] Límite de sobregiro en cuentas corrientes
- [x] Persistencia en JSON
- [x] API REST documentada con Swagger
- [x] Validaciones de negocio
- [x] Manejo robusto de errores

### 🎨 Principios de Diseño Aplicados

- **SOLID**: Separación de responsabilidades, interfaces claras
- **DRY**: Código reutilizable sin duplicación
- **Strategy Pattern**: Flexibilidad en cálculo de intereses
- **Repository Pattern**: Abstracción de persistencia
- **Clean Architecture**: Capas bien definidas

---

## 📚 Documentación Adicional

### Swagger/OpenAPI

La documentación completa de la API está disponible en Swagger UI cuando la aplicación está en ejecución:

```
http://localhost:8080/swagger-ui.html
```

Características de Swagger:
- 📖 Documentación interactiva
- 🧪 Pruebas en vivo de endpoints
- 📝 Especificación OpenAPI 3.0
- 🔍 Exploración de modelos de datos

---

## 🤝 Contribuciones

Este proyecto fue desarrollado como parte del curso de Lógica - Solución de Problemas de la Universidad EAFIT.

### Autor

**Samuel Walteros**  
GitHub: [@SamuW66](https://github.com/SamuW66)

---

## 📄 Licencia

Este proyecto es de uso educativo para la Universidad EAFIT.

---

## 📞 Contacto y Soporte

Para preguntas o problemas relacionados con el proyecto:

- 📧 Email: [Disponible en el perfil de GitHub]
- 🐛 Issues: [GitHub Issues](https://github.com/SamuW66/Logica-SP/issues)
- 📖 Wiki: [GitHub Wiki](https://github.com/SamuW66/Logica-SP/wiki)

---

## 🎓 Conclusiones

Este proyecto demuestra:

1. ✅ Comprensión de arquitectura en capas
2. ✅ Implementación de API REST con Spring Boot
3. ✅ Aplicación de patrones de diseño
4. ✅ Validación exhaustiva mediante pruebas
5. ✅ Documentación completa del sistema
6. ✅ Persistencia de datos sin base de datos
7. ✅ Manejo profesional de errores
8. ✅ Código limpio y mantenible

---

## 📈 Mejoras Futuras

- [ ] Migración a base de datos relacional (PostgreSQL/MySQL)
- [ ] Implementación de autenticación JWT
- [ ] Pruebas de integración completas
- [ ] Frontend con React/Angular
- [ ] Notificaciones por email
- [ ] Reportes y estadísticas
- [ ] Docker containerization
- [ ] CI/CD con GitHub Actions

---

<div align="center">

**🏦 Sistema Bancario - Lógica y Solución de Problemas**

*Desarrollado con ❤️ para Universidad EAFIT*

[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-green.svg)](https://spring.io/projects/spring-boot)
[![Java](https://img.shields.io/badge/Java-17+-orange.svg)](https://www.oracle.com/java/)
[![Swagger](https://img.shields.io/badge/Swagger-OpenAPI%203.0-brightgreen.svg)](https://swagger.io/)
[![License](https://img.shields.io/badge/License-Educational-blue.svg)](LICENSE)

</div>
</p>



