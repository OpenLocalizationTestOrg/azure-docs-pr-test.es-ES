

| **Identificador de límites** | **Límite** | **Comentarios** |
| --- | --- | --- |
| Capacidad total (incluida la nube) |Hasta too64 TB por dispositivo virtual |Puede producir un error en una matriz vacía del tooanother StorSimple Virtual Array completa. Si intentas toorestore toohello mismo dispositivo, asegúrese de que tiene suficiente espacio en hello dispositivo toocomplete esta operación. Después de que haya excedido 32 TB, no se puede restaurar toohello mismo dispositivo. |
| Número máximo de credenciales de la cuenta de almacenamiento por dispositivo |1 | |
| Número máximo de volúmenes o recursos compartidos |16 | |
| Tamaño mínimo de un recurso compartido en capas |500 GB | |
| Tamaño mínimo de un volumen en capas |500 GB | |
| Tamaño máximo de un recurso compartido en capas |20 TB | |
| Tamaño máximo de un volumen en capas |5 TB | |
| Tamaño mínimo de un recurso compartido anclado localmente |50 GB | |
| Tamaño mínimo de un volumen anclado localmente |50 GB | |
| Tamaño máximo del recurso compartido anclado localmente |2 TB | |
| Tamaño máximo de un volumen anclado localmente |200 GB | |
| Número máximo de conexiones de iSCSI de iniciadores |512 | |
| Número máximo de registros de control de acceso por dispositivo |64 | |
| Número máximo de copias de seguridad retenidas por dispositivo virtual de hello en *.backups* carpeta de servidor de archivos |5 |Esto incluye hello más reciente programadas (generados por la directiva de copia de seguridad de hello predeterminada) y copias de seguridad manuales. |
| Número máximo de copias de seguridad programadas retenida por dispositivo de Hola |55 |30 copias de seguridad diarias<br>12 copias de seguridad mensuales<br>13 copias de seguridad anuales |
| Número máximo de copias de seguridad manuales retenidas por dispositivo de Hola |45 | |
| Número máximo de archivos por recurso compartido en un servidor de archivos |1 millón |Al realizar una restauración de dispositivo, tiempos de restauración de hello son proporcional toonumber de archivos a través de todos los recursos compartidos de hello en dispositivo Hola. |
| Número máximo de archivos por volumen en un servidor iSCSI |1 millón | |
| Número máximo de archivos por matriz virtual |4 millones | |
| Tiempo de recuperación de la restauración |Restauración rápida |Hola se basa en el mapa térmico de Hola y restauración depende de tamaño del volumen Hola.<br>Pueden producirse operaciones de copia de seguridad con una operación de restauración en curso. |

