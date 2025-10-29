<h1> 🏦 Proyecto: Lógica – Solución de Problemas (Sistema Bancario) <h1>

<h2> 📘 Descripción general <h2>

Este proyecto fue diseñado de manera estructurada para mostrar cómo funciona un **sistema bancario básico**, construido con una organización clara y separando las responsabilidades en diferentes capas.  
Todo comienza con la clase principal, que se encarga de iniciar la aplicación y preparar el entorno para que el resto de los componentes puedan operar de forma ordenada.  
Desde ahí, las peticiones del usuario son manejadas por distintas partes del sistema que cooperan entre sí, haciendo que el código sea fácil de entender, mantener y extender en el futuro.

---

<h1> 🧭 Arquitectura del sistema <h1>

<h2> 🔹 Controlador (Controller) <h2>
La capa que se encuentra en contacto directo con el usuario es el **controlador**, llamado `BankController`.  
Su papel es similar al de un asistente en ventanilla: recibe las solicitudes del cliente, como abrir una cuenta, realizar depósitos, retirar fondos o revisar transacciones.  

El controlador **no realiza las operaciones directamente**, sino que valida los datos básicos y luego los envía al **servicio correspondiente**, que ejecuta la lógica central.  
Esto permite mantener una separación clara entre la comunicación externa y las reglas internas del negocio.

---

<h2> 🔹 Lógica de negocio (Service) <h2>
La parte más importante de la aplicación está en la lógica de negocio, representada por la interfaz `BankService` y su implementación `BankServiceImpl`.  
Aquí se definen las **reglas que determinan el comportamiento de las operaciones bancarias**:  
- Verificación de existencia de cuentas.  
- Validación de montos.  
- Comprobación de fondos antes de los retiros.  
- Registro correcto de transacciones.  

Si ocurre algo no permitido, se lanza una excepción personalizada (`DomainException`), que informa al usuario o al controlador del motivo del error.

---

<h2> 🔹 Modelo (Model) <h2>
El modelo agrupa las clases que representan los componentes reales del banco:

- **`Customer`** → datos personales del cliente.  
- **`Account`** → clase base para todos los tipos de cuenta (maneja saldo y operaciones comunes).  
- **`CheckingAccount`** → cuenta corriente con límite de sobregiro.  
- **`SavingsAccount`** → cuenta de ahorro que genera intereses.  
- **`Transaction`** → registra cada operación realizada.  
- **`Money`** → maneja cantidades monetarias con precisión para evitar errores de cálculo.

---

<h2> 🔹 Repositorio (Repository) <h2>
El almacenamiento de datos se realiza mediante la clase `JsonRepository`, que trabaja con **archivos JSON** ubicados en la carpeta de datos del proyecto.  

Esta clase se apoya en:
- **`FileManager`** → gestiona lectura y escritura de archivos.  
- **`JsonUtil`** → convierte objetos Java a JSON y viceversa.  

Este tipo de persistencia es ideal para proyectos educativos, ya que conserva la información sin requerir una base de datos compleja.  
Para entornos más grandes, sería recomendable migrar a una base de datos relacional o NoSQL.

---

<h2> 🔹 Estrategias de interés (Strategy Pattern) <h2>
El proyecto aplica el patrón de diseño **Strategy** para calcular los intereses de las cuentas de ahorro.  

Mediante la interfaz `InterestStrategy` y las clases:
- `SimpleRateStrategy`
- `TieredRateStrategy`

…es posible **aplicar distintos métodos de cálculo sin modificar el resto del sistema**, logrando una aplicación flexible y fácil de adaptar a nuevos escenarios financieros.

---

<h2> 🔹 Pruebas (Testing) <h2>
En la carpeta `src/test` se encuentra una clase que verifica que:
- La aplicación arranca correctamente.
- Los componentes principales funcionan como se espera.

Aunque las pruebas actuales son básicas, representan un punto de partida para agregar más casos que validen depósitos, retiros, transferencias y persistencia de datos.

---

<h2> 🧠 Conclusión <h2>

En general, este proyecto representa una **excelente base para aprender sobre la estructura de aplicaciones Java con Spring Boot**.  
Se destacan buenas prácticas como:
- Separación por capas.  
- Uso del patrón **Strategy**.  
- Manejo adecuado de excepciones.  

Su diseño modular facilita futuras mejoras, como:
- Agregar autenticación de usuarios.  
- Implementar validaciones más estrictas.  
- Migrar a una base de datos profesional.  

---

<h2> 👨‍💻 Autor <h2>
Proyecto desarrollado por Samuel López como práctica universitaria de programación y lógica orientada a objetos con Java + Spring Boot.

---

<h1>🧩 Thunder Client</h1>

<img width="1919" height="1079" alt="C 1" src="https://github.com/user-attachments/assets/ea19f2b3-87d6-42e6-b1b3-3267e9986c52" />

<img width="1919" height="1079" alt="C 2" src="https://github.com/user-attachments/assets/598924d9-0b61-4412-9899-98847ae4bdf9" />

<img width="1919" height="1079" alt="C 3" src="https://github.com/user-attachments/assets/ad13db3e-39f9-419b-a541-db37aa1a21f1" />




