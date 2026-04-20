## 1. Estilo Arquitectónico

Estilo adoptado: Arquitectura REST

Justificación basada en REF priorizados:

| REF ID | Descripción | Prioridad | Cómo lo aborda el estilo |
|---|---|---|---|
| REF-01 | El sistema debe responder en menos de 2 segundos en operaciones comunes | Alta | La comunicación mediante recursos estandarizados y formatos ligeros (como JSON) optimiza la transferencia de datos y los tiempos de respuesta. |
| REF-02 | El sistema debe estar disponible al menos un 99% en horario operativo | Alta | Su naturaleza *stateless* (sin estado) y el alto desacoplamiento permiten que el cliente y la API se desplieguen y mantengan de forma independiente, aislando fallos. |
| REF-03 | Solo usuarios autenticados pueden reservar, cancelar o modificar reservas | Alta | La seguridad se gestiona centralizadamente exigiendo tokens de autenticación/autorización en cada petición HTTP hacia los recursos sensibles. |
| REF-04 | La interfaz debe ser simple e intuitiva para estudiantes y administradores | Alta | Al estar totalmente desacoplado, el cliente (frontend) se libera de la lógica de negocio y puede enfocarse al 100% en la experiencia de usuario consumiendo la API. |
| REF-07 | El sistema debe ser modular y de bajo acoplamiento | Alta | El diseño orientado a recursos (salas, usuarios, reservas) permite estructurar la API en endpoints independientes, reduciendo dependencias directas. |
| REF-10 | Los datos de reservas deben mantenerse consistentes en todo momento | Alta | Las operaciones se realizan a través de verbos HTTP específicos (POST, PUT, DELETE) sobre recursos únicos, siendo la API la única puerta de entrada que valida y garantiza la consistencia antes de persistir. |

Explicación textual:  
Se adopta un estilo arquitectónico REST basado en la gestión de recursos a través de servicios web. Esta elección proporciona un alto grado de desacoplamiento entre la interfaz de usuario y la lógica subyacente, ya que interactúan exclusivamente mediante endpoints estandarizados y verbos HTTP. Esta arquitectura es ideal para el sistema de reserva de salas porque su naturaleza *stateless* (sin estado de sesión en el servidor) favorece la escalabilidad y el rendimiento. Tratar las entidades del dominio (salas, reservas, usuarios) como recursos independientes mejora significativamente la modularidad, facilita la seguridad mediante la validación de peticiones individuales y permite integrar futuras funcionalidades de administración sin alterar la estructura base de los servicios expuestos a los estudiantes.

## 2. Diagrama de Arquitectura

![Diagrama de Arquitectura](https://github.com/Proyecto-sala-de-estudio/sala-de-estudio/blob/main/imagen/diagrama_arquitectura.jpg)

## 3. Descomposición Modular

Fundamentación:  
La descomposición modular se realiza por funcionalidad del dominio, separando responsabilidades asociadas a estudiantes, reservas, salas y administración, con el objetivo de mantener alta cohesión y un bajo acoplamiento al exponer o consumir recursos.

### Módulo 1: Interfaz de Usuario
- Responsabilidad: Mostrar la información al usuario y permitir la interacción fluida con el sistema.
- Ofrece a otros módulos: Solicitudes de consulta, reserva, cancelación, edición y administración.
- Depende de: Backend API (consumo de recursos REST).

### Módulo 2: Gestión de Usuarios
- Responsabilidad: Administrar usuarios, su facultad y su rol dentro del sistema.
- Ofrece a otros módulos: Información de usuario y validación contextual.
- Depende de: Base de Datos.

### Módulo 3: Gestión de Salas
- Responsabilidad: Administrar información de salas, ubicación, capacidad, equipamiento y disponibilidad.
- Ofrece a otros módulos: Datos de salas y consulta de disponibilidad.
- Depende de: Base de Datos.

### Módulo 4: Gestión de Reservas
- Responsabilidad: Crear, cancelar, consultar y modificar reservas asociadas a los recursos.
- Ofrece a otros módulos: Estado actual e histórico de reservas.
- Depende de: Gestión de Usuarios, Gestión de Salas, Base de Datos.

### Módulo 5: Administración
- Responsabilidad: Gestionar salas, visualizar estadísticas de uso y configurar reglas del sistema.
- Ofrece a otros módulos: Control administrativo, reportes y configuración.
- Depende de: Gestión de Salas, Gestión de Reservas, Base de Datos.

### Módulo 6: Backend API
- Responsabilidad: Exponer los recursos del sistema mediante servicios REST al frontend y coordinar la lógica de negocio.
- Ofrece a otros módulos: Endpoints estandarizados para operaciones sobre usuarios, salas, reservas y administración.
- Depende de: Gestión de Usuarios, Gestión de Salas, Gestión de Reservas, Administración.

### Módulo 7: Base de Datos
- Responsabilidad: Persistir los recursos (usuarios, salas, reservas) y reglas del sistema.
- Ofrece a otros módulos: Almacenamiento y recuperación de información.
- Depende de: Ninguno.

## 4. Decisiones de Diseño

### Decisión 1
- Decisión: Utilizar una API REST como mecanismo único de comunicación entre frontend y backend.
- Motivación: Favorece la separación de responsabilidades, mantenibilidad y escalabilidad (REF-01, REF-07, REF-09).
- Alternativas consideradas: Comunicación directa del frontend con la base de datos o renderizado desde el servidor.
- Impacto: Mejora seguridad, control de acceso y permite la reutilización de servicios en futuras plataformas (ej. aplicación móvil).

### Decisión 2
- Decisión: Centralizar la validación de reservas exclusivamente en el backend (API).
- Motivación: Garantizar integridad y consistencia en la disponibilidad de salas, sin confiar ciegamente en el cliente (REF-10).
- Alternativas consideradas: Validar únicamente desde el frontend.
- Impacto: Disminuye errores, evita colisiones (reservas simultáneas) y mejora la confiabilidad general del sistema.

### Decisión 3
- Decisión: Separar la administración en un módulo independiente.
- Motivación: Las funcionalidades administrativas tienen responsabilidades distintas a las de los estudiantes y requieren operaciones de control específicas sobre los recursos (REF-07).
- Alternativas consideradas: Integrar funciones de administración dentro de los módulos de estudiantes.
- Impacto: Mejora la claridad del diseño, protege endpoints críticos y facilita la evolución paralela del sistema.

### Decisión 4
- Decisión: Implementar autenticación obligatoria y sin estado (ej. JWT) para acciones sensibles.
- Motivación: Resguardar reservas, reglas del sistema y acciones administrativas asegurando cada petición individualmente (REF-03).
- Alternativas consideradas: Permitir acciones sin autenticación o usar sesiones tradicionales almacenadas en memoria.
- Impacto: Aumenta la seguridad del sistema y mantiene la compatibilidad con los principios del estilo arquitectónico REST.
