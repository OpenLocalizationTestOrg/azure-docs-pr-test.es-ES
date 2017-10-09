trabajo de Hello genera un archivo de salida JSON que contiene metadatos sobre caras detectadas y de seguimiento. los metadatos de Hello incluyen coordenadas que indica la ubicación de Hola de caras, así como una cara Id. número que indica Hola seguimiento de ese individuo. Números de Id. de cara son propensas a tooreset en circunstancias cuando cara frontal Hola se pierde o superpuesta en el marco de hello, lo que da lugar a algunas personas al asignarse a varios identificadores.

Hola de salida que JSON incluye Hola siguientes atributos:

| Elemento | Descripción |
| --- | --- |
| versión |Esto refiere toohello versión de hello API de vídeo. |
| index | (Se aplica tooAzure Redactor de medios) define Hola marco índice del evento actual Hola. |
| timescale |"Tics" de vídeo de Hola por segundo. |
| Offset |Se trata de desplazamiento de hora de Hola para las marcas de tiempo. En la versión 1.0 de las API de vídeo, será siempre 0. En los escenarios futuros que se admitan, este valor puede cambiar. |
| framerate |Fotogramas por segundo de hello vídeo. |
| fragments |metadatos de Hello está fragmentado seguridad en diferentes segmentos denominados fragmentos. Cada fragmento contiene un inicio, una duración, un número de intervalo y eventos. |
| start |Hola hora de inicio del primer evento de hello en 'tics'. |
| duration |longitud de Hola de fragmento de hello, en "tics". |
| interval |intervalo de saludo de cada entrada de eventos dentro de fragmento de hello, en "tics". |
| events |Cada evento contiene caras de hello detectado y realizar un seguimiento dentro de ese período de tiempo. Es una matriz de matriz de eventos. matriz de Hello externo representa un intervalo de tiempo. matriz interna de Hello consta de 0 o más eventos que ocurrieron en ese momento en el tiempo. Un corchete vacío significa que no se detectaron caras. |
| id |Id. de Hola de cara de Hola que realiza el seguimiento. Este número puede cambiar inadvertidamente si una cara deja de detectarse. Una persona determinada debería tener Hola mismo identificador a lo largo de hello general de vídeo, pero esto no se puede garantizar due toolimitations en el algoritmo de detección de hello (oclusión, etcetera). |
| x, y |parte superior izquierda de Hello X y coordenadas de Hola se enfrentan a cuadro de límite en una escala normalizada de too1.0 0,0. <br/>-X e Y coordenadas relativa toolandscape siempre son, por lo que si tiene un retrato de vídeo (o boca abajo, en caso de hello de iOS), tendrá tootranspose Hola coordenadas en consecuencia. |
| width, height |Hola ancho y alto de cara de hello rectángulo de selección en una escala normalizada de too1.0 0,0. |
| facesDetected |Esto se encuentra al final de Hola de resultados JSON de Hola y resume número Hola de caras ese algoritmo Hola detectado durante el saludo de vídeo. Dado que se puede restablecer accidentalmente Hola identificadores si una cara pasa a ser no detectada (p. ej. cara sale fuera de la pantalla, parece ausente), este número puede no siempre igual número real de Hola de caras en vídeo de Hola. |

