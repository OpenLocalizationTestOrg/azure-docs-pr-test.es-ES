---
title: "aaaGet a trabajar con un área de trabajo de análisis de registros de Azure | Documentos de Microsoft"
description: "Puede ponerse a trabajar con un área de trabajo de Log Analytics en cuestión de minutos."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 508716de-72d3-4c06-9218-1ede631f23a6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/08/2017
ms.author: magoedte
ms.openlocfilehash: 442a9258a37ee79e8f0b45759ef24b5e3dae0130
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-log-analytics-workspace"></a>Introducción a un área de trabajo de Log Analytics
Puede empezar a usar Azure Log Analytics rápidamente, lo que ayuda a evaluar la inteligencia operativa recopilada desde su infraestructura de TI. Con este artículo, puede comenzar sin problemas a explorar datos que se recopilan *de forma gratuita*, analizarlos y tomar decisiones basadas en ellos.

Este artículo sirve como un análisis mediante un toowalk breve tutorial de introducción tooLog es a través de una implementación mínima de Azure para que puede comenzar a usar el servicio de Hola. contenedor lógico de Hola donde se almacenan los datos de administración de Azure se llama a un área de trabajo. Después de que ha revisado esa información y ha completado su propia evaluación, puede quitar el área de trabajo de evaluación de Hola. Como este artículo es un tutorial, no trata sobre requisitos empresariales, planeamiento ni orientación sobre la arquitectura.

