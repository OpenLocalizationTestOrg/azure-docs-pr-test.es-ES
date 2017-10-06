---
title: aaaView y administrar las alertas de Microsoft Azure StorSimple Virtual Array | Documentos de Microsoft
description: "Describe las condiciones de alerta de StorSimple Virtual Array y gravedad, y cómo toouse hello StorSimple Manager service toomanage alertas."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 97ee25a1-0ec3-4883-9a0a-54b722598462
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0fb5b1b9064f33df1d8fa7ace45f0d72b0a1622
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-alerts-for-hello-storsimple-virtual-array"></a>Use el Administrador de dispositivos de StorSimple toomanage alertas para hello StorSimple Virtual Array

## <a name="overview"></a>Información general

característica de alertas de Hola Hola servicio Administrador de dispositivos de StorSimple proporciona una manera para tooreview y Borrar alertas relacionadas tooStorSimple arreglos de discos virtuales en tiempo real. Puede usar alertas de hello en hello **resumen del servicio** toocentrally hoja supervisar Hola problemas de estado de los arreglos de discos virtuales de StorSimple y Hola solución general de Microsoft Azure StorSimple.

Este tutorial se describe cómo los niveles de gravedad de alerta de notificaciones de alerta de tooconfigure, condiciones de alerta comunes y cómo tooview y realizar un seguimiento de las alertas. Además, incluye alerta referencia rápida de tablas, lo que permite tooquickly localizar una alerta específica y responden según corresponda.

![Página de alertas](./media/storsimple-virtual-array-manage-alerts/alerts1.png)

## <a name="configure-alert-settings"></a>Configurar alertas

Puede elegir si desea que toobe una notificación por correo electrónico de las condiciones de alerta de Hola para cada uno de los arreglos de discos virtuales de StorSimple. Además, puede identificar otros destinatarios de notificación de alerta escribiendo sus direcciones de correo electrónico en hello **destinatarios de correo electrónico adicionales** cuadro, separados por punto y coma.

> [!NOTE]
> Puede escribir un máximo de 20 direcciones de correo electrónico por matriz virtual.


Después de habilitar la notificación de correo electrónico para una matriz virtual, los miembros de la lista de notificaciones de hello recibirán un mensaje de correo electrónico cada vez que se produzca una alerta crítica. mensajes de saludo se enviarán desde  *storsimple-alerts-noreply@mail.windowsazure.com*  y se describe la condición de alerta de Hola. Pueden hacer clic en los destinatarios **Unsubscribe** tooremove por sí mismos desde la lista de notificaciones de correo electrónico de Hola.

#### <a name="tooenable-email-notification-for-alerts"></a>tooenable de notificación de correo electrónico para alertas

1. Vaya tooyour Administrador de dispositivos de StorSimple de servicio y en hello **administración** sección, seleccione y haga clic en **dispositivos**. Seleccione en la lista Hola de dispositivos mostrados y haga clic en el dispositivo.
   
    ![Configuración de alertas](./media/storsimple-virtual-array-manage-alerts/alerts2.png)
2. Esto abrirá hello **configuración** hoja. Hola **configuración de dispositivo** sección, seleccione **General**. Esto abrirá hello **configuración General** hoja.
   
    ![configuración de notificaciones de alerta](./media/storsimple-virtual-array-manage-alerts/alerts4.png)
3. Hola **configuración General** hoja, vaya demasiado**configuración de alerta** sección y establecer Hola siguiente:
   
   1. Hola **Habilitar notificación de correo electrónico** campo, seleccione **Sí**.
   2. Hola **los administradores de servicios de correo electrónico** campo, seleccione **Sí** si desea que el Administrador de servicios de toohave hello y todos los coadministradores reciban las notificaciones de alerta de Hola.
   3. Hola **destinatarios de correo electrónico adicionales** , a continuación, escriba las direcciones de correo electrónico de Hola de todos los demás destinatarios que deben recibir las notificaciones de alerta de Hola. Escriba los nombres en formato de hello  *someone@somewhere.com* . Utilizar direcciones de correo electrónico de hello tooseparate de punto y coma. Puede configurar un máximo de 20 direcciones de correo electrónico por dispositivo virtual.
      
       ![configuración de notificaciones de alerta](./media/storsimple-virtual-array-manage-alerts/alerts6.png)
   4. toosend una notificación de correo electrónico de prueba, haga clic en **enviar correo electrónico de prueba**. Hola servicio Administrador de dispositivos de StorSimple mostrará mensajes de estado mientras reenvía la notificación de prueba de Hola.
      
       ![Correo electrónico de notificación de alertas de prueba enviado](./media/storsimple-virtual-array-manage-alerts/alerts7.png)
      
      > [!NOTE]
      > Si prueba a hello no se enviará el mensaje de notificación, servicio de administrador de dispositivos de StorSimple de hello mostrará un mensaje adecuado. Haga clic en **Aceptar**, espere unos minutos y, a continuación, intente toosend en el mensaje de notificación de prueba.
      > 
      > 
   5. En la parte inferior de Hola de página de hello, haga clic en **guardar** toosave su configuración. Cuando se le pida confirmación, haga clic en **Sí**.
      
      ![Correo electrónico de notificación de alertas de prueba enviado](./media/storsimple-virtual-array-manage-alerts/alerts10.png)

