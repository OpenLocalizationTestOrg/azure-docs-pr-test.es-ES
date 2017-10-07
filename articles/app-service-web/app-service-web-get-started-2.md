---
title: "funcionalidad aaaAdd tooyour primera aplicación de web | Documentos de Microsoft"
description: "Agregar características muy atractivas tooyour primer web app en unos minutos."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 542671c2-22f0-4f20-8b4b-fa477264c492
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2016
ms.author: cephalin
ms.openlocfilehash: 46c9b118c2c188508cb0a369c691a79073b7d7b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-functionality-tooyour-first-web-app"></a>Agregar funcionalidad tooyour la primera aplicación de web
En [implementar su primer tooAzure de aplicación web en cinco minutos](app-service-web-get-started-dotnet.md), ha implementado una aplicación web de ejemplo en [servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md). En este artículo, rápidamente, podrá agregar algunas aplicaciones de web excelentes funcionalidades tooyour implementado. En unos minutos, aprenderá a:

* aplicar autenticación para los usuarios
* escalar la aplicación automáticamente
* recibir alertas sobre el rendimiento de saludo de la aplicación

Independientemente de qué aplicación de ejemplo que se ha implementado en el artículo anterior de hello, puede seguir a lo largo de tutorial Hola.

Hola tres actividades en este tutorial son solo algunos ejemplos de Hola muchas características útiles que se obtiene al poner la aplicación web en el servicio de aplicaciones. Muchas de las características de hello están disponibles en hello **libre** capa (que es lo que la primera aplicación web se está quedando), y se puede usar el tootry créditos prueba las características que requieren los niveles de precios superior. Tener la certeza de que la aplicación web permanece en **libre** nivel a menos que se cambie de forma explícita tooa diferente de nivel de precios.