>[!NOTE]
>Si usas Hola nube de Microsoft Azure Government, utilizar [supervisión de la administración pública de Azure + documentación de administración](https://docs.microsoft.com/azure/azure-government/documentation-government-services-monitoringandmanagement#log-analytics) en su lugar.

Este es un vistazo Hola proceso usado tooget iniciado:

![diagrama de proceso](./media/log-analytics-get-started/onboard-oms.png)

## <a name="1-create-an-azure-account-and-sign-in"></a>1 Creación de una cuenta de Azure e inicio de sesión

Si ya no tiene una cuenta de Azure, deberá toocreate un toouse análisis de registros. Puede crear una [cuenta gratuita](https://azure.microsoft.com/free/) que le permita acceder durante 30 días a todos los servicios de Azure.

### <a name="toocreate-a-free-account-and-sign-in"></a>toocreate una cuenta gratuita e iniciar sesión en
1. Siga las instrucciones de hello en [crear su cuenta de Azure gratuita](https://azure.microsoft.com/free/).
2. Vaya toohello [portal de Azure](https://portal.azure.com) e inicie sesión.

## <a name="2-create-a-workspace"></a>2 Creación de un área de trabajo

Hola siguiente paso es toocreate un área de trabajo.

1. Hola portal de Azure, lista de hello de servicios en hello Marketplace de búsqueda para *análisis de registros*y, a continuación, seleccione **análisis de registros**.  
    ![Portal de Azure](./media/log-analytics-get-started/log-analytics-portal.png)
2. Haga clic en **crear**, a continuación, seleccione las opciones correspondientes Hola siguientes elementos:
   * **Área de trabajo de OMS**: escriba un nombre para el área de trabajo.
   * **Suscripción** : si tiene varias suscripciones, elija uno desea tooassociate con la nueva área de trabajo Hola Hola.
   * **Grupos de recursos**
   * **Ubicación**
   * **Plan de tarifa**  
       ![creación rápida](./media/log-analytics-get-started/oms-onboard-quick-create.png)
3. Haga clic en **Aceptar** toosee una lista de las áreas de trabajo.
4. Seleccione un área de trabajo toosee sus detalles en hello portal de Azure.       
    ![detalles de área de trabajo](./media/log-analytics-get-started/oms-onboard-workspace-details.png)         

## <a name="3-upgrade-workspace-toonew-log-search"></a>Búsqueda de registros de área de trabajo de actualización 3 toonew
Se ha publicado un nuevo lenguaje de consulta de análisis de registros y en orden tootake aprovecharlo, deberá tooconvert el área de trabajo.  Si se ha actualizado el área de trabajo se hospeda en el área de hello, verá un banner de color púrpura a través de la parte superior de hello del área de trabajo invitar a tooconvert. actualización de Hello es totalmente voluntaria y no afecta a la experiencia de trabajar con análisis de registros y las soluciones que se agregará.  

Para aún más beneficios de información toounderstand hello, consideraciones y tooupgrade de proceso, consulte [búsqueda de registros de actualización de Azure Log Analytics toonew](log-analytics-log-search-upgrade.md).  

## <a name="4-add-solutions-and-solution-offerings"></a>4 Incorporación de soluciones y ofertas de soluciones

A continuación, agregue soluciones de administración y ofertas de soluciones. Las soluciones de administración son una colección de reglas de lógica, visualización y adquisición de datos que proporcionan métricas que giran en torno a una determinada área de problemas. Una oferta de solución es un conjunto de soluciones de administración.

Agregar área de trabajo de soluciones tooyour permite toocollect de análisis de registros distintos tipos de datos de equipos que están conectados tooyour área de trabajo con agentes. Más adelante, se trata la incorporación de agentes.

### <a name="tooadd-solutions-and-solution-offerings"></a>soluciones de tooadd y ofertas de soluciones

1. En el portal de Azure, haga clic en **New** y, a continuación, en hello **busque en marketplace hello** , escriba **análisis de registros de actividad** y, a continuación, presione ENTRAR.
2. En Hola a todos los elementos hoja, seleccione **análisis de registros de actividad** y, a continuación, haga clic en **crear**.  
    ![Análisis de registros de actividad](./media/log-analytics-get-started/activity-log-analytics.png)  
3. Hola *nombre de la solución de administración* hoja, seleccione un área de trabajo que desee tooassociate con soluciones de administración de Hola.
4. Haga clic en **Crear**.  
    ![área de trabajo de solución](./media/log-analytics-get-started/solution-workspace.png)  
5. Repita los pasos 1 a 4 tooadd:
    - Hola **seguridad y cumplimiento** con soluciones de evaluación de Antimalware y seguridad y auditoría de Hola la oferta de servicio.
    - Hola **Control y automatización** con soluciones de evaluación de actualización del sistema (también denominado Administración de actualizaciones), seguimiento de cambios y Hola Hybrid Worker de automatización de la oferta de servicio. Debe crear una cuenta de automatización cuando se agrega la oferta de solución Hola.  
        ![Cuenta de Automation](./media/log-analytics-get-started/automation-account.png)  
6. Puede ver soluciones de administración de Hola que agregó el área de trabajo de tooyour desplazándose demasiado**análisis de registros** > **suscripciones** > ***denombredeáreadetrabajo***  >  **Introducción**. Se muestran los iconos para soluciones de administración de Hola que agregó.  
    >[!NOTE]
    >Puesto que aún no hemos conectado cualquier área de trabajo de toohello de agentes, no ve ningún dato para soluciones de Hola que agregó.  

    ![iconos de las soluciones sin datos](./media/log-analytics-get-started/solutions-no-data.png)

## <a name="4-create-a-vm-and-onboard-an-agent"></a>4 Creación de una máquina virtual e incorporación de un agente

Ahora, cree una máquina virtual simple en Azure. Después de crear una máquina virtual, tooenable de agente OMS Hola incorporar lo. Habilitar agente de hello inicia la recopilación de datos de hello VM y envía datos tooLog análisis.

### <a name="toocreate-a-virtual-machine"></a>toocreate una máquina virtual

- Siga las instrucciones de hello en [crear la primera máquina virtual de Windows en el portal de Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md) e iniciar la máquina virtual nueva de Hola.

### <a name="connect-hello-virtual-machine-toolog-analytics"></a>Conectar máquina virtual de hello tooLog análisis

- Siga las instrucciones de hello en [tooLog de máquinas virtuales de Azure conectarse análisis](log-analytics-azure-vm-extension.md) tooconnect Hola VM tooLog análisis con Hola portal de Azure.

## <a name="6-view-and-act-on-data"></a>6 Visualización de datos y acciones con ellos

Anteriormente, se habilitó la solución de análisis de registros de actividad de Hola y ofertas de servicio de seguridad y cumplimiento de normas y automatización y Control de Hola. A continuación, se empiezan a examinar los datos recopilados por las soluciones y los resultados de búsquedas de registros.

toostart, vistazo a los datos que se muestran desde dentro de las soluciones. Después, consulte algunas búsquedas de registros a las que se accede desde búsquedas de registros. Búsquedas de registros permiten toocombine y correlacionan datos de varios orígenes en el entorno del equipo. Para obtener más información, consulte [búsquedas de registro de análisis de registros](log-analytics-log-searches.md) o si convierte el lenguaje de consultas nuevo toohello de área de trabajo, consulte [busca en el registro de descripción en análisis de registros](log-analytics-log-search-new.md). 

### <a name="tooview-antimalware-data"></a>tooview datos de Antimalware

1. En la consulta Hola portal de Azure, navegue demasiado**análisis de registros** > ***el área de trabajo***.
2. En la hoja de hello para el área de trabajo, en **General**, haga clic en **Introducción**.  
    ![Información general](./media/log-analytics-get-started/overview.png)
3. Haga clic en hello **evaluación Antimalware** icono. En este ejemplo, puede ver que Windows Defender está instalado en un equipo, pero su firma no está actualizada.  
    ![Antimalware](./media/log-analytics-get-started/solution-antimalware.png)
4. En este ejemplo, en **el estado de protección**, haga clic en **firma no actualizada** tooopen búsqueda de registros y ver los detalles acerca de los equipos de Hola que tienen firmas no está actualizadas. En este ejemplo, tenga en cuenta con el nombre de ese equipo hello *getstarted*. Si hubiera más de un equipo con las firmas no está actualizados, todos aparecerían en hello búsqueda de registros de resultados.  
    ![Antimalware no actualizado](./media/log-analytics-get-started/antimalware-search.png)

### <a name="tooview-security-and-audit-data"></a>tooview datos de seguridad y auditoría

1. En la hoja de hello para el área de trabajo, en **General**, haga clic en **Introducción**.  
2. Haga clic en hello **seguridad y auditoría** icono. En este ejemplo, puede ver que hay dos problemas importantes: a un equipo le faltan actualizaciones críticas y otro carece de protección suficiente.  
    ![Seguridad y auditoría](./media/log-analytics-get-started/security-audit.png)
3. En este ejemplo, en **problemas importantes**, haga clic en **equipos que faltan actualizaciones críticas** tooopen búsqueda de registros y ver los detalles acerca de los equipos que faltan actualizaciones críticas. En este ejemplo, falta una actualización crítica y 63 de otro tipo.  
    ![Búsqueda de registros de Seguridad y auditoría](./media/log-analytics-get-started/security-audit-log-search.png)

### <a name="tooview-and-act-on-system-update-data"></a>tooview y actuar en los datos de la actualización del sistema

1. En la hoja de hello para el área de trabajo, en **General**, haga clic en **Introducción**.  
2. Haga clic en hello **evaluación de actualización del sistema** icono. En este ejemplo, puede ver que hay un equipo Windows llamado *getstarted* que necesita actualizaciones críticas y otro que necesita actualizaciones de definiciones.  
    ![Actualizaciones del sistema](./media/log-analytics-get-started/system-updates.png)
3. En este ejemplo, en **las actualizaciones que faltan**, haga clic en **actualizaciones críticas** tooopen búsqueda de registros y ver los detalles acerca de los equipos que faltan actualizaciones críticas. En este ejemplo, hay una actualización que falta y otra necesaria.  
    ![Búsqueda de registros de Actualizaciones de sistema](./media/log-analytics-get-started/system-updates-log-search.png)
4. Vaya toohello [Operations Management Suite](http://microsoft.com/oms) sitio Web e inicie sesión con su cuenta de Azure. Cuando inicia sesión, observe que la información sobre soluciones de hello es toowhat similar ha verá Hola portal de Azure.  
    ![Portal de OMS](./media/log-analytics-get-started/oms-portal.png)
5. Haga clic en hello **administración de actualizaciones** icono.
6. En el panel de administración de actualización de hello, tenga en cuenta que información de actualización del sistema de hello es toohello actualización del sistema información similar que ha visto en hello portal de Azure. Sin embargo, Hola **administrar implementaciones de actualizaciones** mosaico es nuevo. Haga clic en hello **administrar implementaciones de actualizaciones** icono.  
    ![Icono Administración de actualizaciones](./media/log-analytics-get-started/update-management.png)
7. En hello **actualizar implementaciones** página, haga clic en **agregar** toocreate una *actualización, ejecute*.  
    ![Implementaciones de actualizaciones](./media/log-analytics-get-started/update-management-update-deployments.png)
8.  En hello **nueva implementación de actualización** , escriba un nombre para la implementación de actualizaciones de hello, seleccione tooupdate de equipos (en este ejemplo, *getstarted*), elija una programación y, a continuación, haga clic en **guardar**.  
    ![Nueva implementación](./media/log-analytics-get-started/new-deployment.png)  
    Después de guardar parche de hello, vea Hola programado actualizar.  
    ![actualización programada](./media/log-analytics-get-started/scheduled-update.png)  
    Una vez completada la ejecución de actualización de hello, Hola estado muestra **finalizado**.
    ![actualización finalizada](./media/log-analytics-get-started/completed-update.png)
9. Una vez finalizada la ejecución de actualización de hello, puede ver si Hola ejecutar fue correcta o no y también puede ver detalles acerca de qué actualizaciones aplicarse.

## <a name="after-evaluation"></a>Después de la evaluación

En este tutorial, ha instalado un agente en una máquina virtual y se ha puesto en marcha rápidamente. pasos de Hola que ha seguido eran rápido y sencillo. Sin embargo, la mayoría de las grandes organizaciones y empresas cuentan con infraestructuras de TI locales complejas. Por lo tanto, la recopilación de datos de esos entornos complejos toma diseño y un esfuerzo adicional de tutorial Hola. Revise la información de Hola Hola pasos de la sección pasos siguiente para los artículos de toohelpful de vínculos.

Si lo desea puede quitar el área de trabajo de hello creadas con este tutorial.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo conectar [agentes de Windows](log-analytics-windows-agents.md) tooLog análisis.
* Obtenga información acerca de cómo conectar [agentes de Operations Manager](log-analytics-om-agents.md) tooLog análisis.
* [Adición de soluciones de análisis de registros desde la Galería de soluciones de hello](log-analytics-add-solutions.md) tooadd funcionalidad y recopilar datos.
* Familiarizarse con [búsquedas de registro](log-analytics-log-searches.md) tooview detallada información recopilada por soluciones.
