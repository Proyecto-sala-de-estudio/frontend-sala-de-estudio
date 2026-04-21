## 1. Cambio solicitado
Se requiere agregar un módulo de vigilancia en tiempo real mediante cámaras IP con procesamiento de imagen para detectar ocupación real versus reserva registrada, operando de forma continua.

## 2. Nuevas historias de usuario
### US-XX: [nombre]
Como [actor],
quiero [acción],
para [beneficio].

Criterios de aceptación:
CA1: [descripción]
CA2: [descripción]

### US-XX: [nombre]
Como [actor],
quiero [acción],
para [beneficio].

Criterios de aceptación:
CA1: [descripción]
CA2: [descripción]


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
| REF-01 | [descripción] | Alta | Alta | Sin cambio |
| REF-03 | [descripción] | Media | Alta | El cambio lo hace crítico |
| REF-07 | [nuevo REF derivado del cambio] | - | Alta | Nuevo requisito |

## 4. Impacto en entidades del dominio
[Nuevas entidades, atributos o relaciones afectadas]

## 5. Impacto en mockups
[Mockups afectados y descripción de cambios necesarios]

## 6. Impacto en arquitectura

### 6.1 ¿Cambia el estilo arquitectónico?
[Sí/No]
Justificación:
[Si la repriorización de REF obliga a cambiar el estilo, explicar por qué. Si el estilo se mantiene, justificar que sigue siendo válido frente al cambio.]

### 6.2 Relación REF (repriorizado) con decisiones de arquitectura
| REF ID | Prioridad nueva | Decisión de arquitectura que lo aborda |
|---|---|---|
| REF-03 | Alta | [cambio o confirmación de decisión existente] |
| REF-07 | Alta | [nueva decisión derivada del cambio] |

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
Decisión: [qué se decide]
Motivación: [por qué, referenciando REF repriorizado si aplica]
Alternativas consideradas: [opciones evaluadas]
Impacto: [en qué módulos o REF afecta]

## 9. Trazabilidad actualizada
| Historia | REF relacionado | Módulo | Mockup |
|---|---|---|---|
| US-XX | REF-XX | [módulo] | [ref] |

## 10. Justificación global y trade-offs
[Por qué la solución propuesta es coherente con el sistema. Qué trade-offs se asumieron, especialmente ante cambios de prioridad en REF. Qué se gana y qué se sacrifica con las decisiones tomadas.]
