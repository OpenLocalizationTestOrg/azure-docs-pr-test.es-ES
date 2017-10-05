El trabajo genera un archivo de salida JSON que contiene metadatos de los rostros detectados y de los que se ha realizado seguimiento. Los metadatos incluyen coordenadas que indican tanto la ubicación de los rostros como un número de identificación de rostro, que indica que se realiza un seguimiento de dicha persona. Los números de identificación de cara son propensos a restablecerse en circunstancias en las que la cara de frente se pierde o se superpone en el fotograma, lo que provoca que a algunas personas se les asigne varios identificadores.

La salida JSON incluye los siguientes atributos:

| Elemento | Descripción |
| --- | --- |
| version |Esto se refiere a la versión de la API de vídeo. |
| index | (Se aplica solo a Azure Media Redactor) define el índice del marco del evento actual. |
| timescale |"Tics" por segundo del vídeo. |
| Offset |Se trata de la diferencia de tiempo para las marcas de tiempo. En la versión 1.0 de las API de vídeo, será siempre 0. En los escenarios futuros que se admitan, este valor puede cambiar. |
| framerate |Fotogramas por segundo del vídeo. |
| fragments |Los metadatos se separan en diferentes segmentos denominados fragmentos. Cada fragmento contiene un inicio, una duración, un número de intervalo y eventos. |
| start |La hora de inicio del primer evento, en 'tics'. |
| duration |La longitud del fragmento, en "tics". |
| interval |El intervalo de cada entrada de evento dentro del fragmento, en "tics". |
| events |Cada evento contiene las caras detectadas y seguidas dentro de esa duración de tiempo. Es una matriz de matriz de eventos. La matriz externa representa un intervalo de tiempo. La matriz interna consta de 0 o más eventos que ocurrieron en ese momento en el tiempo. Un corchete vacío significa que no se detectaron caras. |
| id |El identificador de la cara que se sigue. Este número puede cambiar inadvertidamente si una cara deja de detectarse. Una persona determinada debe tener el mismo identificador durante todo el vídeo, pero esto no se puede garantizar debido a las limitaciones en el algoritmo de detección (oclusión, etc.). |
| x, y |Las coordenadas X e Y de la parte superior izquierda del cuadro de límite en una escala normalizada de 0,0 a 1,0. <br/>-Las coordenadas X e Y son relativas siempre a la posición horizontal, por lo que si tiene un vídeo en vertical (o boca a abajo, en el caso de iOS), tendrá que transponer las coordenadas en consecuencia. |
| width, height |El ancho y alto del cuadro de límite de la cara en una escala normalizada de 0,0 a 1,0. |
| facesDetected |Este atributo se encuentra al final de los resultados JSON y resume el número de caras que el algoritmo detectó durante el vídeo. Dado que los identificadores pueden restablecerse inadvertidamente si una cara deja de detectarse (por ejemplo, la cara sale de la pantalla o aparta la vista), este número puede no ser siempre el número real de caras en el vídeo. |

