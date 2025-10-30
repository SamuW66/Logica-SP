<h1>💼 Proyecto AppBank - Lógica y Programación con Spring Boot</h1>

Este proyecto fue diseñado de manera estructurada para mostrar cómo funciona un sistema bancario básico, construido con una organización clara y separando las responsabilidades en diferentes capas. Todo comienza con la clase principal, que se encarga de iniciar la aplicación y preparar el entorno para que el resto de los componentes puedan operar de forma ordenada. Desde ahí, las peticiones del usuario son manejadas por distintas partes del sistema que cooperan entre sí, haciendo que el código sea fácil de entender, mantener y extender en el futuro.

La capa que se encuentra en contacto directo con el usuario es el controlador, llamado **BankController**. Su papel es similar al de un asistente en ventanilla: recibe las solicitudes del cliente, como abrir una cuenta, realizar depósitos, retirar fondos o revisar transacciones. El controlador no realiza las operaciones por sí mismo, sino que valida los datos básicos y luego los envía al servicio correspondiente, que es el encargado de ejecutar la lógica central. Esto permite mantener una separación clara entre la comunicación externa y las reglas internas del negocio.

La parte más importante de la aplicación está en la lógica de negocio, representada por la interfaz **BankService** y su clase de implementación **BankServiceImpl**. En este módulo se definen las reglas que determinan cómo deben comportarse las operaciones bancarias. Aquí se revisa que las cuentas existan, que los montos sean válidos, que haya fondos disponibles antes de realizar un retiro y que toda transacción cumpla con las normas del sistema. Si ocurre algo que no está permitido, se lanza una excepción personalizada, **DomainException**, que informa al usuario o al controlador del motivo del error.

El modelo del sistema agrupa las clases que representan los componentes reales del banco. La clase **Customer** describe a los clientes y almacena su información personal. **Account** funciona como la base para todos los tipos de cuentas, manejando el saldo y las operaciones comunes. A partir de ella se crean dos tipos concretos: **CheckingAccount**, que representa una cuenta corriente con un límite de sobregiro, y **SavingsAccount**, una cuenta de ahorro que puede generar intereses. Además, **Transaction** guarda el detalle de cada operación realizada y **Money** se utiliza para manejar las cantidades de dinero de forma precisa, evitando errores en cálculos.

El almacenamiento de los datos se realiza mediante el repositorio **JsonRepository**, que trabaja con archivos JSON ubicados en la carpeta de datos del proyecto. Esta clase se apoya en **FileManager**, que gestiona la lectura y escritura de los archivos, y en **JsonUtil**, que convierte los objetos Java en formato JSON y viceversa. Este tipo de persistencia es ideal para proyectos educativos o demostraciones, ya que permite conservar la información sin necesidad de una base de datos compleja. Sin embargo, en aplicaciones más grandes, sería conveniente reemplazarlo por un sistema de base de datos relacional o NoSQL.

Un aspecto técnico interesante del proyecto es el uso del patrón de diseño **Strategy** para calcular los intereses de las cuentas de ahorro. Mediante la interfaz **InterestStrategy** y las clases concretas **SimpleRateStrategy** y **TieredRateStrategy**, se pueden aplicar diferentes métodos de cálculo sin modificar el resto del sistema. Este enfoque hace que la aplicación sea más flexible y fácil de adaptar a distintos escenarios financieros.

En la carpeta `src/test` se encuentra una clase que verifica que:
- La aplicación arranca correctamente.  
- Los componentes principales funcionan como se espera.

Aunque las pruebas actuales son básicas, representan un punto de partida para agregar más casos que validen depósitos, retiros, transferencias y almacenamiento de datos.

---

<h2>👨‍💻 Autor <h2>

Proyecto desarrollado por **Samuel López** como práctica universitaria de programación y lógica orientada a objetos con **Java + Spring Boot**.

---

<h2>⚡ Thunder Client <h2>

**Thunder Client** es una extensión integrada en **Visual Studio Code** que facilita la **prueba de endpoints de una API REST** sin necesidad de usar herramientas externas como Postman.  
En este proyecto se utilizó para **validar el correcto funcionamiento de las operaciones bancarias**, como la creación de clientes, manejo de cuentas, depósitos y retiros.

### 🧩 Pasos para realizar las pruebas

1. Abre la pestaña **Thunder Client** en la barra lateral de VS Code.  
2. Crea una nueva solicitud seleccionando **New Request**.  
3. Elige el método HTTP adecuado según la operación:
   - `POST` → Crear clientes o cuentas nuevas.  
   - `GET` → Consultar información existente.  
   - `PUT` → Actualizar datos ya registrados.  
   - `DELETE` → Eliminar registros.  
4. En la barra de dirección, escribe la URL del endpoint.  
   Ejemplo: http://localhost:8080/api/customers
5. Si el endpoint requiere datos, agrégalos en el cuerpo de la solicitud en formato **JSON**.  
6. Finalmente, presiona **Send** y observa la respuesta del servidor.

---

<p align="center">
<img width="1919" height="1079" alt="C 1" src="https://github.com/user-attachments/assets/71f86dd7-2bf6-437f-a77e-9ed88d82766b" />

<img width="1919" height="1079" alt="C 2" src="https://github.com/user-attachments/assets/9d619b92-c06b-4a05-bf67-b9370d6ae773" />

<img width="1919" height="1079" alt="C 3" src="https://github.com/user-attachments/assets/0b11bc51-7d0e-4818-8046-bfa32010c6f2" />
</p>



