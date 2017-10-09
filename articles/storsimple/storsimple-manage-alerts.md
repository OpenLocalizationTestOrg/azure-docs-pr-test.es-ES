---
title: aaaView y administrar las alertas de StorSimple | Documentos de Microsoft
description: "Describe las condiciones de alerta de StorSimple y gravedad, cómo tooconfigure notificaciones de alerta y cómo toouse hello StorSimple Manager service toomanage alertas."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bee49253-9ac7-4131-95f6-6bf0e72b8438
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/08/2017
ms.author: anbacker
ms.openlocfilehash: d322c88b565606538a3acb61ff939ec1fbe2f3cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-alerts"></a>Usar tooview de servicio de StorSimple Manager hello y administrar las alertas de StorSimple
## <a name="overview"></a>Información general
Hola **alertas** ficha Hola el servicio StorSimple Manager proporciona una manera para tooreview y borrar avisos relacionados con el dispositivo de StorSimple en tiempo real. En esta pestaña, puede supervisar Hola problemas de mantenimiento de los dispositivos de StorSimple centralmente y Hola solución general de Microsoft Azure StorSimple.

Este tutorial describen las condiciones de alerta comunes, niveles de gravedad de alerta y cómo tooconfigure notificaciones de alerta. Además, incluye alerta referencia rápida de tablas, lo que permite tooquickly localizar una alerta específica y responden según corresponda.

![Página de alertas](./media/storsimple-manage-alerts/HCS_AlertsPage.png)

## <a name="common-alert-conditions"></a>Condiciones de alerta comunes
El dispositivo StorSimple genera alertas en gran variedad de tooa de respuesta de condiciones. siguiente Hola es tipos más comunes de Hola de condiciones de alerta:

* **Problemas de hardware** : estas alertas le indican sobre el estado de saludo del hardware. Le permiten saber si son necesarias actualizaciones de firmware, si una interfaz de red tiene problemas o si existe un problema con alguno de sus discos de datos.
* **Problemas de conectividad** : estas alertas se producen cuando existen dificultades para transferir datos. Problemas de comunicación pueden producirse durante la transferencia de datos tooand de cuenta de almacenamiento de Azure de Hola o de vencimiento toolack de conectividad entre los dispositivos de Hola y el servicio StorSimple Manager Hola. Problemas de comunicación son algunos de hello más difícil toofix porque hay muchísimos puntos de error. Siempre primero debe comprobar que la conectividad de red y acceso a Internet están disponibles antes de continuar en toomore solución avanzada de problemas. Para obtener ayuda a solucionar el problema, vaya demasiado[solución de problemas con el cmdlet Test-Connection hello](storsimple-troubleshoot-deployment.md).
* **Problemas de rendimiento** : estas alertas se producen cuando el sistema no tiene un rendimiento óptimo, por ejemplo, cuando está sobrecargado.

Además, podría ver toosecurity relacionados de alertas, actualizaciones o errores en el trabajo.

## <a name="alert-severity-levels"></a>Niveles de gravedad de alerta
Las alertas tienen distintos niveles de gravedad, según el impacto de Hola que Hola situación alerta tendrá y Hola necesidad de una alerta de toohello de respuesta. niveles de gravedad de Hello son:

* **Crítico** : esta alerta está en estado de tooa de respuesta que está afectando al rendimiento correcta de saludo del sistema. La acción es tooensure requiere que el servicio de StorSimple de hello no se interrumpe.
* **Advertencia** : esta condición puede convertirse en crítica si no se resuelve. Debe investigar la situación de Hola y realizar cualquier problema de hello tooclear acción requerida.
* **Información** : esta alerta contiene información que puede ser útil para el seguimiento y la administración del sistema.

## <a name="configure-alert-settings"></a>Configurar alertas
Puede elegir si desea que toobe una notificación por correo electrónico de las condiciones de alerta para cada uno de los dispositivos de StorSimple. Además, puede identificar otros destinatarios de notificación de alerta escribiendo sus direcciones de correo electrónico en hello **otros destinatarios de correo electrónico** cuadro, separados por punto y coma.

> [!NOTE]
> Puede escribir un máximo de 20 direcciones de correo electrónico por dispositivo.
> 
> 

