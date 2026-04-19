## Catálogo de Requisitos Extrafuncionales

Clasificación según ISO 25010 y tipo de restricción.  
La columna Prioridad refleja la importancia para las decisiones de arquitectura: Alta, Media o Baja.

| ID     | Tipo                         | Descripción                                                                | Prioridad |
|--------|------------------------------|----------------------------------------------------------------------------|-----------|
| REF-01 | Calidad de servicio (Perf.)  | El sistema debe responder en menos de 2 segundos en operaciones comunes    | Alta      |
| REF-02 | Calidad de servicio (Disp.)  | El sistema debe estar disponible al menos un 99% en horario operativo      | Alta      |
| REF-03 | Calidad de servicio (Seg.)   | Solo usuarios autenticados pueden reservar, cancelar o modificar reservas  | Alta      |
| REF-04 | Calidad de servicio (Usab.)  | La interfaz debe ser simple e intuitiva para estudiantes y administradores | Alta      |
| REF-05 | Restricción técnica          | El sistema debe implementarse como aplicación web cliente-servidor         | Media     |
| REF-06 | Restricción técnica          | Debe funcionar en navegadores modernos                                     | Media     |
| REF-07 | Calidad de servicio (Mant.)  | El sistema debe ser modular y de bajo acoplamiento                         | Alta      |
| REF-08 | Otros no funcionales         | La interfaz debe estar disponible en idioma español                        | Baja      |
| REF-09 | Calidad de servicio (Escal.) | El sistema debe soportar múltiples usuarios concurrentes                   | Media     |
| REF-10 | Calidad de servicio (Conf.)  | Los datos de reservas deben mantenerse consistentes en todo momento        | Alta      |

