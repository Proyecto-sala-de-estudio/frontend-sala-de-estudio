## 1. Cambio solicitado
Se requiere agregar un módulo de vigilancia en tiempo real mediante cámaras IP con procesamiento de imagen para detectar ocupación real versus reserva registrada, operando de forma continua.

## 2. Nuevas historias de usuario
### US-11: Monitoreo de reserva
Como administrador,
quiero monitorear en vivo las cámaras de las salas reservadas,
para confirmar si los estudiantes se presentaron y liberar el espacio si está vacío.

​Criterio de aceptación 1: El sistema debe mostrar un indicador de "Transmisión en vivo" en el panel de control del administrador al seleccionar una sala.

​Criterio de aceptación 2: Si la sala está vacía 15 minutos después del inicio de la reserva, el sistema debe habilitar un botón de "Forzar Liberación" que cancele la reserva actual y deje la sala como 'Disponible'.


### US-12: Moniterio de uso
Como administrador,
quiero verificar visualmente la cantidad de personas y el uso de la sala,
para asegurar que se respeta la capacidad máxima y las normativas del recinto.

​Criterio de aceptación 1: La vista de la cámara debe mostrar en pantalla la "Capacidad Máxima Permitida" junto a la "Cantidad Declarada en la Reserva" para facilitar la comparación visual.

​Criterio de aceptación 2: El administrador debe poder enviar una notificación del mal uso de la sala a quien la reservó.

### ​US-13: Monitorear estado de la sala, post uso
Como administrador,
quiero revisar el estado físico de la sala inmediatamente después de que finaliza una reserva,
para identificar posibles daños, desorden o necesidades de mantenimiento antes del siguiente turno.

​Criterio de aceptación 1: El sistema debe sacar una captura automaticamente, de la cámara en el minuto exacto en que finaliza la reserva y guardarla en el historial.

​Criterio de aceptación 2: El administrador debe tener un botón rápido para cambiar el estado de la sala a "En Mantenimiento", bloqueando reservas futuras hasta su revisión física.

criterio de aceptación 3: El administrador podrá sancionar a usuarios, si la sala queda en mal estado luego de su usp.

## 3. Impacto en requisitos extrafuncionales
Indicar si el cambio altera la prioridad de algún REF o introduce nuevos.
Trazar cambios de prioridad que motiven cambios en decisiones de arquitectura.

| REF ID | Descripción | Prioridad anterior | Prioridad nueva | Cambio / Motivo |
|---|---|---|---|---|
| REF-01 | El sistema debe responder en menos de 2 segundos en operaciones comunes     | Alta      | - | Sin cambio |
| REF-02 | El sistema debe estar disponible al menos un 99% en horario operativo       | Alta      | - | Sin cambio |
| REF-03 | Solo usuarios autenticados pueden reservar, cancelar o modificar reservas   | Alta      | - | Sin cambio |
| REF-04 | La interfaz debe ser simple e intuitiva para estudiantes y administradores  | Alta      | - | Sin cambio |
| REF-05 | El sistema debe implementarse como aplicación web cliente-servidor          | Media     | - | Sin cambio |
| REF-06 | Debe funcionar en diferentes navegadores                                    | Media     | - | Sin cambio |
| REF-07 | El sistema debe ser modular y de bajo acoplamiento                          | Alta      | - | Sin cambio |
| REF-08 | La interfaz debe estar disponible en idioma español                         | Baja      | - | Sin cambio |
| REF-09 | El sistema debe soportar múltiples usuarios concurrentes                    | Media     | - | Sin cambio |
| REF-10 | Los datos de reservas deben mantenerse consistentes en todo momento         | Alta      | - | Sin cambio |
| REF-11 | Solo los administradores puden tener acceso a las cámaras | - | Alta | Nuevo Requisito |
| REF-12 | Mantener todos los modulos bajo 200 ms | - | Alta | Nuevo Requisito |


