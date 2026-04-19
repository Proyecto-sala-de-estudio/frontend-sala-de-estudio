## Catálogo de Requisitos Extrafuncionales

Clasificación según ISO 25010 y tipo de restricción.  
La columna Prioridad refleja la importancia para las decisiones de arquitectura: Alta, Media o Baja.

| ID     | Tipo                         | Descripción                                              | Prioridad |
|--------|------------------------------|----------------------------------------------------------|-----------|
| REF-01 | Calidad de servicio (Perf.)  | El sistema debe responder en menos de 2 segundos         | Alta      |
| REF-02 | Calidad de servicio (Disp.)  | Disponibilidad >= 99% en horario operativo               | Alta      |
| REF-03 | Calidad de servicio (Seg.)   | Autenticación obligatoria para realizar reservas         | Alta      |
| REF-04 | Calidad de servicio (Usab.)  | Interfaz simple e intuitiva para el usuario              | Alta      |
| REF-05 | Restricción técnica          | Sistema basado en arquitectura web (cliente-servidor)    | Media     |
| REF-06 | Restricción técnica          | Compatible con navegadores modernos                      | Media     |
| REF-07 | Calidad de servicio (Mant.)  | Sistema modular y de bajo acoplamiento                   | Media     |
| REF-08 | Otros no funcionales         | Interfaz disponible en idioma español                    | Baja      |
| REF-09 | Calidad de servicio (Escal.) | Soportar múltiples usuarios concurrentes                 | Media     |
| REF-10 | Calidad de servicio (Conf.)  | Los datos de reservas deben mantenerse consistentes      | Alta      |