Después de habilitar la notificación de correo electrónico para un dispositivo, los miembros de la lista de notificaciones de hello recibirán un mensaje de correo electrónico cada vez que se produzca una alerta crítica. mensajes de saludo se enviarán desde  *storsimple-alerts-noreply@mail.windowsazure.com*  y se describe la condición de alerta de Hola. Pueden hacer clic en los destinatarios **Unsubscribe** tooremove por sí mismos desde la lista de notificaciones de correo electrónico de Hola.

#### <a name="tooenable-email-notification-of-alerts-for-a-device"></a>notificación de correo electrónico de tooenable de alertas para un dispositivo
1. Vaya demasiado**dispositivos** > **configurar** para dispositivo Hola.
2. En **configuración de alerta**, establecer Hola siguiente:
   
   1. Hola **enviar notificación de correo electrónico** campo, seleccione **Sí**.
   2. Hola **los administradores de servicios de correo electrónico** campo, seleccione **Sí** si desea que el Administrador de servicios de toohave hello y todos los coadministradores reciban las notificaciones de alerta de Hola.
   3. Hola **otros destinatarios de correo electrónico** , a continuación, escriba las direcciones de correo electrónico de Hola de todos los demás destinatarios que deben recibir las notificaciones de alerta de Hola. Escriba los nombres en formato de hello  *someone@somewhere.com* . Utilizar direcciones de correo electrónico de hello tooseparate de punto y coma. Puede configurar un máximo de 20 direcciones de correo electrónico por dispositivo. 
      
       ![Configuración de notificaciones de alerta](./media/storsimple-manage-alerts/AlertNotify.png)
3. toosend una notificación de correo electrónico de prueba, haga clic en icono de flecha de hello siguiente demasiado**enviar correo electrónico de prueba**. Hola el servicio StorSimple Manager mostrará mensajes de estado mientras reenvía la notificación de prueba de Hola. 
4. Cuando hello siguiente mensaje aparezca, haga clic en **Aceptar**. 
   
    ![Correo electrónico de notificación de alertas de prueba enviado](./media/storsimple-manage-alerts/HCS_AlertNotificationConfig3.png)
   
   > [!NOTE]
   > Si hello mensaje de notificación de prueba no se puede enviar, Hola el servicio StorSimple Manager mostrará un mensaje adecuado. Haga clic en **Aceptar**, espere unos minutos y, a continuación, intente toosend en el mensaje de notificación de prueba. 
   > 
   > 

## <a name="view-and-track-alerts"></a>Ver y realizar un seguimiento de las alertas
panel de servicio de StorSimple Manager Hola proporciona una vista rápida en el número de Hola de alertas en los dispositivos, organizadas por nivel de gravedad.

![Panel de alertas](./media/storsimple-manage-alerts/admin_alerts_dashboard.png)

Al hacer clic en el nivel de gravedad de hello abre hello **alertas** resultados de Hola de ficha incluyen solo las alertas de Hola que coinciden con ese nivel de gravedad.

![Informe de alertas con ámbito de tipo tooalert](./media/storsimple-manage-alerts/admin_alerts_scoped.png)

Al hacer clic en una alerta en la lista de hello proporciona detalles adicionales de alerta de hello, incluidos Hola la última hora Hola alerta notificó, Hola número de apariciones de alerta de hello en dispositivo de Hola y Hola recomienda alerta de acción tooresolve Hola. Si se trata de una alerta de hardware, también identificará el componente de hardware Hola.

![Ejemplo de alerta de hardware](./media/storsimple-manage-alerts/admin_alerts_hardware.png)

Puede copiar el archivo de texto de tooa de detalles de la alerta de hello si necesita toosend Hola información tooMicrosoft soporte técnico. Una vez haya seguido de la recomendación de Hola y resolver la condición de alerta de hello en local, debe borrar la alerta de hello de dispositivo de Hola seleccionando alerta Hola Hola **alertas** ficha y haga clic en **borrar**. tooclear varias alertas, seleccionadas cada alerta, haga clic en cualquier columna excepto hello **alerta** columna y, a continuación, haga clic en **desactive** después de haber seleccionado todos Hola toobe alertas desactivada. Tenga en cuenta que algunas alertas se borran automáticamente cuando se resuelve el problema de Hola o al sistema de hello actualizaciones alerta Hola con nueva información.

