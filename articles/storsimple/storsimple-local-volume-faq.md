---
title: "aaaStorSimple localmente anclado volúmenes preguntas más frecuentes | Documentos de Microsoft"
description: "Proporciona respuestas toofrequently más frecuentes preguntas sobre StorSimple localmente anclado volúmenes."
services: storsimple
documentationcenter: NA
author: manuaery
manager: syadav
editor: 
ms.assetid: 7a2f4b1a-4ac9-4ce1-9359-bd40a9cbbb5d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 1/11/2017
ms.author: manuaery
ms.openlocfilehash: 6a0c742acea836c2b960cb604e4010bcb08c3169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-locally-pinned-volumes-frequently-asked-questions-faq"></a>Volúmenes de StorSimple anclados localmente: preguntas más frecuentes (P+F)
## <a name="overview"></a>Información general
Hola continuación se incluyen preguntas y respuestas que tendrá cuando se crea un volumen de StorSimple anclado localmente, convertir un volumen de tooa anclado localmente de volumen en capas (y viceversa), o copia de seguridad y restaurar un volumen anclado localmente.

Preguntas y respuestas se organizan en las siguientes categorías de Hola

* Creación de un volumen anclado localmente
* Copia de seguridad de un volumen anclado localmente
* Convertir un volumen del volumen en capas tooa anclado localmente
* Restauración de un volumen anclado localmente
* Conmutación por error de un volumen anclado localmente

## <a name="questions-about-creating-a-locally-pinned-volume"></a>Preguntas sobre la creación de un volumen anclado localmente
**P.** ¿Qué es el tamaño máximo de Hola de un volumen anclado localmente que puedo crear en dispositivos serie 8000 de hello?

**Un** en dispositivos que ejecutan StorSimple 8000 Series Update 3.0, puede aprovisionar volúmenes en capas hasta too200 TB en dispositivo 8100 Hola o volúmenes anclados localmente una too8.5 TB. En el dispositivo 8600 mayor de hello, puede aprovisionar volúmenes anclados localmente una too22.5 TB o volúmenes en capas hasta too500 TB.    
En dispositivos que ejecutan StorSimple 8000 Series Update 2.x, puede aprovisionar volúmenes en capas hasta too200 TB en dispositivo Hola 8100 o volúmenes anclados localmente hasta too8 TB. En el dispositivo 8600 mayor de hello, puede aprovisionar volúmenes anclados localmente hasta too20 TB o volúmenes en capas hasta too500 TB.   

**P.** Acaba de actualizar mi tooUpdate de dispositivo 8100 2.0 y cuando intento toocreate un volumen anclado localmente, tamaño máximo posible de hello solo es 6 TB y no 8 TB. ¿Por qué no puedo crear un volumen de 8 TB?

**A** si su dispositivo ejecuta la actualización 2.0, puede aprovisionar volúmenes anclados localmente hasta too8 TB o volúmenes en capas hasta too200 TB en Hola dispositivo 8100. Si el dispositivo ya interconectan volúmenes, espacio de hello disponible para crear un volumen anclado localmente será inferior proporcionalmente a este límite máximo. Por ejemplo, si ya se ha aprovisionado 100 TB de volúmenes en capas en el dispositivo 8100 (que es la mitad de hello en capas capacidad), tamaño máximo de Hola de un volumen local que se puede crear en el dispositivo de hello 8100 será reducido too4 TB (aproximadamente la mitad de máximo de Hello localmente anclados capacidad del volumen).

Dado que espacio local en el dispositivo de hello es hello toohost uso conjunto de volúmenes en capas de trabajo, espacio disponible de Hola para crear un volumen anclado localmente se reduce si dispositivo Hola ha niveles volúmenes. Por el contrario, la creación de un volumen anclado localmente proporcionalmente reduce el espacio disponible de Hola para volúmenes en capas. Hola las tablas siguientes resume la capacidad en niveles disponibles de hello en los dispositivos de hello 8100 y 8600 cuando se crean volúmenes anclados localmente.

####<a name="update-30"></a>Actualización 3.0 
| Capacidad aprovisionada de los volúmenes anclados localmente | Toobe capacidad disponible aprovisionado para volúmenes en capas: 8100 | Toobe capacidad disponible aprovisionado para volúmenes en capas - 8600 |
| --- | --- | --- |
| 0 |200 TB |500 TB |
| 1 TB |176,5 TB |477,8 TB |
| 4 TB |105,9 TB |411,1 TB |
| 8,5 TB |0 TB |311,1 TB |
| 10 TB |N/D |277,8 TB |
| 15 TB |N/D |166,7 TB |
| 22,5 TB |N/D |0 TB |

