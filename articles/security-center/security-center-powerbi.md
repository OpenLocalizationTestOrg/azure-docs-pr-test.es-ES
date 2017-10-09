---
title: "Visión aaaGet de datos de Azure Security Center con Power BI | Documentos de Microsoft"
description: "Hola paquete de contenido de Azure Security Center Power BI resulta fácil toofind alertas de seguridad, recomendaciones, atacadas recursos y de tendencias, en función de un conjunto de datos que se ha creado para los informes."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 0ded6bc7-52e8-43b4-8940-0bee137526e3
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: af68aef626034fe03d793c36b515a3f26619e5f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-insights-from-azure-security-center-data-with-power-bi"></a>Obtención de información mediante los datos de Azure Security Center con Power BI
Hola [panel de Power BI](http://aka.ms/azure-security-center-power-bi) de Azure Security Center le permite toovisualize, analizar y filtrar las alertas de seguridad desde cualquier lugar, incluido su dispositivo móvil y recomendaciones. Utilice las tendencias tooreveal de panel de Power BI de Hola y ataques patrones - ver alertas de seguridad por recursos o dirección IP de origen y los riesgos de seguridad sin haberse desarrollado por recursos o edad.

También puede mezclar recomendaciones de Security Center y alertas de seguridad con otros datos de diversas maneras, por ejemplo, con los datos de los [registros de auditoría de Azure](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) y la [auditoría de Azure SQL Database](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/). Ambos ofrecen paneles de Power BI y también puede exportar este tooExcel de datos de informes fácil en estado de seguridad de Hola de los recursos de nube.

## <a name="using-azure-security-center-dashboard-tooaccess-power-bi"></a>Uso de Azure Security Center panel tooaccess Power BI
También puede usar informes de Power BI de hello Azure Security Center panel tooaccess. Siga Hola pasos tooperform esta tarea:

1. Hola **Azure Security Center** panel, haga clic en **Power BI** botón.

    ![Conectar el centro de seguridad de tooAzure con Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-1-newUI-2017.png)
2. Hola **Power BI** hoja se abre en el lado derecho de hello tal como se muestra en hello después de pantalla:

    ![Conectar el centro de seguridad de tooAzure con Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new11-2017.png)
3. Si va a crear panel de Power BI de Hola para hello primera vez, puede elegir uno de los siguientes Hola opciones de hello **explorar en Power BI** hoja:

   * **Panel de información de seguridad**: elija esta opción si desea que toocreate un panel que incluye el estado de seguridad, los subprocesos y las detecciones. Se trata de una opción más habitual para el rol de DevOps, cuya responsabilidad es analizar su estado de protección y las alertas detectadas en las suscripciones.
   * **Panel de administración de directivas**: elija esta opción si desea que las directivas de administración y cumplimiento de tooexplore.  Se trata de una opción más habitual para TI central, que se concentra más en el control. Puede usar esta visibilidad de toogain de panel y visión en cumplimiento de la directiva de seguridad a través de su organización.
   * Si ya tiene un panel de Power BI, haga clic en **panel de Power BI actual de Go tooyour**.
4. Para este ejemplo, haga clic en **Panel de información de seguridad** . Si se trata de hello primera vez, está creando un panel de Power BI para que es el centro de seguridad se le pida tooinstall paquete de contenido de Hola. Haga clic en **obtener** botón en hello **paquetes de contenido para Power BI** ventana tal y como se muestra en hello después de pantalla:

    ![Security Insights dashboard (Panel de información de seguridad) de Azure Security Center](./media/security-center-powerbi/security-center-powerbi-fig1-new3.png)
5. Hola **conectar detallada sobre la seguridad de centro de seguridad de tooAzure** aparece la ventana. Asegúrese de hello seguro **autenticación** método es **oAuth2** tal y como se muestra a continuación y haga clic en **iniciar sesión en** botón.

    ![Autenticación](./media/security-center-powerbi/security-center-powerbi-fig1-new4.png)
6. Se le pedirá tooauthenticate nuevo con sus credenciales de Azure. Después de autenticarse, se creará el panel. Una vez que se crea el panel de hello ver un informe con una estructura similar Hola tal como se muestra en hello después de pantalla:

    ![Panel de Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new5.png)

> [!NOTE]
> Una actualización del informe de hello es lugar tootake programada diariamente. En caso de que se produce un error en esta actualización, lea [posibles problemas de actualización con hello Azure Security Center Power BI](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), para obtener más información acerca de cómo tootroubleshoot.
>
>

Aquí puede ver el número de Hola de alertas de seguridad y recomendaciones, así como número de Hola de máquinas virtuales, las bases de datos SQL Azure y recursos de red supervisados por el centro de seguridad de Azure.

Un centro de seguridad de vínculo tooAzure redirige toohello portal de Azure. gráficos de Hello hacen que sea fácil toovisualize información acerca de las recomendaciones de seguridad y las alertas, incluidas:

* Estado de seguridad de los recursos
* Recomendaciones pendientes
* Recomendaciones de máquina virtual
* Alertas a lo largo del tiempo
* Recursos atacados
* Direcciones IP atacadas

Detrás de cada gráfico hay información adicional. Seleccione un icono toosee obtener más información. Por ejemplo, hello **estado de seguridad de recursos** mosaico muestra detalles adicionales sobre pendientes recomendaciones por recursos como se muestra en hello después de pantalla:

![Recomendaciones](./media/security-center-powerbi/security-center-powerbi-fig1-new6.png)

Si hace clic en cualquier línea de este gráfico, hello otros usuarios van toogray out y usted se centra únicamente en hello que elemento seleccionado. tooreturn toohello panel, haga clic en **Azure Security Center** en hello **paneles** opción en el panel izquierdo de Hola de esta página.

> [!NOTE]
> Si desea que toocustomize sus informes agregando campos adicionales o cambiar los objetos visuales existentes, puede editar el informe de Hola. Lea el artículo [Interacción con un informe en la vista de edición en Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) para más información.
>
>

Hola **alertas con el tiempo, recursos atacadas** y **IP atacante** mosaicos tendrán un resultado similar Hola al hacer clic en cada uno de ellos del mismo. Esto sucede porque el informe de hello agrega información sobre esas tres variables y lo llama **recursos siendo atacado** tal como se muestra en hello después de pantalla:

![Resources under Attack](./media/security-center-powerbi/security-center-powerbi-fig1-new7.png)

En este momento puede también guardar una copia de este informe, imprimirlo o publicar en web Hola con hello las opciones disponibles en hello **archivo** menú.

![Menú Archivo](./media/security-center-powerbi/security-center-powerbi-fig8.png)

## <a name="exploring-your-azure-security-center-data-with-power-bi-services"></a>Exploración de los datos de Azure Security Center con los servicios de Power BI
Conectar toohello [Power BI Content Pack Services](https://msit.powerbi.com/groups/me/getdata/services) en Power BI y ejecute hello pasos:

1. Hola **paquete de contenido para Power BI** ventana verá dos opciones tal y como se muestra a continuación.

    ![Content Pack for Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new.png)

   > [!NOTE]
   > Si ya ha ejecutado primera parte de este artículo de hello verá sólo una opción, que es la administración de directivas de centro de seguridad de Azure.
   >
   >
2. A fin de Hola de este ejemplo, haga clic en **obtener** en hello **administración de directivas de centro de seguridad de Azure** icono.
3. Hola **conectar tooAzure administración de directivas de seguridad Center** (ventana), asegúrese de que tooselect **oAuth2** en **método de autenticación** drop hacia abajo, tal y como se muestra a continuación y haga clic en **Iniciar sesión en** botón.

    ![Ventana Administración de directivas](./media/security-center-powerbi/security-center-powerbi-fig1-new8.png)
4. Es posible que la página de autenticación tooan redirigida donde debe escribir las credenciales de Hola que está usando el centro de seguridad de tooconnect tooAzure. Una vez completado el proceso de autenticación de hello, Power BI se iniciará la importación de datos toobuild los informes. Durante este tiempo, puede ver Hola siguiente mensaje en la esquina derecha del saludo del explorador:

    ![Conectar el centro de seguridad de tooAzure con Power BI](./media/security-center-powerbi/security-center-powerbi-fig4.png)

   > [!NOTE]
   > Cuando el panel de Hola se crea para hello primera vez puede tardar más de lo habitual, principalmente para escenarios donde tiene varias suscripciones.
   >
   >
5. Una vez que finalice el proceso de hello, el panel de Azure Security Center Power BI se cargará con hello **administración de directivas de** informes toohello similar que se muestra a continuación:

    ![Panel de administración de directivas](./media/security-center-powerbi/security-center-powerbi-fig1-new9.png)

## <a name="see-also"></a>Otras referencias
En este documento, se habrá aprendido cómo toouse Power BI en el centro de seguridad de Azure. toolearn más información acerca del centro de seguridad de Azure, vea Hola recursos siguientes:

* [Guía de operaciones de planificación de Azure Security Center e](security-center-planning-and-operations-guide.md) : más información cómo tooplan adopción de centro de seguridad de Azure.
* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : más información cómo tooconfigure configuración de seguridad en el centro de seguridad de Azure
* [Toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md) : más información cómo toomanage y que responden las alertas de toosecurity
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.