## 4. Impacto en entidades del dominio
Las nuevas entidades que aparecerán serán la entidad CAMARA

Los atributos que llevará esta entidad Cámara serán:

-Int Id

-String Estado

Además, se agregará un atributo a Sala, esto se debe a que la entidad Cámara esta relacionada con la entidad Sala.

El atributo que se agregará a Sala será el ID_Cámara, para poder identificar que cámara está en cada sala.

Las relaciones que serán afectadas corresponden a la relación del Admin con Salas, que ahora estará vinculada a:
Admin-Cárama-Salas

## 5. Impacto en mockups
[Mockups afectados y descripción de cambios necesarios]
### 1. Panel Admin - Nuevo botón de cámaras:
Hay que agregar un botón de cámaras en el panel principal. Al pulsarlo, debe mostrar todas las salas disponibles. Si seleccionas una, se tiene que abrir una pantalla o modal con el video en vivo de esa cámara.

### 2. Detalle de Reserva:
En esta vista, justo al lado de la pantalla de la cámara, hay que poner la información técnica de la sala (aforo máximo y qué implementos tiene). Ahí mismo tienen que ir los botones de acción rápida para el administrador: "Registrar Incidencia", "Forzar Liberación" y "Mandar a Mantenimiento".


## 6. Impacto en arquitectura

### 6.1 ¿Cambia el estilo arquitectónico?
No, la arquitectura tipo Rest gracias a su flexibilidad permite agregar nuevos módulos, hardware y solo tendrán que ser editadas las partes afectadas directamente (cómo agregar paneles en pantalla del admin)

### 6.2 Relación REF (repriorizado) con decisiones de arquitectura
| REF ID | Prioridad nueva | Decisión de arquitectura que lo aborda |
|---|---|---|
| REF-11 | Alta | El administrador por medio de su panel tendrá acceso a los cambios, esto será manejado |
| REF-12 | Alta | El backend, la base de datos y el sistema de cámaras deben mejorar sus tiempos de respuesta. Por medio de mejorar el rendimiento y conectividad entre los modulos |

## 7. Impacto en módulos
| Módulo | Tipo de impacto | Responsabilidad actualizada | Ofrece a otros (actualizado) |
|---|---|---|---|
| [Módulo existente] | modificado | [descripción actualizada] | [interfaces actualizadas] |
| [Módulo nuevo] | nuevo | [responsabilidad] | [qué expone] |
| [Módulo eliminado] | eliminado | [descripción actualizada responsabilidad] | - |

Fundamentación de cambios modulares:
[Justificar por qué se agregan, modifican o eliminan módulos en función del cambio de requerimientos y/o la repriorización de REF.]

## 8. Nuevas decisiones de diseño
### Decisión 1
Decisión: Implementar nuevas funciones al panel de administrador.

Motivación: Debido a que las salas tienen cámaras, los administradores deben tener acceso a estas, y poder tomar decisiones en base a lo que vigilan. 

Alternativas consideradas: no se consideraron más alternativas, se vio esto como la acción  más óptima.

Impacto: Se modificaron tres módulos y se añade uno nuevo. 

## 9. Trazabilidad actualizada
| Historia | REF relacionado | Módulo | Mockup |
|---|---|---|---|
| US-XX | REF-XX | [módulo] | [ref] |

## 10. Justificación global y trade-offs
El sistema original funcionaba correctamente desde el punto de vista de la gestión de reservas; sin embargo, presentaba una limitación en la práctica, ya que el administrador no tenía visibilidad sobre lo que ocurría dentro de la sala de estudio una vez iniciado el horario reservado.
La incorporación de cámaras permite abordar esta problemática, proporcionando un mecanismo de supervisión que se justifica según lo establecido en las historias de usuario. Esta mejora tiene como objetivo evitar el uso inadecuado o el desperdicio de las salas, resguardar el cumplimiento de las normas, cuidar el espacio físico y asegurar condiciones adecuadas para el siguiente grupo de usuarios