## <a name="common-alert-conditions"></a>Condiciones de alerta comunes

La matriz Virtual de StorSimple genera alertas en gran variedad de tooa de respuesta de condiciones. siguiente Hola es tipos más comunes de Hola de condiciones de alerta:

* **Problemas de conectividad** : estas alertas se producen cuando existen dificultades para transferir datos. Problemas de comunicación pueden producirse durante la transferencia de datos tooand de cuenta de almacenamiento de Azure de Hola o de vencimiento toolack de conectividad entre dispositivos virtuales de Hola y el servicio de administrador de dispositivos de StorSimple Hola. Problemas de comunicación son algunos de hello más difícil toofix porque hay muchísimos puntos de error. Siempre primero debe comprobar que la conectividad de red y acceso a Internet están disponibles antes de continuar en toomore solución avanzada de problemas. Para obtener información sobre los puertos y la configuración del firewall, visite demasiado[requisitos de sistema de StorSimple Virtual Array](storsimple-ova-system-requirements.md). Para obtener ayuda a solucionar el problema, vaya demasiado[solución de problemas con el cmdlet Test-Connection hello](storsimple-troubleshoot-deployment.md).
* **Problemas de rendimiento** : estas alertas se producen cuando el sistema no tiene un rendimiento óptimo, por ejemplo, cuando está sobrecargado.

Además, podría ver toosecurity relacionados de alertas, actualizaciones o errores en el trabajo.

## <a name="alert-severity-levels"></a>Niveles de gravedad de alerta

Las alertas tienen distintos niveles de gravedad, según el impacto de Hola que Hola situación alerta tendrá y Hola necesidad de una alerta de toohello de respuesta. niveles de gravedad de Hello son:

* **Crítico** : esta alerta está en estado de tooa de respuesta que está afectando al rendimiento correcta de saludo del sistema. La acción es tooensure requiere que el servicio de StorSimple de hello no se interrumpe.
* **Advertencia** : esta condición puede convertirse en crítica si no se resuelve. Debe investigar la situación de Hola y realizar cualquier problema de hello tooclear acción requerida.
* **Información** : esta alerta contiene información que puede ser útil para el seguimiento y la administración del sistema.

## <a name="view-and-track-alerts"></a>Ver y realizar un seguimiento de las alertas

hoja de resumen de servicio de administrador de dispositivos de StorSimple de Hello proporciona una vista rápida en el número de Hola de alertas en los dispositivos virtuales, organizadas por nivel de gravedad.

![Panel de alertas](./media/storsimple-virtual-array-manage-alerts/alerts14.png)

Haga clic en Hola Hola de tooopen de nivel de gravedad **alertas** hoja. los resultados de Hello incluyen solo las alertas de Hola que coinciden con ese nivel de gravedad.

![Informe de alertas con ámbito de tipo tooalert](./media/storsimple-virtual-array-manage-alerts/alerts15.png)

Haga clic en una alerta en hello lista tooget obtener más detalles de alerta de hello, incluidos Hola última vez que se emitió la alerta de hello, Hola número de apariciones de alerta de hello en dispositivo hello y alerta de hello acción recomendada tooresolve Hola.

![Lista de alertas y detalles](./media/storsimple-virtual-array-manage-alerts/alerts16.png)

