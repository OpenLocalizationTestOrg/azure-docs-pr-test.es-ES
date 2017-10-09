<!--author=alkohli last changed: 12/15/15-->

| Identificador de límites | Límite | Comentarios |
| --- | --- | --- |
| Número máximo de credenciales de la cuenta de almacenamiento |64 | |
| Número máximo de contenedores de volúmenes |64 | |
| Número máximo de volúmenes |255 | |
| Número máximo de programaciones por plantilla de ancho de banda |168 |Una programación para cada hora, cada día de semana de hello (24 * 7). |
| Tamaño máximo de un volumen en capas en dispositivos físicos |64 TB para 8100 y 8600 |8100 y 8600 son dispositivos físicos. |
| Tamaño máximo de un volumen en capas en dispositivos virtuales de Azure |30 TB para 8010  <br></br> 64 TB para 8020 |8010 y 8020 son dispositivos virtuales de Azure que utilizan el almacenamiento estándar y premium respectivamente. |
| Tamaño máximo de un volumen anclado localmente en dispositivos físicos |9 TB para 8100  <br></br> 24 TB para 8600 |8100 y 8600 son dispositivos físicos. |
| Número máximo de conexiones iSCSI |512 | |
| Número máximo de conexiones de iSCSI de iniciadores |512 | |
| Número máximo de registros de control de acceso por dispositivo |64 | |
| Número máximo de volúmenes por directiva de copia de seguridad |24 | |
| Número máximo de copias de seguridad por directiva de copia de seguridad |64 | |
| Número máximo de programaciones por directiva de copia de seguridad |10 | |
| Número máximo de instantáneas de cualquier tipo que se pueden retener por volumen |256 |Esto incluye las instantáneas locales y en la nube. |
| Número máximo de instantáneas que pueden estar presentes en cualquier dispositivo |10.000 | |
| Número máximo de volúmenes que se pueden procesar en paralelo para copia de seguridad, restauración o clonación |16 |<ul><li>Si hay más de 16 volúmenes, se procesarán secuencialmente a medida que las ranuras de procesamiento estén disponibles.</li><li>Nuevas copias de seguridad de un clonado o un volumen en capas restaurado no puede producirse hasta que finalice la operación de Hola. Sin embargo, para un volumen local, se permiten las copias de seguridad después de hello volumen está en línea.</li></ul> |
| Tiempo de recuperación de la restauración y la clonación |< 2 minutos |<ul><li>volumen de Hello debe ponerse a disposición en dos minutos de operación de restauración o clonación, independientemente del tamaño del volumen Hola.</li><li>rendimiento de volumen de Hello inicialmente puede ser más lento que normal, ya que la mayoría de los datos de Hola y metadatos aún residen en la nube de Hola. Puede aumentar el rendimiento como flujos de datos desde el dispositivo de StorSimple de toohello de hello en la nube.</li><li>Hola tiempo total toodownload metadatos depende de hello tamaño de volumen asignado. Metadatos se trasladan automáticamente a dispositivo de hello en segundo plano de Hola a velocidad de Hola de 5 minutos por cada TB de datos del volumen asignado. Esta velocidad puede verse afectada por la nube de toohello de ancho de banda de Internet.</li><li>Hola restauración o una operación de clonación se ha completado una vez todos los metadatos de hello en dispositivo Hola.</li><li>No se puede realizar operaciones de copia de seguridad hasta que la restauración de Hola o una operación de clonación se ha completado totalmente. |
| Restauración del tiempo de recuperación de volúmenes anclados localmente |< 2 minutos |<ul><li>volumen de Hello debe ponerse a disposición en dos minutos de operación de restauración de hello, independientemente del tamaño del volumen Hola.</li><li>rendimiento de volumen de Hello inicialmente puede ser más lento que normal, ya que la mayoría de los datos de Hola y metadatos aún residen en la nube de Hola. Puede aumentar el rendimiento como flujos de datos desde el dispositivo de StorSimple de toohello de hello en la nube.</li><li>Hola tiempo total toodownload metadatos depende de hello tamaño de volumen asignado. Metadatos se trasladan automáticamente a dispositivo de hello en segundo plano de Hola a velocidad de Hola de 5 minutos por cada TB de datos del volumen asignado. Esta velocidad puede verse afectada por la nube de toohello de ancho de banda de Internet.</li><li>A diferencia de los volúmenes en capas, en caso de hello de volúmenes anclados localmente, también se descargan localmente datos de volumen de hello en dispositivo Hola. operación de restauración de Hello está completa cuando todos los datos de volumen de saludo se ha incluido toohello dispositivo.</li><li>las operaciones de restauración de Hello pueden ser largos y restauración de hello tiempo total toocomplete Hola dependerá de tamaño de Hola de volumen local Hola aprovisionado, el ancho de banda de Internet y Hola los datos en el dispositivo de hello existentes. Se permiten las operaciones de copia de seguridad en el volumen de hello anclado localmente mientras se realiza la operación de restauración de Hola. |
| Disponibilidad de restauración fina |Última conmutación por error | |
| Rendimiento de lectura/escritura de número máximo de clientes (cuando se atiende desde la capa SSD de hello) * |920/720 MB/s con una sola interfaz de red de 10GbE |Seguridad too2x con MPIO y dos interfaces de red. |
| Rendimiento de lectura/escritura de número máximo de clientes (cuando se atiende desde la capa HDD de hello) * |120/250 MB/s | |
| Rendimiento de lectura/escritura de número máximo de clientes (cuando se atiende desde la capa de nube de hello) * |11/41 MB/s |El rendimiento de lectura depende de que los clientes generen y mantengan una profundidad de cola de E/S suficiente. |

&#42; Se midió el rendimiento máximo por tipo de E/S con escenarios de escritura y de lectura del 100%. Es posible que el rendimiento real sea inferior y dependa de las condiciones de la red y de la mezcla de E/S.