####<a name="update-2x"></a>Actualización 2.x  
 | Capacidad aprovisionada de los volúmenes anclados localmente | Toobe capacidad disponible aprovisionado para volúmenes en capas: 8100 | Toobe capacidad disponible aprovisionado para volúmenes en capas - 8600 |  
 | --- | --- | --- |  
 | 0 |200 TB |500 TB |  
 | 1 TB |25 TB |475 TB |  
 | 4 TB |100 TB |400 TB |  
 | 8 TB |0 TB |300 TB |  
 | 10 TB |N/A |250 TB |  
 | 15 TB |N/D |125 TB |  
 | 20 TB |N/D |0 TB |   

**P.** ¿Por qué la creación de volúmenes anclados localmente es una operación de larga duración? 

**R.** Los volúmenes anclados localmente tienen un aprovisionamiento denso. espacio de toocreate en Hola niveles locales del dispositivo de hello, algunos datos de volúmenes en capas existentes se pueden insertar toohello en la nube durante el proceso de aprovisionamiento de Hola. Y puesto que esto depende de tamaño de hello del volumen de hello está aprovisionando, los datos existentes en la nube toohello de ancho de banda disponible de hello y dispositivo, Hola tiempo Hola cuidado toocreate que un volumen local puede tener varias horas.

**P.** ¿Durante cuánto tiempo tarda toocreate un volumen anclado localmente?

**R.** Porque son un aprovisionamiento grueso de volúmenes anclados localmente, puede que algunos datos existentes de volúmenes en capas se insertar toohello en la nube durante el proceso de aprovisionamiento de Hola. Por lo tanto, hello toocreate de tiempo que tarda un volumen anclado localmente depende de varios factores, incluidos el tamaño de hello del volumen de hello, Hola datos en el dispositivo y Hola ancho de banda disponible. En un dispositivo recién instalado que no tiene volúmenes, Hola tiempo toocreate un volumen anclado localmente es aproximadamente 10 minutos por terabyte de datos. Sin embargo, la creación de volúmenes locales puede tardar varias horas en función de factores de hello explicados con anterioridad en un dispositivo que está en uso.

**P.** Desea toocreate un volumen anclado localmente. ¿Existen todas las recomendaciones que se necesita toobe en cuenta?

**R.** Los volúmenes anclados localmente son adecuados para las cargas de trabajo que requieran garantías locales de los datos en todo momento y estén latencias toocloud confidenciales. Teniendo en cuenta el uso de los volúmenes locales para cualquiera de las cargas de trabajo, ten en cuenta Hola siguiente:

* Aprovisionan grueso de los volúmenes anclados localmente y crear volúmenes locales afecta al espacio disponible de Hola para volúmenes en capas. Por lo tanto, se recomienda comenzar con los volúmenes de menor tamaño y escalar verticalmente a medida que los requisitos de almacenamiento aumentan.
* El aprovisionamiento de volúmenes locales es una operación larga que podría implicar la inserción de datos existentes de la nube de toohello de volúmenes en capas. Como resultado, puede experimentar un rendimiento reducido en estos volúmenes.
* El aprovisionamiento de los volúmenes locales es una operación que tarda mucho tiempo. tiempo real de Hello implicado depende de varios factores: Hola el tamaño del volumen de saludo se está aprovisionando, datos en el dispositivo y el ancho de banda disponible. Si no se hizo copia de seguridad de la nube de toohello volúmenes existentes, crear el volumen es más lento. Se recomienda tomar instantáneas en la nube de los volúmenes existentes antes de aprovisionar un volumen local.
* Puede convertir los volúmenes de toolocally anclado volúmenes en capas existentes, y esta conversión implica el aprovisionamiento de espacio en el dispositivo de Hola para hello resultante volumen anclado localmente (en suma toobringing hacia abajo de los datos en niveles [Si cualquier] de la nube de Hola). De nuevo, se trata de una operación de larga duración que depende de los factores mencionados anteriormente. Se recomienda que haga una copia su tooconversion anteriores de los volúmenes existentes como proceso de hello sea incluso más lenta si los volúmenes existentes no se copian. El dispositivo también puede experimentar un rendimiento reducido durante este proceso.