Puede copiar el archivo de texto de tooa de detalles de la alerta de hello si necesita toosend Hola información tooMicrosoft soporte técnico. Una vez haya seguido de la recomendación de Hola y resolver la condición de alerta de hello en local, debe desactivar alerta Hola de lista de Hola. Seleccione la alerta de hello en lista de hello y, a continuación, haga clic en **desactive**. tooclear varias alertas, seleccionadas cada alerta, haga clic en cualquier columna excepto hello **alerta** columna y, a continuación, haga clic en **desactive** después de haber seleccionado todos Hola toobe alertas desactivada.

Al hacer clic en **desactive**, tendrá comentarios de Hola oportunidad tooprovide acerca de la alerta de Hola y pasos de Hola que tardó tooresolve Hola problema. 

![comentarios de alertas](./media/storsimple-virtual-array-manage-alerts/alerts17.png)

Algunos eventos se borrará al sistema de hello si otro evento se desencadena con nueva información. 

## <a name="sort-and-review-alerts"></a>Clasificar y revisar alertas

Hola **alertas** hoja puede mostrar las alertas de too250. Si se ha superado el número de alertas, no todas las alertas se mostrará en la vista predeterminada de Hola. Puede combinar Hola después toocustomize campos qué alertas se muestran:

* **Estado**: puede mostrar alertas **Activas** o **Desactivadas**. Alertas activas se siguen desencadenando en el sistema, mientras que borradas se han bien borrar manualmente por un administrador o mediante programación desactivada porque sistema Hola actualiza la condición de alerta de hello con nueva información.
* **Gravedad** – Puede mostrar las alertas de todos los niveles de gravedad (crítica, advertencia, información), o solo las de determinada gravedad, como las alertas críticas únicamente.
* **Origen** : puede mostrar alertas de todos los orígenes, o limitar toothose de alertas de Hola que proceden de servicio de Hola o uno o todos los dispositivos virtuales de Hola.
* **El intervalo de tiempo** : mediante la especificación de hello **de** y **a** fechas y marcas de tiempo, puede ver las alertas durante Hola período de tiempo que le interesa.

## <a name="alerts-quick-reference"></a>Referencia rápida de alertas

Hola las tablas siguientes enumera algunas de las alertas de StorSimple de Hola que pueden surgir, así como recomendaciones e información adicional cuando sea posible. Alertas de StorSimple Virtual Array se dividen en uno de hello siguientes categorías:

