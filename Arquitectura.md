## 1. Estilo Arquitectónico

Estilo adoptado: Arquitectura REST

Justificación basada en REF priorizados:

| REF ID | Descripción | Prioridad | Cómo lo aborda el estilo |
|---|---|---|---|
| REF-01 | El sistema debe responder en menos de 2 segundos en operaciones comunes | Alta | Al usar formatos livianos y permitir que el navegador guarde respuestas a consultas frecuentes, se reduce la carga del servidor y se agiliza la entrega de información. |
| REF-02 | El sistema debe estar disponible al menos un 99% en horario operativo | Alta | La independencia entre la interfaz y el servidor permite que ambos se mantengan de forma separada; si una parte requiere ajustes, no se interrumpe necesariamente el funcionamiento de la otra. |
| REF-03 | Solo usuarios autenticados pueden reservar, cancelar o modificar reservas | Alta | El servidor exige una llave digital de acceso (jwt) en cada solicitud de reserva, permitiendo validar la identidad del usuario de forma segura y directa en cada acción. |
| REF-04 | La interfaz debe ser simple e intuitiva para estudiantes y administradores | Alta | Al separar completamente la apariencia visual de la lógica interna, es posible diseñar interfaces centradas exclusivamente en la facilidad de uso para el estudiante. |
| REF-07 | El sistema debe ser modular y de bajo acoplamiento | Alta | El diseño se organiza en torno a elementos independientes (salas, reservas, usuarios), lo que permite estructurar el sistema en secciones que no dependen rígidamente entre sí. |
| REF-10 | Los datos de reservas deben mantenerse consistentes en todo momento | Alta | El servidor actúa como el único punto de control y validación; todas las solicitudes deben cumplir las mismas reglas antes de que cualquier cambio se guarde permanentemente. |

Explicación textual:  
Se adopta un estilo REST que desacopla la presentación de la lógica de negocio. El sistema se organiza en torno a recursos (Salas, Reservas) accesibles mediante una interfaz uniforme. Esta elección garantiza que tanto la aplicación para estudiantes como el panel de administración consuman la misma lógica de negocio, asegurando integridad y permitiendo que cada parte del sistema evolucione de forma independiente.

## 2. Diagrama de Arquitectura

![Diagrama de Arquitectura](./imagen/diagrama_arquitectura.png)

## 3. Descomposición Modular

Fundamentación:  
La descomposición se basa en una arquitectura de sistemas distribuidos, separando las interfaces de cliente según el rol del usuario y centralizando la lógica y persistencia en un Backend robusto.

### Módulo 1: Frontend Web/Mobile (Interfaz de Usuario)
- **Responsabilidad:** Proveer la interfaz principal para que los estudiantes visualicen, filtren y reserven salas de estudio.
- **Ofrece a otros módulos:** Captura de datos de usuario y solicitudes de reserva.
- **Depende de:** API REST (Módulo 3).

### Módulo 2: Panel de Control / CMS (Admin Salas)
- **Responsabilidad:** Interfaz dedicada a administradores para la gestión de inventario de salas, configuración de reglas y visualización de métricas.
- **Ofrece a otros módulos:** Comandos de configuración y administración del sistema.
- **Depende de:** API REST (Módulo 3).

### Módulo 3: API REST (Lógica de la App)
- **Responsabilidad:** Orquestar la lógica de negocio, validar autenticación, verificar disponibilidad de salas y procesar transacciones.
- **Ofrece a otros módulos:** Endpoints REST (servicios) para los clientes.
- **Depende de:** Base de Datos (Módulo 4).

### Módulo 4: Base de Datos (Horas Agendadas)
- **Responsabilidad:** Almacenamiento persistente de toda la información del dominio (usuarios, salas, reservas y reglas).
- **Ofrece a otros módulos:** Operaciones de lectura y escritura de datos (CRUD).
- **Depende de:** Ninguno.

## 4. Decisiones de Diseño

### Decisión 1
- **Decisión:** Implementar dos clientes independientes (Frontend y Panel de Control).
- **Motivación:** Separa las preocupaciones de seguridad y usabilidad entre estudiantes y administradores (REF-04, REF-07).
- **Impacto:** Mayor seguridad al aislar funciones administrativas.

### Decisión 2
- **Decisión:** Uso de API REST como único punto de acceso a datos.
- **Motivación:** Asegura que todas las reglas de negocio se apliquen de forma consistente (REF-10).
- **Impacto:** Facilita el mantenimiento y futuras integraciones.