Para obtener más información acerca de cómo demasiado[crear un volumen anclado localmente](storsimple-manage-volumes-u2.md#add-a-volume)

**P.** ¿Puedo crear varios volúmenes anclados localmente en hello mismo tiempo?

**R.** Sí, pero los trabajos de creación y expansión de volúmenes anclados localmente se procesarán secuencialmente.

Aprovisionan grueso de los volúmenes anclados localmente y esto requiere la creación de espacio local en el dispositivo de hello (lo que podría ocasionar en los datos existentes de toobe de volúmenes en capas que se insertan en la nube toohello durante el proceso de aprovisionamiento de hello). Por lo tanto, si un trabajo de aprovisionamiento está en curso, otros trabajos de creación de un volumen local se pondrán en cola hasta que el trabajo finalice.

De forma similar, si se expande un volumen local existente o un volumen en capas que se va a convertir tooa localmente había anclado volumen y luego hello creación de un nuevo volumen anclado localmente se pone en cola hasta que se complete la tarea anterior Hola. Al expandir el tamaño de Hola de un volumen anclado localmente implica la expansión de Hola de espacio local existente de Hola para ese volumen. Conversión de un volumen en capas toolocally anclado también implica la creación de hello de espacio local para hello resultante volumen anclado localmente. En estas operaciones, la creación o expansión del espacio local es un trabajo de larga duración.

Estos trabajos se pueden ver en hello **trabajos** página de hello el servicio Administrador de StorSimple de Azure. Hola trabajo que se está procesando activamente es continuamente de actualizar el progreso de hello tooreflect de aprovisionamiento de espacio. Hola restantes trabajos de volumen anclado localmente se marca como en ejecución, pero se ha detenido el progreso y que se seleccionan en orden de Hola se pusieron en cola.

**P.** He eliminado un volumen anclado localmente. ¿Por qué no veo espacio Hola reclame reflejados en el espacio disponible de hello cuando intento toocreate un nuevo volumen? 

**R.** Si elimina un volumen anclado localmente, puede que Hola espacio disponible para nuevos volúmenes no se actualiza inmediatamente. Hola el servicio StorSimple Manager actualiza disponible el espacio local Hola aproximadamente cada hora. Se recomienda que espere una hora antes de probar el nuevo volumen de toocreate Hola.

**P.** ¿Se admiten volúmenes anclados localmente en el dispositivo de hello en la nube?

**R.** No se admiten volúmenes anclados localmente en el dispositivo de nube de hello (8010 y 8020 dispositivos tooas anteriormente que se hace referencia Hola dispositivo virtual StorSimple).

**P.** ¿Puedo usar toocreate de cmdlets de PowerShell de Azure de Hola y administrar volúmenes anclados localmente? 

**R.** No, no puede crear volúmenes anclados localmente mediante los cmdlets de Azure PowerShell (cualquier volumen creado mediante Azure PowerShell será de tipo en capas). Le sugerimos que no utilice toomodify de cmdlets de PowerShell de Azure de hello las propiedades de un volumen anclado localmente, tal y como habrá Hola efecto no deseado de la modificación de hello volumen tipo tootiered.

## <a name="questions-about-backing-up-a-locally-pinned-volume"></a>Preguntas acerca de la copia de seguridad de un volumen anclado localmente
**P.** ¿Son compatibles las instantáneas locales de volúmenes anclados localmente?

**R.** Sí, puede tomar instantáneas locales de sus volúmenes anclados localmente. Sin embargo, se recomienda encarecidamente que hace con regularidad copias de seguridad los volúmenes anclados localmente con tooensure de instantáneas en la nube que sus datos están protegidos en Hola eventualidad de un desastre.

**P.** ¿Existen instrucciones para administrar las instantáneas locales para volúmenes anclados localmente?

**R.** Las instantáneas locales junto con una alta tasa de renovación de datos en hello localmente volumen anclado podría provocar el espacio local en hello dispositivo toobe agotarse rápidamente y dar lugar a datos de volúmenes en capas que se va a insertar en la nube toohello más frecuentes. Por lo tanto, se recomienda que minimizar el número de Hola de instantáneas locales.

**P.** Recibo una alerta que indica que es posible que se invaliden mis instantáneas de volúmenes anclados localmente. ¿Cuándo puede ocurrir?

**R.** Tendrá una frecuencia de las instantáneas locales junto con una alta tasa de renovación de datos en hello localmente volumen anclado puede provocar el espacio local en hello dispositivo toobe agotarse rápidamente. Si se usa mucho los niveles local de hello de dispositivo de hello, puede dar lugar a una interrupción en la nube extendida en el dispositivo de hello llenen y podría producir invalidación de instantáneas de Hola entrantes escrituras toohello volumen (como no hay espacio tooupdate Hola instantáneas toorefer toohello anteriores bloques de datos que se han sobrescrito). En este tipo hello de situación escrituras toohello volumen seguirá toobe sirve, pero las instantáneas locales de hello pueden no ser válidas. No hay ningún impacto tooyour existente instantáneas en la nube.

Advertencia de alerta de Hello es toonotify esta situación puede surgir y garantizar que direcciones Hola mismo de forma puntual revisando las instantáneas locales programa tootake menos frecuentes instantáneas locales o eliminar las instantáneas más antiguas locales que ya no están Obligatorio.

Si se invalidan las instantáneas locales de hello, recibirá una alerta de información que le notifica que se han invalidado las instantáneas locales de Hola para directiva de copia de seguridad específica de hello junto con la lista de Hola de marcas de tiempo de las instantáneas locales Hola invalidados. Estas instantáneas será eliminada automáticamente y ya no será capaz de tooview ellas en hello **catálogos de copia de seguridad** página Hola portal de Azure clásico.

## <a name="questions-about-converting-a-tiered-volume-tooa-locally-pinned-volume"></a>Preguntas sobre cómo convertir un volumen de volumen en capas tooa anclado localmente
**P.** Al convertir un volumen de tooa anclado localmente de volumen en capas estoy observar la algunos lentitud en dispositivo Hola. ¿Por qué ocurre esto? 

**R.** proceso de conversión de Hello implica dos pasos: 

1. Aprovisionamiento de espacio en el dispositivo de Hola para hello pronto-a--convertirá había anclado localmente el volumen.
2. Descargar los datos en niveles de hello en la nube tooensure local garantiza.

Estos dos pasos son largos ejecutando operaciones que dependen de tamaño de hello del volumen de Hola que se va a convertir los datos en el dispositivo de Hola y ancho de banda disponible. Como algunos datos de volúmenes en capas existentes pueden retrasar toohello en la nube como parte del proceso de aprovisionamiento de hello, el dispositivo puede experimentar un rendimiento reducido durante este tiempo. Además, el proceso de conversión de hello puede ser más lento si:

* Los volúmenes existentes todavía no ha realizado ninguna nube toohello; por lo que se recomienda que el tooinitiating anterior una conversión de volúmenes de copia de seguridad.
* Se han aplicado las directivas de limitación de ancho de banda, que podría restringir en la nube Hola ancho de banda disponible toohello; por lo tanto, se recomienda que tener un 40 Mbps dedicada o una nube de toohello de conexión más.
* proceso de conversión de Hello puede tardar varias horas debido toohello varios factores que se ha explicado anteriormente; por lo tanto, se recomienda que lleva a cabo esta operación durante las horas no picos o en un fin de semana tooavoid Hola impacto en los consumidores finales.

Para obtener más información acerca de cómo demasiado[convertir un volumen de volumen en capas tooa anclado localmente](storsimple-manage-volumes-u2.md#change-the-volume-type)

**P.** ¿Puedo cancelar la operación de conversión del volumen de hello?

**R.** No, no se Hola operación de conversión de Hola de cancelar una vez iniciada. Según lo descrito en hello anterior pregunta, ten en cuenta de hello posibles problemas de rendimiento que podría encontrar durante el proceso de Hola y seguir Hola los procedimientos recomendados mencionados anteriormente, cuando planee su conversión.

**P.** Volumen de toomy ¿qué ocurre si se produce un error en la operación de conversión de hello?

**R.** Conversión de un volumen puede producir un error debido a problemas de conectividad de toocloud. dispositivo de Hello finalmente puede dejar el proceso de conversión de hello después de una serie de intentos fallidos de toobring hacia abajo de los datos en niveles de nube de Hola. En este escenario, el tipo de volumen Hola continuará toobe Hola origen volumen tipo anterior tooconversion, y:

* Una alerta crítica será toonotify generado error de conversión de volumen de Hola. Obtener más información sobre [alertas de volúmenes relacionados toolocally anclado](storsimple-manage-alerts.md#locally-pinned-volume-alerts)
* Si va a convertir un volumen en capas tooa anclado localmente, volumen de hello continuará tooexhibit propiedades de un volumen en capas como datos todavía pueden residir en la nube de Hola. Se recomienda que resolver problemas de conectividad de hello y, a continuación, vuelva a intentar la operación de conversión de Hola.
* De forma similar, cuando la conversión de un tooa anclado localmente en niveles de volumen se produce un error, aunque el volumen de Hola se marcará como un volumen anclado localmente, funcionará como un volumen en capas (porque los datos se hayan esparcido toohello nube). Sin embargo, seguirá toooccupy espacio en capas locales hello de dispositivo de Hola. Este espacio no estará disponible para otros volúmenes anclados localmente. Se recomienda que vuelva a intentar esta operación tooensure si la conversión de un volumen Hola está completo y se puede reclamar el espacio local hello en dispositivo Hola.

## <a name="questions-about-restoring-a-locally-pinned-volume"></a>Preguntas sobre la restauración de un volumen anclado localmente
**P.** ¿Los volúmenes anclados localmente se restauran instantáneamente?

**R.** Sí, los volúmenes anclados localmente se restauran al instante. Tan pronto como se extrae información de metadatos de hello para el volumen de hello nube hello como parte de la operación de restauración de hello, volumen de Hola se pone en línea y puede tener acceso a host de Hola. Sin embargo, garantías locales para el volumen de hello datos no estará presentes hasta que todos los datos de saludo se ha descargado de la nube de Hola y es posible que experimente un rendimiento en estos volúmenes durante Hola de restauración de hello reducen.

**P.** ¿Durante cuánto tiempo tarda toorestore un volumen anclado localmente?

**R.** Los volúmenes anclados localmente se restaura al instante y poner en línea tan pronto como se recupera información de metadatos de volumen de Hola de nube hello, mientras los datos de volumen de hello continúan toobe se descargan en segundo plano de Hola. Esta última parte de la operación de restauración de hello--vuelta garantías local Hola Hola datos de volumen: es una operación larga y puede tardar varias horas para todas las toobe de datos de hello vuelva a estar local. Hola tiempo toocomplete Hola mismo depende de varios factores, como el tamaño de Hola de volumen de Hola que se está restaurando y Hola ancho de banda disponible. Si se ha eliminado el volumen original de Hola que se está restaurando, le llevará más tiempo toocreate Hola espacio local Hola dispositivo como parte de la operación de restauración de Hola.

**P.** Necesito toorestore mi existente localmente anclado instantánea más antigua de volumen tooan (realizada cuando se interconectan volumen hello). ¿Volumen de Hola se restaurarán como niveles en este caso?

**R.** No, se restaurará el volumen de Hola como un volumen anclado localmente. Aunque las fechas toohello hora cuando se interconectan volumen hello, durante la restauración de los volúmenes existentes, de la instantánea de hello StorSimple utiliza siempre tipo hello de volumen en disco de hello tal como existe actualmente.

**P.** Extiende recientemente Mi volumen anclado localmente, pero ahora se necesita tiempo de tooa toorestore Hola datos al volumen de hello era más pequeño. ¿Cambiará de tamaño restauración volumen actual de Hola y deberá tamaño de hello tooextend del volumen de hello una vez completada la restauración de hello?

**R.** Sí, restauración de hello cambiará el tamaño de volumen de hello, y deberá tooextend tamaño de Hola de volumen de hello una vez completada la restauración de Hola.

**P.** ¿Puedo cambiar el tipo de Hola de un volumen durante la restauración?

**R.**No, no se puede cambiar el tipo de volumen de Hola durante la restauración.

* Volúmenes que se han eliminado se restauran como tipo hello almacenado en hello instantánea.
* Se restauran los volúmenes existentes en función del tipo actual, independientemente del tipo hello almacenado en hello instantánea (consulte las preguntas toohello dos anteriores).

**P.** Necesito toorestore Mi volumen anclado localmente, pero ha seleccionado un punto incorrecto en la instantánea del tiempo. ¿Puedo cancelar la operación de restauración de hello actual?

**R.** Sí, puede cancelar una operación de restauración en curso. estado de Hola de volumen de Hola se revertirá toohello estado en el inicio de Hola de restauración de Hola. Sin embargo, se perderán las escrituras realizadas toohello volumen durante la restauración de hello en curso.

**P.** Comencé una operación de restauración en uno de mis volúmenes anclados localmente y ahora veo una instantánea de mi catálogo de trabajos pendientes que no he creado. ¿Para qué se usa?

**R.** Se trata de hello temporales de instantánea que se crean la operación de restauración toohello anterior y se utilizan para la reversión en caso de restauración de Hola se cancela o falla. No elimine esta instantánea; se eliminará automáticamente cuando se completa la restauración de Hola. Este comportamiento puede producirse si el trabajo de restauración ha anclado solo localmente volúmenes o una mezcla de volúmenes nivelados y anclados localmente. Si el trabajo de restauración de hello incluye solo los volúmenes en capas, este comportamiento no se producirá.

**P.** ¿Puedo clonar un volumen anclado localmente?

**R.** Sí, puede hacerlo. Sin embargo, el volumen de hello anclado localmente se clonará como un volumen en capas de forma predeterminada. Para obtener más información acerca de cómo demasiado[clonar un volumen anclado localmente](storsimple-clone-volume-u2.md)

## <a name="questions-about-failing-over-a-locally-pinned-volume"></a>Preguntas acerca de la conmutación por error de un volumen anclado localmente
**P.** Necesito toofail en mi dispositivo físico de tooanother de dispositivo. ¿Mis volúmenes anclados localmente realizarán la conmutación por error como anclados localmente o en capas?

**R.** Dependiendo de la versión del software Hola Hola del dispositivo de destino, los volúmenes anclados localmente se conmute por error como:

* Anclado localmente si el dispositivo de destino de Hola está ejecutando StorSimple 8000 series update 2
* En niveles si el dispositivo de destino de Hola está ejecutando StorSimple 8000 serie actualiza 1.x
* En niveles si es de dispositivo de destino de hello aparato de nube de hello (actualización de software versión 2 o actualizar 1.x)

Más información acerca de las [conmutación por error y la recuperación ante desastres de volúmenes anclados localmente en las distintas versiones](storsimple-device-failover-disaster-recovery.md#device-failover-across-software-versions)

**P.** ¿Se restauran los volúmenes anclados localmente al instante durante la recuperación ante desastres?

**R.** Sí, los volúmenes anclados localmente se restauran al instante durante la conmutación por error. Tan pronto como se extrae información de metadatos de hello para el volumen de hello nube hello como parte de la operación de conmutación por error de hello, volumen de Hola se pone en línea en el dispositivo de destino de Hola y puede tener acceso a host de Hola. Mientras tanto, datos de volumen de hello seguirán toodownload en segundo plano de Hola y puede experimentar un rendimiento reducido en estos volúmenes dure Hola Hola conmutación por error.

**P.** Veo que ha completado el trabajo de conmutación por error de hello, ¿cómo puedo comprobar progreso Hola del volumen anclado localmente que se restaura en el dispositivo de destino de Hola?

**R.** Durante una operación de conmutación por error, el trabajo de conmutación por error de Hola se marca como completa una vez que se han restaurado y poner en línea en el dispositivo de destino de hello instantáneamente todos los volúmenes de hello en el conjunto de conmutación por error de Hola. Esto incluye los volúmenes anclados localmente que podrían haber fallado sobre; Sin embargo, garantías locales de los datos de hello sólo estará disponibles cuando se ha descargado todos los datos de hello para el volumen de Hola. Puede realizar un seguimiento de este progreso para cada volumen anclado localmente superados la tecla correspondiente trabajos de restauración de Hola que se crean como parte de la conmutación por error de Hola de supervisión. Estos trabajos de restauración individuales solo se crearán para los volúmenes anclados localmente.

**P.** ¿Puedo cambiar el tipo de Hola de un volumen durante la conmutación por error?

**R.** No, no puede cambiar el tipo de volumen de Hola durante una conmutación por error. Si conmuta por error tooanother físico dispositivo que ejecute actualización de la serie StorSimple 8000 2, volúmenes de hello conmutarán por error basado en tipo de volumen de hello almacenado en hello instantánea. Cuando se conmuta tooany otra versión del dispositivo, consulte la pregunta toohello anterior en el tipo de volumen Hola después de una conmutación por error.

**P.** ¿Se puede conmutar un contenedor de volúmenes con el dispositivo de volúmenes anclados localmente toohello en la nube?

**R.** Sí, puede hacerlo. volúmenes de Hello anclado localmente conmutarán por error como volúmenes en capas. Más información acerca de las [conmutación por error y la recuperación ante desastres de volúmenes anclados localmente en las distintas versiones](storsimple-device-failover-disaster-recovery.md#considerations-for-device-failover)