Al hacer clic en **desactive**, tendrá comentarios de Hola oportunidad tooprovide acerca de la alerta de Hola y pasos de Hola que tardó tooresolve Hola problema. Algunos eventos se borrará al sistema de hello si otro evento se desencadena con nueva información. En ese caso, verá el siguiente mensaje de Hola.

![Borrar mensaje de alerta](./media/storsimple-manage-alerts/admin_alerts_system_clear.png)

## <a name="sort-and-review-alerts"></a>Clasificar y revisar alertas
Quizá le resulte más eficaces informes toorun en alertas para que pueda revisar y anular la selección de grupos. Además, Hola **alertas** ficha puede mostrar las alertas de too250. Si se ha superado el número de alertas, no todas las alertas se mostrará en la vista predeterminada de Hola. Puede combinar Hola después toocustomize campos qué alertas se muestran:

* **Estado**: puede mostrar alertas **Activas** o **Desactivadas**. Alertas activas se siguen desencadenando en el sistema, mientras que borradas se han bien borrar manualmente por un administrador o mediante programación desactivada porque sistema Hola actualiza la condición de alerta de hello con nueva información.
* **Gravedad** – Puede mostrar las alertas de todos los niveles de gravedad (crítica, advertencia, información), o solo las de determinada gravedad, como las alertas críticas únicamente.
* **Origen** : puede mostrar alertas de todos los orígenes, o limitar toothose de alertas de Hola que proceden de servicio de Hola o uno o todos los dispositivos de Hola.
* **El intervalo de tiempo** : mediante la especificación de hello **de** y **a** fechas y marcas de tiempo, puede ver las alertas durante Hola período de tiempo que le interesa.

## <a name="alerts-quick-reference"></a>Referencia rápida de alertas
Hola las tablas siguientes enumera algunas de las alertas de Microsoft Azure StorSimple Hola que pueden surgir, así como recomendaciones e información adicional cuando sea posible. Las alertas de dispositivo de StorSimple se dividen en uno de hello siguientes categorías:

