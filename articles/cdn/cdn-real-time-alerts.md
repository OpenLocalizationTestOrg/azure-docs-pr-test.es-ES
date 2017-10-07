---
title: alertas en tiempo real de aaaAzure CDN | Documentos de Microsoft
description: Alertas en tiempo real en la red CDN de Microsoft Azure. Alertas en tiempo real proporcionan notificaciones sobre el rendimiento de Hola de extremos de hello en el perfil de CDN.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269c90437088bbc41bf899a8c02749e8e6f3006c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a>Alertas en tiempo real en la red CDN de Microsoft Azure
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Información general
En este documento se explican las alertas en tiempo real en la red CDN de Microsoft Azure. Esta funcionalidad proporciona notificaciones en tiempo real sobre el rendimiento de Hola de extremos de hello en el perfil de CDN.  Las alertas de correo o de HTTP se pueden configurar por:

* Ancho de banda
* Códigos de estado
* Estados de la memoria caché
* Conexiones

## <a name="creating-a-real-time-alert"></a>Creación de una alerta en tiempo real
1. Hola [Portal de Azure](https://portal.azure.com), examinar el perfil de CDN tooyour.
   
    ![Hoja del perfil de red CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. En la hoja de perfil CDN Hola, haga clic en hello **administrar** botón.
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    se abre el portal de administración de red CDN Hola.
3. Mantenga el mouse sobre hello **análisis** ficha y, a continuación, mantenga el mouse sobre hello **estadísticas en tiempo real** ventana flotante.  Haga clic en **Real-Time Alerts**(Alertas en tiempo real).
   
    ![Portal de administración de la red CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    se muestra la lista de Hola de las configuraciones de alerta existentes (si existe).
4. Haga clic en hello **Agregar alerta** botón.
   
    ![Botón Add Alert (Agregar alerta)](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    Se muestra un formulario para crear una alerta nueva.
   
    ![Formulario de alerta nueva](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. Si desea que esta alerta toobe activa al hacer clic en **guardar**, comprobar hello **alerta habilitada** casilla de verificación.
6. Escriba un nombre descriptivo para la alerta en hello **nombre** campo.
7. Hola **tipo de medio** lista desplegable, seleccione **objetos grandes de HTTP**.
   
    ![Tipo de medio con objetos HTTP grande seleccionado](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > Debe seleccionar **objetos grandes de HTTP** como hello **tipo de medio**.  Hello otras opciones no se usan por **CDN de Azure de Verizon**.  Error tooselect **objetos grandes de HTTP** hará que la alerta se desencadena toonever.
   > 
   > 
8. Crear un **expresión** toomonitor seleccionando un **métrica**, **operador**, y **desencadenar valor**.
   
   * Para **métrica**, seleccione tipo hello de condición que desee supervisar.  **Mbps de ancho de banda** es la cantidad de Hola de uso de ancho de banda en megabits por segundo.  **Total de conexiones** es número de Hola de tooour de conexiones HTTP simultánea servidores perimetrales.  Para obtener definiciones de saludo diversos estados de memoria caché y códigos de estado, consulte [códigos de estado de memoria caché de CDN de Azure](https://msdn.microsoft.com/library/mt759237.aspx) y [códigos de estado de HTTP de CDN de Azure](https://msdn.microsoft.com/library/mt759238.aspx)
   * **Operador** es Hola operador matemático que establece Hola relación entre la métrica de Hola y el valor de desencadenador de Hola.
   * **Desencadenar valor** es el valor de umbral de Hola que debe cumplirse antes de que se enviará una notificación de.
     
     Hola ejemplo siguiente, expresión Hola que se crearon indica que me gustaría toobe una notificación cuando el número de hello 404 códigos de estado es mayor que 25.
     
     ![Expresión de ejemplo de alerta en tiempo real](./media/cdn-real-time-alerts/cdn-expression.png)
9. Para **intervalo**, escriba la frecuencia con que desea que la expresión Hola evaluada.
10. Hola **que se notifique** lista desplegable, seleccione cuándo desea toobe una notificación cuando hello expresión es verdadera.
    
    * **Condición de inicio** indica que se enviará una notificación cuando Hola especifica primero se detecta la condición.
    * **Condición final** indica que se enviará una notificación cuando Hola especificado ya no se detecta la condición. Solo se puede desencadenar esta notificación después de nuestro sistema de supervisión de red ha detectado que Hola especificado insuficiente.
    * **Continuo** indica que se enviará una notificación cada vez que Hola sistema de supervisión de red detecta Hola especificada condición. Tenga en cuenta esa red Hola supervisión sistema sólo comprobación de una vez por intervalo de hello condición especificada.
    * **Condición inicial y final** indica que se enviará una notificación Hola se detecta la primera vez que Hola condición especificada y una vez más cuando se detecta ya no es la condición de Hola.
11. Si desea tooreceive notificaciones por correo electrónico, active hello **notificar por correo electrónico** casilla de verificación.  
    
    ![Formulario de notificación por correo electrónico](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    Hola **a** , escriba la dirección de correo electrónico de Hola donde desea que las notificaciones envió. Para **asunto** y **cuerpo**, puede dejar predeterminado de Hola o sólo puede personalizar el mensaje de Hola mediante hello **palabras clave disponibles** lista toodynamically insertar datos de alertas cuando se envía el mensaje de bienvenida.
    
    > [!NOTE]
    > Puede probar la notificación por correo electrónico de hello haciendo clic en hello **notificación de prueba** button, pero solo después de que se ha guardado la configuración de alertas de Hola.
    > 
    > 
12. Si desea que registra el servidor web de tooa de toobe de notificaciones, compruebe hello **notificar mediante HTTP Post** casilla de verificación.
    
    ![Formulario de notificación de HTTP Post](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    Hola **dirección Url** , escriba la dirección URL de hello, donde desea que el mensaje de bienvenida HTTP publica. Hola **encabezados** cuadro de texto, escriba Hola HTTP encabezados toobe enviado en la solicitud de saludo.  Para **cuerpo** sólo puede personalizar el mensaje de Hola mediante hello **palabras clave disponibles** lista toodynamically insertar datos de alertas cuando se envía el mensaje de bienvenida.  **Encabezados de** y **cuerpo** predeterminado tooan XML carga similar toohello ejemplo siguiente.
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > Puede probar Hola notificación HTTP Post haciendo clic en hello **notificación de prueba** button, pero solo después de que se ha guardado la configuración de alertas de Hola.
    > 
    > 
13. Haga clic en hello **guardar** botón toosave la configuración de alertas.  Si activó **Alert Enabled** (Alerta habilitada) en el paso 5, la alerta ya está activa.

## <a name="next-steps"></a>Pasos siguientes
* Análisis de [estadísticas en tiempo real en la CDN de Microsoft Azure](cdn-real-time-stats.md)
* Mayor profundización con [Informes de HTTP avanzados en la red CDN de Microsoft Azure](cdn-advanced-http-reports.md)
* Analizar [patrones de uso](cdn-analyze-usage-patterns.md)