> [!NOTE]
> aplicación web de Hello creadas con CLI de Azure se ejecuta en **libre** nivel, lo que permite solo una instancia compartida de máquina virtual con las cuotas de recursos. Para más información sobre lo que se obtiene con el nivel **Gratis** , consulte [Límites de Servicio de aplicaciones](../azure-subscription-service-limits.md#app-service-limits).
> 
> 

## <a name="authenticate-your-users"></a>Autenticación de los usuarios
Ahora, veamos lo fácil que es la aplicación de tooadd authentication tooyour (obtener más información en [autenticación/autorización del servicio de aplicación](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)).

1. En la hoja de portal de hello para la aplicación, que se acaba de abrir, haga clic en **configuración** > **autenticación / autorización**.  
    ![Autenticar, hoja de configuración](./media/app-service-web-get-started/aad-login-settings.png)
2. Haga clic en **en** tooturn en la autenticación.  
3. En **Proveedores de autenticación**, haga clic en **Azure Active Directory**.  
    ![Autenticar, seleccionar Azure AD](./media/app-service-web-get-started/aad-login-config.png)
4. Hola **configuración de Azure Active Directory** hoja, haga clic en **Express**, a continuación, haga clic en **Aceptar**. Hello configuración predeterminada de crea una nueva aplicación de Azure AD en el directorio predeterminado.  
    ![Autenticar, configuración rápida](./media/app-service-web-get-started/aad-login-express.png)
5. Haga clic en **Guardar**.  
    ![Autenticar, guardar configuración](./media/app-service-web-get-started/aad-login-save.png)
   
    Una vez que el cambio de hello es correcta, verá campana de notificación de hello cambiar a verde, junto con un mensaje descriptivo.
6. En la hoja de portal de saludo de la aplicación, haga clic en hello **URL** vínculo (o **examinar** en la barra de menús de hello). vínculo de Hello es una dirección HTTP.  
    ![Autenticar - examinar tooURL](./media/app-service-web-get-started/aad-login-browse-click.png)  
    Pero una vez que se abre la aplicación hello en una nueva pestaña, Hola redireccionamientos de direcciones URL cuadro varias veces y finaliza en la aplicación con una dirección HTTPS. Lo que ve es que ya está iniciado en tooyour suscripción de Azure y automáticamente está autenticado en la aplicación hello.  
    ![Autenticar, sesión iniciada](./media/app-service-web-get-started/aad-login-browse-http-postclick.png)  
    Por lo que si ahora abre una sesión sin autenticar en un explorador diferente, verá una pantalla de inicio de sesión al navegar toohello misma dirección URL.  
    <!-- ![Authenticate - login page](./media/app-service-web-get-started/aad-login-browse.png)  -->
    Si nunca ha utilizado Azure Active Directory, es posible que el directorio predeterminado no tenga usuarios de Azure AD. En ese caso, probablemente única cuenta de hello ahí es Hola cuenta Microsoft con su suscripción de Azure. Que se razón por la que se hubiera iniciado automáticamente en la aplicación toohello en Hola mismo explorador anteriormente.
    En esta página de inicio de sesión también puede usar ese mismo toolog de cuenta de Microsoft en.

Enhorabuena, se autentican todos los tráfico tooyour web app.

Quizás haya observado en hello **autenticación / autorización** hoja que puede hacer mucho más, como:

* Habilitar el inicio de sesión social
* Habilitar varias opciones de inicio de sesión
* Cambiar el comportamiento predeterminado de Hola cuando personas desplace tooyour aplicación por primera vez

Servicio de aplicaciones proporciona que una solución preparada para algunos de autenticación común de hello necesita por lo que no necesita lógica de autenticación de tooprovide Hola.
Para más información, consulte [Expanding App Service Authentication/Authorization](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)(Expansión de autorización y autenticación en el Servicio de aplicaciones).

## <a name="scale-your-app-automatically-based-on-demand"></a>Escalado automático de la aplicación según la demanda
Después, vamos a escalado automático la aplicación, por lo que TI automáticamente ajustará capacidad toorespond toouser petición (obtener más información en [escalar la aplicación en Azure](web-sites-scale.md) y [escalar el recuento de instancias de forma manual o automática](../monitoring-and-diagnostics/insights-how-to-scale.md)).

Brevemente, la aplicación web se escala de dos maneras:

* [Escalado vertical](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): obtenga más CPU, memoria, espacio en disco y características adicionales como máquinas virtuales dedicadas, dominios y certificados personalizados, ranuras de almacenamiento provisional, escalado automático y mucho más. Escalar verticalmente cambiando Hola tarifa del plan de servicio de aplicaciones al que pertenece la aplicación.
* [Escalar horizontalmente](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): aumentar Hola número de instancias de máquina virtual que ejecuta la aplicación.
  Puede escalar horizontalmente tooas muchas como 50 instancias, según el nivel de precios.

Sin más rodeos, vamos a configurar el escalado automático.

1. En primer lugar, vamos a escalar verticalmente tooenable Autoescala. En la hoja de portal de saludo de la aplicación, haga clic en **configuración** > **escalar vertical (Plan de servicio de aplicaciones)**.  
    ![Escalado vertical, hoja de configuración](./media/app-service-web-get-started/scale-up-settings.png)
2. Desplácese y seleccione hello **S1 estándar** nivel, Hola nivel más bajo que admite el escalado automático (dentro de un círculo en captura de pantalla), haga clic en **seleccione**.  
    ![Escalado vertical, elegir nivel](./media/app-service-web-get-started/scale-up-select.png)
   
    Ya ha terminado con el escalado vertical.
   
   > [!IMPORTANT]
   > Este nivel gastará los créditos de la evaluación gratuita. Si tiene una cuenta de pago por uso, incurre en cuenta tooyour de cargos.
   > 
   > 
3. A continuación, vamos a configurar el escalado automático. En la hoja de portal de saludo de la aplicación, haga clic en **configuración** > **horizontalmente (Plan de servicio de aplicaciones)**.  
    ![Escalado horizontal, hoja de configuración](./media/app-service-web-get-started/scale-out-settings.png)
4. Cambio **escalar** demasiado**porcentaje de CPU**. controles deslizantes de Hello debajo de la lista desplegable de hello actualizan en consecuencia. A continuación, defina un intervalo de **Instancias** entre **1** y **2**, y un **Rango objetivo** entre**40** y **80**. Puede hacerlo escribiendo en los cuadros de Hola o mover los controles deslizantes de Hola.  
    ![Escalado horizontal, configurar el escalado automático.](./media/app-service-web-get-started/scale-out-configure.png)
   
    Según esta configuración, la aplicación se escalará horizontalmente de forma automática cuando el uso de CPU sea superior al 80 % y se reducirá horizontalmente cuando el uso de CPU sea inferior al 40 %.
5. Haga clic en **guardar** en la barra de menús de Hola.

Enhorabuena, su aplicación ya escala automáticamente.

Quizás haya observado en hello **configuración de escalado** hoja que puede hacer mucho más, como:

* Escalar manualmente tooa número específico de instancias
* Escalar por otras métricas de rendimiento, como la cola de disco o el porcentaje de memoria
* Personalizar el comportamiento de escalado cuando se desencadena una regla de rendimiento
* Escalado automático según una programación
* Establecer el comportamiento del escalado automático para un evento futuro

Para más información sobre el escalado vertical de su aplicación, consulte [Escalado de una aplicación web en el Servicio de aplicaciones de Azure](web-sites-scale.md). Para más información sobre el escalado horizontal, consulte [Escalado manual o automático del número de instancias](../monitoring-and-diagnostics/insights-how-to-scale.md).

## <a name="receive-alerts-for-your-app"></a>Recepción de alertas para su aplicación
Ahora que la aplicación esté escalado automático, ¿qué ocurre cuando alcanza el número máximo de instancias de hello (2) y CPU sea superior al uso deseado (80%)?
Puede configurar una alerta (obtener más información en [recibir notificaciones de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)) tooinform de esta situación, por lo que puede escala arriba/horizontalmente su aplicación, por ejemplo. Vamos a configurar rápidamente una alerta para este escenario.

1. En la hoja de portal de saludo de la aplicación, haga clic en **herramientas** > **alertas**.  
    ![Alertas, hoja de configuración](./media/app-service-web-get-started/alert-settings.png)
2. Haga clic en **Agregar alerta**. A continuación, en hello **recursos** cuadro recursos seleccione Hola que termina por **(granjas)**. Ese es el plan del Servicio de aplicaciones.  
    ![Alertas, agregar alerta para plan de App Service](./media/app-service-web-get-started/alert-add.png)
3. Especifique **Nombre** como `CPU Maxed`, **Métrica** como **Porcentaje de CPU** y **Umbral** como `90`; después, seleccione **Lectores, colaboradores y propietarios de correo electrónico** y haga clic en **Aceptar**.   
    ![Alertas, configurar alertas](./media/app-service-web-get-started/alert-configure.png)
   
    Cuando Azure termine de crear la alerta de hello, lo verá en hello **alertas** hoja.  
    ![Alertas, vista terminada](./media/app-service-web-get-started/alert-done.png)

Enhorabuena, ya recibe alertas.

Esta configuración de alertas comprobará el uso de la CPU cada cinco minutos. Si esa cifra supera el 90 %, se le enviará una alerta por correo electrónico, además a otras personas que estén autorizadas. toosee todos los usuarios que está autorizado tooreceive Hola alertas, vaya copia toohello hoja portal de la aplicación y haga clic en hello **acceso** botón.  
![Ver quién recibe las alertas](./media/app-service-web-get-started/alert-rbac.png)

Debería ver que **los administradores de suscripciones** ya están hello **propietario** de aplicación hello. Este grupo incluiría si eres administrador de la cuenta de hello de su suscripción de Azure (p. ej. su suscripción de prueba). Para más información sobre el control de acceso basado en rol de Azure, consulte [Uso de asignaciones de roles para administrar el acceso a los recursos de Azure Active Directory](../active-directory/role-based-access-control-configure.md).

> [!NOTE]
> Las reglas de alerta son una característica de Azure. Para más información, consulte [Recibir notificaciones de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).
> 
> 

## <a name="next-steps"></a>Pasos siguientes
En su hello tooconfigure de manera alerta, es podrán que haya observado un amplio conjunto de herramientas de hello **herramientas** hoja. En este caso, puede solucionar problemas, supervisar el rendimiento, pruebas en busca de vulnerabilidades, administrar recursos, interactuar con la consola de VM de Hola y agregar extensiones útiles. Le invitamos a tooclick en cada uno de estos toodiscover Hola sencilla pero eficaz de las herramientas a su alcance.

Obtener información sobre cómo toodo más con la aplicación implementada. Esta es una lista parcial:

* [Compre y configure un nombre de dominio personalizado](custom-dns-web-site-buydomains-web-app.md) : compre un dominio atractivo para la aplicación web en lugar del dominio *.azurewebsites.net. También puede usar un dominio que ya tenga.
* [Configurar entornos de ensayo](web-sites-staged-publishing.md) -implementar su tooa aplicación dirección URL de almacenamiento provisional antes de llevarla a producción. Actualice la aplicación web activa con confianza. Configure una solución de DevOps elaborada con varias ranuras de implementación.
* [Configure la implementación continua](app-service-continuous-deployment.md) : integre la implementación de la aplicación en el sistema de control de código fuente. Impleméntela en Azure con cada confirmación.
* [Acceda a recursos locales](web-sites-hybrid-connection-get-started.md) : acceda a una base de datos local existente o un sistema CRM.
* [Haga una copia de seguridad de la aplicación](web-sites-backup.md) : configure la copia de seguridad y la restauración para la aplicación web. Prepárese para errores inesperados y recupérese de ellos.
* [Habilitar los registros de diagnóstico](web-sites-enable-diagnostic-log.md) -Hola lectura IIS los registros de los seguimientos de Azure o de la aplicación. Léalos en una transmisión, descárguelos o pórtelos a [Application Insights](../application-insights/app-insights-overview.md) para realizar un análisis "llave en mano".
* [Detecte vulnerabilidades en la aplicación](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/)-
  Examine la aplicación web en busca de amenazas modernas con el servicio que proporciona [Tinfoil Security](https://www.tinfoilsecurity.com/).
* [Ejecute trabajos en segundo plano](../azure-functions/functions-overview.md) : ejecute trabajos de procesamiento de datos, informes, etc.
* [Obtener información acerca de cómo funciona el Servicio de aplicaciones](../app-service/app-service-how-works-readme.md)