* [Alertas de conectividad de la nube](#cloud-connectivity-alerts)
* [Alertas de configuración](#configuration-alerts)
* [Alertas de errores de trabajo](#job-failure-alerts)
* [Alertas de rendimiento](#performance-alerts)
* [Alertas de seguridad](#security-alerts)
* [Alertas de actualización](#update-alerts)

### <a name="cloud-connectivity-alerts"></a>Alertas de conectividad de la nube

| Texto de la alerta | Evento | Más información / acciones recomendadas |
|:--- |:--- |:--- |
| Dispositivo  *<device name>*  es no conectado toohello en la nube. |Hola con el nombre de dispositivo no puede conectar toohello en la nube. |No se pudo conectar toohello en la nube. Esto puede deberse tooone de siguientes hello:<ul><li>Puede haber un problema con la configuración de red de hello en el dispositivo.</li><li>Puede haber un problema con las credenciales de cuenta de almacenamiento de Hola.</li></ul>Para obtener más información sobre cómo solucionar problemas de conectividad, vaya toohello [IU web local](storsimple-ova-web-ui-admin.md) del dispositivo de Hola. |

### <a name="configuration-alerts"></a>Alertas de configuración

| Texto de la alerta | Evento | Más información / acciones recomendadas |
|:--- |:--- |:--- |
| Configuración del dispositivo virtual local no admitida. |Rendimiento lento. |configuración actual de Hello puede producir una degradación del rendimiento. Asegúrese de que el servidor cumple los requisitos mínimos de configuración de Hola. Para obtener más información, consulte demasiado[StorSimple Virtual Array requisitos](storsimple-ova-system-requirements.md). |
| Se está quedando sin espacio aprovisionado en disco en <*nombre de dispositivo*>. |Advertencia de espacio en disco. |Se está agotando el espacio en disco de aprovisionamiento. toofree espacio, considere la posibilidad de mover las cargas de trabajo tooanother volumen o recurso compartido o eliminar datos. |

### <a name="job-failure-alerts"></a>Alertas de errores de trabajo

| Texto de la alerta | Evento | Más información / acciones recomendadas |
|:--- |:--- |:--- |
| La copia de seguridad de <*nombre de dispositivo*> no se pudo completar. |Error de trabajo de copia de seguridad. |No se pudo crear una copia de seguridad. Tenga en cuenta uno de hello siguientes:<ul><li>Problemas de conectividad podrían evitar operación de copia de seguridad de hello completara correctamente. Asegúrese de que no hay ningún problema de conectividad. Para obtener más información sobre cómo solucionar problemas de conectividad, vaya toohello [IU web local](storsimple-ova-web-ui-admin.md) del dispositivo virtual.</li><li>Ha alcanzado el límite de almacenamiento disponible de Hola. toofree espacio, considere la posibilidad de eliminar las copias de seguridad que ya no son necesarios.</li></ul> Resolver problemas de hello, desactive la alerta de Hola y vuelva a intentar la operación de Hola. |
| No se puedo completar la clonación de  <*nombre de dispositivo*>. |Error de trabajo de clonación. |No se pudo crear una clonación. Tenga en cuenta uno de hello siguientes:<ul><li>La lista de copia de seguridad puede no ser válida. Actualizar Hola lista tooverify sigue siendo válida.</li><li>Problemas de conectividad podrían evitar que una operación de clonación Hola completara correctamente. Asegúrese de que no hay ningún problema de conectividad.</li><li>Ha alcanzado el límite de almacenamiento disponible de Hola. toofree espacio, considere la posibilidad de eliminar las copias de seguridad que ya no son necesarios.</li></ul>Resolver problemas de hello, desactive la alerta de Hola y vuelva a intentar la operación de Hola. |

### <a name="performance-alerts"></a>Alertas de rendimiento

| Texto de la alerta | Evento | Más información / acciones recomendadas |
|:--- |:--- |:--- |
| Observa retrasos inesperados en la transferencia de datos. |Transferencias de datos lenta. |Limitación de errores se produce cuando se superan los objetivos de escalabilidad de Hola de un servicio de almacenamiento. servicio de almacenamiento de Hello tiene este tooensure que ningún inquilino o cliente único puede usar servicio de hello en gastos de Hola de otros usuarios. Para obtener más información sobre cómo solucionar problemas de la cuenta de almacenamiento de Azure, vaya demasiado[supervisar, diagnosticar y solucionar problemas de almacenamiento de Microsoft Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md). |
| Se está agotando el espacio de reserva en disco local en <*nombre de dispositivo*>. |Tiempo de respuesta lento. |total de 10% de hello tamaño aprovisionado para <*nombre de dispositivo*> está reservado en hello dispositivo local y si se encuentra ahora en hello insuficiente espacio reservado. carga de trabajo de Hello en <*nombre de dispositivo*> está generando una mayor tasa de renovación o podría haber migrado recientemente una gran cantidad de datos. Esto puede producir un rendimiento inferior. Considere una de Hola siguientes tooresolve de acciones:<ul><li>Aumentar el dispositivo de toothis de ancho de banda de hello en la nube.</li><li>Reduzca o mueva las cargas de trabajo tooanother volumen o recurso compartido.</li></ul> |

### <a name="security-alerts"></a>Alertas de seguridad

| Texto de la alerta | Evento | Más información / acciones recomendadas |
|:--- |:--- |:--- |
| La contraseña de <*nombre de dispositivo*> expirará en <*número*> días. |Advertencia de contraseña. |Su contraseña expirará en < número> días. Considere la posibilidad de cambiar la contraseña. Para obtener más información, consulte demasiado[contraseña de administrador de dispositivo StorSimple Virtual Array de cambio hello](storsimple-virtual-array-change-device-admin-password.md). |

### <a name="update-alerts"></a>Alertas de actualización

| Texto de la alerta | Evento | Más información / acciones recomendadas |
|:--- |:--- |:--- |
| Hay nuevas actualizaciones disponibles para el dispositivo. |Están disponibles las actualizaciones toohello StorSimple Virtual Array. |Puede instalar nuevas actualizaciones desde hello **mantenimiento** página. |
| No se pudo analizar si hay nuevas actualizaciones en <*nombre de dispositivo*>. |Error de actualización. |Se produjo un error al instalar nuevas actualizaciones. Puede instalar manualmente las actualizaciones de Hola. Si persiste el problema de hello, póngase en contacto con [Microsoft Support](storsimple-contact-microsoft-support.md). |

## <a name="next-steps"></a>Pasos siguientes

* [Obtenga información acerca de hello StorSimple Virtual Array](storsimple-ova-overview.md).