* [Alertas de conectividad de la nube](#cloud-connectivity-alerts)
* [Alertas de clúster](#cluster-alerts)
* [Alertas de recuperación ante desastres](#disaster-recovery-alerts)
* [Alertas de hardware](#hardware-alerts)
* [Alertas de errores de trabajo](#job-failure-alerts)
* [Alertas de volumen anclado localmente](#locally-pinned-volume-alerts)
* [Alertas de red](#networking-alerts)
* [Alertas de rendimiento](#performance-alerts)
* [Alertas de seguridad](#security-alerts)
* [Alertas de paquetes de soporte](#support-package-alerts)

### <a name="cloud-connectivity-alerts"></a>Alertas de conectividad de la nube
| Texto de la alerta | Evento | Más información / acciones recomendadas |
|:--- |:--- |:--- |
| Conectividad demasiado <*nombre de la credencial de nube*> no se puede establecer. |No se puede conectar la cuenta de almacenamiento de toohello. |Parece que podría existir un problema de conectividad con su dispositivo. Vuelva a ejecutar hello `Test-HcsmConnection` cmdlet impide Hola interfaz de Windows PowerShell para StorSimple en su dispositivo tooidentify y corregir el problema de Hola. Si Hola configuración es correcta, el problema de hello podría ser con credenciales de Hola de cuenta de almacenamiento de hello para el que se generó la alerta de Hola. En este caso, utilice hello `Test-HcsStorageAccountCredential` cmdlet toodetermine si existe algún problema que pueda resolver.<ul><li>Compruebe la configuración de red.</li><li>Compruebe las credenciales de la cuenta de almacenamiento.</li></ul> |
| No hemos recibido ningún latido desde el dispositivo para hello última <*número*> minutos. |No se puede conectar toodevice. |Parece que existe un problema de conectividad con su dispositivo. Use hello `Test-HcsmConnection` cmdlet impide Hola interfaz de Windows PowerShell para StorSimple en su dispositivo tooidentify y corrija el problema de Hola o póngase en contacto con el Administrador de red. |

### <a name="storsimple-behavior-when-cloud-connectivity-fails"></a>Comportamiento de StorSimple cuando se produce un error de conectividad de la nube
¿Qué sucede si se produce un error de conectividad de la nube para mi dispositivo StorSimple que se ejecuta en producción?

Si se produce un error en la conectividad de nube en el dispositivo de producción de StorSimple, a continuación, según Hola estado del dispositivo, siguiente Hola puede producirse: 

* **Para los datos locales de hello en el dispositivo**: durante algún tiempo, no habrá interrupción y de lectura seguirán toobe sirve. Sin embargo, tal y como número de Hola de operaciones de E/s pendientes aumenta y excede el límite, lecturas de hello podrían iniciar toofail. 
  
    Según la cantidad de Hola de datos en el dispositivo, Hola escrituras también seguirá toooccur para hello primeras horas después de la interrupción de hello en la conectividad de hello en la nube. escrituras de Hola se ralentice, a continuación e iniciará finalmente toofail si se interrumpe la conectividad de la nube de Hola durante varias horas. (No hay almacenamiento temporal en el dispositivo de Hola para datos que se inserta en la nube toohello de toobe. Esta área se vacía cuando se envían datos de Hola. Si se produce un error de conectividad, datos de esta área de almacenamiento no se insertarán en la nube toohello, y se producirá un error de E/S.)   
* **Para los datos de hello en la nube de Hola**: para la mayoría de los errores de conectividad en la nube, se devuelve un error. Una vez que se restaure la conectividad de hello, IOs Hola se reanudan sin usuario Hola cuyo volumen de Hola de toobring en línea. En raras ocasiones, intervención del usuario puede ser necesario toobring Hola back-volumen en línea de hello portal de Azure clásico. 
* **Para las instantáneas de nube en curso**: Hola operación se reintenta varias veces dentro de 4 a 5 horas y si no se restaura la conectividad de hello, instantáneas en la nube Hola se producirá un error.

### <a name="cluster-alerts"></a>Alertas de clúster
| Texto de la alerta | Evento | Más información / acciones recomendadas |
|:--- |:--- |:--- |
| El dispositivo conmutó demasiado <*nombre de dispositivo*>. |El dispositivo está en modo de mantenimiento. |El dispositivo conmutó debido tooentering o modo de mantenimiento existente. Esto es normal y no se requiere ninguna acción. Una vez reconocida esta alerta, bórrela de la página de alertas de Hola. |
| El dispositivo conmutó demasiado <*nombre de dispositivo*>. |Se actualizó recientemente el firmware o software del dispositivo. |Se ha producido una conmutación por error de clúster debido a tooan update. Esto es normal y no se requiere ninguna acción. Una vez reconocida esta alerta, bórrela de la página de alertas de Hola. |
| El dispositivo conmutó demasiado <*nombre de dispositivo*>. |Se apagó o reinició el controlador. |Dispositivo conmutó por error porque el controlador activo Hola se apaga o reinicia un administrador. No se requiere ninguna acción. Una vez reconocida esta alerta, bórrela de la página de alertas de Hola. |
| El dispositivo conmutó demasiado <*nombre de dispositivo*>. |Conmutación por error planeada. |Verifique que se trató de una conmutación por error planeada. Una vez realizadas las acciones apropiadas, borre esta alerta de la página de alertas de Hola. |
| El dispositivo conmutó demasiado <*nombre de dispositivo*>. |Conmutación por error no planeada. |StorSimple está diseñado tooautomatically recuperar las conmutaciones por error no planeada. Si ve un gran número de estas alertas, póngase en contacto con el soporte técnico de Microsoft. |
| El dispositivo conmutó demasiado <*nombre de dispositivo*>. |Otras causas/causas desconocidas. |Si ve un gran número de estas alertas, póngase en contacto con el soporte técnico de Microsoft. Una vez resuelto el problema de hello, borre esta alerta de la página de alertas de Hola. |
| Un servicio de dispositivo crítico indica un estado error. |Error del servicio de ruta de datos. |Para recibir asistencia, póngase en contacto con el servicio de soporte técnico de Microsoft. |
| La dirección IP virtual de la interfaz de red <*DATA #*> indica un estado de error. |Otras causas/causas desconocidas. |A veces las condiciones temporales pueden causar estas alertas. Si éste es el caso de hello, a continuación, esta alerta se borrará automáticamente más tarde. Si persiste el problema de hello, póngase en contacto con Microsoft Support. |
| La dirección IP virtual de la interfaz de red <*DATA #*> indica un estado de error. |Nombre de la interfaz: <*datos #*> dirección IP <IP address> no se puede poner en conexión porque se ha detectado una dirección IP duplicada en la red de Hola. |Asegúrese de que se quita una dirección IP duplicada Hola de red de Hola o volver a configurar la interfaz de hello con una dirección IP diferente. |

### <a name="disaster-recovery-alerts"></a>Alertas de recuperación ante desastres
| Texto de la alerta | Evento | Más información / acciones recomendadas |
|:--- |:--- |:--- |
| Las operaciones de recuperación no pudieron restaurar todos los valores de hello para este servicio. Los datos de configuración de dispositivo están en un estado incoherente para algunos dispositivos. |Incoherencia de datos detectada después de la recuperación ante desastres. |Los datos cifrados en el servicio de hello no está sincronizados con la en el dispositivo de Hola. Autorizar al dispositivo de Hola <*nombre de dispositivo*> Administrador de StorSimple toostart Hola proceso de sincronización. Hola uso interfaz de Windows PowerShell para StorSimple toorun hello `Restore-HcsmEncryptedServiceData` en dispositivo <*nombre de dispositivo*> cmdlet, proporcionando la contraseña antigua de hello como una entrada toothis perfil de seguridad de cmdlet toorestore Hola. A continuación, ejecute hello `Invoke-HcsmServiceDataEncryptionKeyChange` clave de cifrado de datos de servicio de cmdlet tooupdate Hola. Una vez realizadas las acciones apropiadas, borre esta alerta de la página de alertas de Hola. |

### <a name="hardware-alerts"></a>Alertas de hardware
| Texto de la alerta | Evento | Más información / acciones recomendadas |
|:--- |:--- |:--- |
| El componente de hardware <*id. de componente*> notifica el estado como <*estado*>. | |A veces las condiciones temporales pueden causar estas alertas. Si es el caso, esta alerta se borrará automáticamente después de un tiempo. Si persiste el problema de hello, póngase en contacto con Microsoft Support. |
| Funcionamiento incorrecto del controlador pasivo. |controlador de Hello pasivo (secundario) no funciona. |El dispositivo está operativo, pero uno de los controladores no funciona. Intente reiniciar ese controlador. Si no se resuelve el problema de hello, póngase en contacto con Microsoft Support. |
| Se ha detectado un error de la unidad inminente. | Se ha detectado un error de la unidad inminente. |Hemos detectado un error inminente de la unidad para el componente de hardware de hello ' unidad en ranura <*Id. de ranura*>, alojamiento <*Id. de alojamiento*>'. Considere la posibilidad de sustituir la unidad. <br> Antes de comenzar el reemplazo del disco de hello, revise Hola siguiente información.<br><br>Si el sistema tiene más de un disco defectuoso, no quite más de un SSD o HDD en un determinado momento. Esto puede provocar la pérdida de datos.<br><br>Asegúrese de colocar un SSD de reemplazo en una ranura que previamente contenía un SSD. Hello mismo puede decirse de una unidad de disco duro.<br><br>Las ranuras se numeran de 0 too11. Un disco erróneo en la ranura 2 asigna tooa disco erróneo en la ranura 3 de dispositivo de hello (de hello esquina superior izquierda).<br><br>Para obtener más información sobre el reemplazo del disco, visite toohttps://go.microsoft.com/fwlink/?linkid=838653. Si el problema continúa, póngase en contacto con el soporte técnico de Microsoft a través de https://go.microsoft.com/fwlink/?linkid=838654. |

### <a name="job-failure-alerts"></a>Alertas de errores de trabajo
| Texto de la alerta | Evento | Más información / acciones recomendadas |
|:--- |:--- |:--- |
| Error de copia de seguridad de <*id. de grupo de volúmenes de origen*>. |Error de trabajo de copia de seguridad. |Problemas de conectividad podrían evitar operación de copia de seguridad de hello completara correctamente. Si no hay ningún problema de conectividad, podría haber alcanzado número máximo de Hola de copias de seguridad. Eliminar las copias de seguridad que ya no son necesarios y vuelva a intentar la operación de Hola. Una vez realizadas las acciones apropiadas, borre esta alerta de la página de alertas de Hola. |
| Clonación de <*identificadores de elementos de copia de seguridad de origen*> demasiado <*números de serie del volumen de destino*> error. |Error de trabajo de clonación. |Actualización Hola lista de reserva tooverify que Hola copia de seguridad sigue siendo válida. Si la copia de seguridad de hello es válida, es posible que problemas de conectividad en la nube estén impidiendo una operación de clonación Hola completara correctamente. Si no hay ningún problema de conectividad, podría haber alcanzado el límite de almacenamiento de Hola. Eliminar las copias de seguridad que ya no son necesarios y vuelva a intentar la operación de Hola. Después de haber tomado problema de hello tooresolve las acciones apropiadas, borre esta alerta de la página de alertas de Hola. |
| Error de restauración de <*id. de elemento de copia de seguridad de origen*>. |Error de trabajo de restauración. |Actualización Hola lista de reserva tooverify que Hola copia de seguridad sigue siendo válida. Si la copia de seguridad de hello es válida, es posible que problemas de conectividad en la nube estén impidiendo la operación de restauración de hello completara correctamente. Si no hay ningún problema de conectividad, podría haber alcanzado el límite de almacenamiento de Hola. Eliminar las copias de seguridad que ya no son necesarios y vuelva a intentar la operación de Hola. Después de haber tomado problema de hello tooresolve las acciones apropiadas, borre esta alerta de la página de alertas de Hola. |

### <a name="locally-pinned-volume-alerts"></a>Alertas de volumen anclado localmente
| Texto de la alerta | Evento | Más información / acciones recomendadas |
|:--- |:--- |:--- |
| Error de creación de un volumen local <*nombre de volumen*>. |Error del trabajo de creación de volumen de Hola. <*Toohello correspondiente del mensaje de error no pudo código de error*>. |Problemas de conectividad podrían evitar que la operación de creación de espacio de hello completara correctamente. Aprovisionan grueso de los volúmenes anclados localmente y proceso de Hola de creación de espacio implica verter nube toohello de volúmenes en capas. Si no hay ningún problema de conectividad, es posible que agote el espacio local hello en dispositivo Hola. Determinar si existe espacio en el dispositivo de hello antes de intentar esta operación. |
| Error de expansión del volumen local <*nombre de volumen*>. |Error del trabajo de modificación de volumen de Hello debido demasiado <*toohello correspondiente del mensaje de error no pudo código de error*>. |Problemas de conectividad podrían evitar operación de expansión del volumen de hello completara correctamente. Aprovisionan grueso de los volúmenes anclados localmente y proceso de hello de la extensión de espacio de hello implica verter nube toohello de volúmenes en capas. Si no hay ningún problema de conectividad, es posible que agote el espacio local hello en dispositivo Hola. Determinar si existe espacio en el dispositivo de hello antes de intentar esta operación. |
| Error de conversión de volumen <*nombre de volumen*>. |Error en el tipo de volumen de Hello volumen conversión trabajo tooconvert Hola de tootiered anclado localmente. |No se pudo completar la conversión del volumen de Hola de tootiered tipo anclado localmente. Asegúrese de que no hay ningún problema de conectividad que impidan que Hola realice correctamente. Para solucionar problemas de conectividad problemas vaya demasiado[solución de problemas con el cmdlet Test-HcsmConnection de hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet).<br>volumen anclado localmente original de Hello ahora se ha marcado como un volumen en capas puesto que algunos de los datos de Hola de volumen anclado localmente de hello ha derramado toohello en la nube durante la conversión de Hola. volumen en capas de Hello resultante todavía está ocupando espacio local en el dispositivo para futuras volúmenes locales Hola que no se puede reclamar.<br>Solucione los problemas de conectividad, desactive la alerta de Hola y convertir este tooensure de tipo de volumen anclado localmente original de volumen toohello atrás todos los datos de hello es localmente vuelve a estar disponible. |
| Error de conversión de volumen <*nombre de volumen*>. |no se pudo el tipo de volumen de Hello volumen conversión trabajo tooconvert Hola de toolocally en capas anclado. |No se pudo completar la conversión del volumen de Hola de tipo en capas toolocally anclado. Asegúrese de que no hay ningún problema de conectividad que impidan que Hola realice correctamente. Para solucionar problemas de conectividad problemas vaya demasiado[solución de problemas con el cmdlet Test-HcsmConnection de hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet).<br>ya no se puede reclamar el volumen en capas original Hola ahora se marca como un volumen anclado localmente como parte del proceso de conversión de hello sigue toohave que los datos residen en la nube de hello, mientras Hola un aprovisionamiento grueso de espacio en el dispositivo de Hola para este volumen para futuras local volúmenes con errores.<br>Resuelva los problemas de conectividad, las alertas de Hola desactive y convertir este volumen toohello atrás original volumen en capas tipo tooensure local espacio un aprovisionamiento grueso en dispositivo Hola se puede recuperar. |
| A punto de consumir el espacio local para instantáneas locales de <*nombre del grupo de volúmenes*> |Las instantáneas locales para la directiva de copia de seguridad de hello pronto podrían quedarse sin espacio y ser tooavoid invalidado errores de escritura de host. |Las instantáneas locales frecuentes junto con una alta actividad de datos en volúmenes de hello asociados a este grupo de directivas de copia de seguridad están causando el espacio local en hello dispositivo toobe agotarse rápidamente. Elimine las instantáneas locales que no sean necesarias. Además, actualice las programaciones de copias instantáneas locales para esta tootake de directiva de copia de seguridad menos frecuentes instantáneas locales y asegúrese de que las instantáneas en la nube se realizan con regularidad. Si no se realizan estas acciones, el espacio local para estas instantáneas pronto podría agotarse y configurará automáticamente y de sistema de hello eliminarlas tooensure que las escrituras de host continuar toobe ha procesado correctamente. |
| Las instantáneas locales para <*nombre del grupo de volúmenes*> se han invalidado. |Hola las instantáneas locales para <*nombre grupo de volúmenes*> se han invalidado y, a continuación, eliminar porque superaban el espacio local hello en dispositivo Hola. |tooensure esto no vuelva a ocurrir en hello futuro, revise las programaciones de copias instantáneas locales de Hola para esta directiva de copia de seguridad y elimine las instantáneas locales que ya no son necesarios. Las instantáneas locales frecuentes junto con una alta actividad de datos en volúmenes de hello asociados a este grupo de directivas de copia de seguridad pueden provocar el espacio local en hello dispositivo toobe agotarse rápidamente. |
| Error de restauración de <*id. de elemento de copia de seguridad de origen*>. |Error del trabajo de restauración de Hola. |Si ha anclado localmente o una combinación de volúmenes anclados localmente y en niveles de esta directiva de copia de seguridad, tooverify de lista de reserva de Hola de actualización Hola copia de seguridad sigue siendo válida. Si la copia de seguridad de hello es válida, es posible que problemas de conectividad en la nube estén impidiendo la operación de restauración de hello completara correctamente. Hola localmente anclados volúmenes que se están restaurando como parte de este grupo de instantánea no tiene todos sus dispositivos de toohello descargado de datos y, si tiene una mezcla de volúmenes anclados localmente y en niveles en este grupo de instantáneas, no estarán sincronizadas entre sí. toosuccessfully completar la operación de restauración de hello, realizar los volúmenes de hello en este grupo sin conexión en el host de Hola y vuelva a intentar la operación de restauración de Hola. Tenga en cuenta que el proceso de restauración de los datos de volumen de toohello las modificaciones que se realizaron durante el saludo se perderá. |

### <a name="networking-alerts"></a>Alertas de red
| Texto de la alerta | Evento | Más información / acciones recomendadas |
|:--- |:--- |:--- |
| No se han podido iniciar los servicios de StorSimple. |Error de ruta de datos |Si persiste el problema de hello, póngase en contacto con Microsoft Support. |
| Se ha detectado una dirección IP duplicada para 'Data0'. | |sistema de Hello ha detectado un conflicto de dirección IP '10.0.0.1'. Hola 'Data0' del recurso de red en el dispositivo de hello  *<device1>*  está sin conexión. Asegúrese de que ninguna otra entidad de esta red utilice esta dirección IP. problemas de red tootroubleshoot, vaya demasiado[solución de problemas con el cmdlet Get-NetAdapter hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet). Para resolver este problema, póngase en contacto con el administrador de red. Si persiste el problema de hello, póngase en contacto con Microsoft Support. |
| La dirección IPv4 (o IPv6) para 'Data0' está sin conexión. | |recursos de red de Hello 'Data0' con la dirección IP '10.0.0.1'. el prefijo de longitud '22' en el dispositivo de hello  *<device1>*  está sin conexión. Asegúrese de que toowhich de puertos de conmutador de hello está conectada esta interfaz son operativos. problemas de red tootroubleshoot, vaya demasiado[solución de problemas con el cmdlet Get-NetAdapter hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet). |

### <a name="performance-alerts"></a>Alertas de rendimiento
| Texto de la alerta | Evento | Más información / acciones recomendadas |
|:--- |:--- |:--- |
| Hello carga del dispositivo ha superado <*umbral*>. |Tiempos de respuesta más lentos que lo esperado. |El dispositivo indica su utilización con una carga elevada de entrada/salida. Esto podría provocar el trabajo de toonot dispositivo así como debería. Revise las cargas de trabajo de Hola que atribuidas toohello dispositivo y determine si hay alguna que se puedan mover tooanother dispositivo o que ya no son necesarios.<br>toounderstand Hola estado actual, vaya demasiado[uso Hola toomonitor de servicio de StorSimple Manager el dispositivo](storsimple-monitor-device.md) |

### <a name="security-alerts"></a>Alertas de seguridad
| Texto de la alerta | Evento | Más información / acciones recomendadas |
|:--- |:--- |:--- |
| Se ha iniciado una sesión de soporte técnico de Microsoft Support. |Un tercero ha accedido a la sesión de soporte técnico. |Confirme que este acceso está autorizado. Una vez realizadas las acciones apropiadas, borre esta alerta de la página de alertas de Hola. |
| La contraseña de <*elemento*> caducará en <*período de tiempo*>. |La caducidad está a punto de caducar. |Cambiar la contraseña antes de que caduque. |
| Falta información de la configuración de seguridad para <*id. de elemento*>. | |Hola volúmenes asociados a este contenedor de volumen no puede ser tooreplicate usa la configuración de StorSimple. tooensure que los datos se almacenan de forma segura, se recomienda que elimine contenedor de volúmenes de Hola y los volúmenes asociados con el contenedor de volúmenes de Hola. Una vez realizadas las acciones apropiadas, borre esta alerta de la página de alertas de Hola. |
| <*número*&gt; intentos de inicio de sesión incorrectos para &lt;*id. de elemento*&gt;. |Múltiples intentos de inicio de sesión erróneos. |El dispositivo podría esté siendo atacado o un usuario autorizado está intentando tooconnect con una contraseña incorrecta.<ul><li>Póngase en contacto con los usuarios autorizados y verifique que estos intentos proceden de un origen legítimo. Si continúa toosee gran número de intentos de inicio de sesión fallidos, considere la posibilidad de deshabilitar la administración remota y ponerse en contacto con el Administrador de red. Una vez realizadas las acciones apropiadas, borre esta alerta de la página de alertas de Hola.</li><li>Compruebe que las instancias del Administrador de instantáneas están configuradas con la contraseña correcta de Hola. Una vez realizadas las acciones apropiadas, borre esta alerta de la página de alertas de Hola.</li></ul>Para obtener más información, consulte demasiado[cambiar una contraseña de dispositivo caducada](storsimple-snapshot-manager-manage-devices.md#change-an-expired-device-password). |
| Se han producido uno o más errores al cambiar la clave de cifrado de datos del servicio de Hola. | |Se produjeron errores al cambiar la clave de cifrado de datos del servicio de Hola. Cuando haya abordado condiciones de error de hello, ejecute hello `Invoke-HcsmServiceDataEncryptionKeyChange` cmdlet impide Hola interfaz de Windows PowerShell para StorSimple en su servicio de hello de dispositivo tooupdate. Si el problema persiste, póngase en contacto con el servicio de soporte técnico de Microsoft. Después de resolver el problema de hello, borre esta alerta de la página de alertas de Hola. |

### <a name="support-package-alerts"></a>Alertas de paquetes de soporte
| Texto de la alerta | Evento | Más información / acciones recomendadas |
|:--- |:--- |:--- |
| Error de creación de paquete de soporte técnico. |StorSimple no pudo generar el paquete de saludo. |Vuelva a intentarlo. Si persiste el problema de hello, póngase en contacto con Microsoft Support. Después de resolver el problema de hello, borre esta alerta de la página de alertas de Hola. |

## <a name="next-steps"></a>Pasos siguientes
Aprenda más sobre [los errores de StorSimple y la solución de problemas de un dispositivo operativo](storsimple-troubleshoot-operational-device.md).

