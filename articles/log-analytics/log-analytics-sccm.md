---
title: "Análisis de Configuration Manager tooLog aaaConnect | Documentos de Microsoft"
description: "Este artículo muestra hello pasos tooconnect tooLog del Administrador de configuración de análisis y empezar a analizar los datos."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f2298bd7-18d7-4371-b24a-7f9f15f06d66
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: dc50ebc46020a806d99d1a3e3d0e91fd09ad2c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-configuration-manager-toolog-analytics"></a>Análisis de Configuration Manager tooLog Connect
Puede conectar System Center Configuration Manager tooLog análisis de datos de colección de dispositivos de toosync OMS. De este modo, los datos de la jerarquía de Configuration Manager estarán disponibles en OMS.

## <a name="prerequisites"></a>Requisitos previos

Log Analytics es compatible con la rama actual de System Center Configuration Manager, versión 1606 y posteriores.  

## <a name="configuration-overview"></a>Información general sobre la configuración
Hola pasos resume Hola proceso tooconnect análisis tooLog de Configuration Manager.  

1. Hola Portal de administración de Azure, registrar Configuration Manager como una aplicación de la aplicación Web o API Web y asegúrese de que tiene Hola cliente y el Id. de clave secreta de cliente en el registro de hello de Azure Active Directory. Vea [usar la aplicación de portal toocreate Active Directory y la entidad de servicio que puede tener acceso a recursos](../azure-resource-manager/resource-group-create-service-principal-portal.md) para obtener información detallada acerca de cómo realizar este paso.
2. En el Portal de administración de Azure, hello [proporcionar Configuration Manager (aplicación web registrado de hello) con permiso tooaccess OMS](#provide-configuration-manager-with-permissions-to-oms).
3. En el Administrador de configuración, [agregar una conexión mediante Hola Asistente para la conexión de OMS de agregar](#add-an-oms-connection-to-configuration-manager).
4. En el Administrador de configuración, [actualizar las propiedades de conexión de hello](#update-oms-connection-properties) clave secreta de hello cliente o la contraseña nunca expira o se pierde.
5. Con información del portal de OMS de hello, [descargar e instalar Microsoft Monitoring Agent hello](#download-and-install-the-agent) en equipo Hola ejecuta conexión de servicio de Configuration Manager Hola punto de rol de sistema de sitio. agente de Hello envía tooOMS de datos de Configuration Manager.
6. En Log Analytics, [importe recopilaciones de Configuration Manager](#import-collections) como grupos de equipos.
7. En Log Analytics, consulte datos de Configuration Manager como [grupos de equipos](log-analytics-computer-groups.md).

Puede leer más acerca de cómo conectar tooOMS de Configuration Manager en [sincronizar los datos de Configuration Manager toohello Microsoft Operations Management Suite](https://technet.microsoft.com/library/mt757374.aspx).

## <a name="provide-configuration-manager-with-permissions-toooms"></a>Proporcione de Configuration Manager con permisos tooOMS
Hello siguiente procedimiento proporciona Hola Portal de administración de Azure con permisos tooaccess OMS. En concreto, debe conceder hello *rol Colaborador* toousers en grupo de recursos de hello en orden tooallow Hola Portal de administración de Azure tooconnect tooOMS de Configuration Manager.

> [!NOTE]
> Debe especificar permisos en OMS para Configuration Manager. En caso contrario, recibirá un mensaje de error cuando se usa el Asistente para configuración de hello en Configuration Manager.
>
>

1. Abra hello [portal de Azure](https://portal.azure.com/) y haga clic en **examinar** > **Log Analytics (OMS)** hoja de tooopen Hola Log Analytics (OMS).  
2. En hello **Log Analytics (OMS)** hoja, haga clic en **agregar** tooopen hello **área de trabajo de OMS** hoja.  
   ![Hoja OMS](./media/log-analytics-sccm/sccm-azure01.png)
3. En hello **área de trabajo de OMS** hoja, proporcionar Hola siguiente información y, a continuación, haga clic en **Aceptar**.

   * **Área de trabajo de OMS**
   * **Suscripción**
   * **Grupos de recursos**
   * **Ubicación**
   * **Plan de tarifa**  
     ![Hoja OMS](./media/log-analytics-sccm/sccm-azure02.png)  

     > [!NOTE]
     > ejemplo de Hola anterior crea un nuevo grupo de recursos. grupo de recursos de Hello es solo usa tooprovide Configuration Manager con el área de trabajo OMS de permisos toohello en este ejemplo.
     >
     >
4. Haga clic en **examinar** > **grupos de recursos** tooopen hello **grupos de recursos** hoja.
5. Hola **grupos de recursos** hoja, haga clic en el grupo de recursos de Hola que haya creado anteriormente hello tooopen &lt;nombre del grupo de recursos&gt; hoja de configuración.  
   ![Hoja de configuración del grupo de recursos](./media/log-analytics-sccm/sccm-azure03.png)
6. Hola &lt;nombre del grupo de recursos&gt; hoja de configuración, haga clic en Hola de Access control (IAM) tooopen &lt;nombre del grupo de recursos&gt; hoja usuarios.  
   ![Hoja de usuarios del grupo de recursos](./media/log-analytics-sccm/sccm-azure04.png)  
7. Hola &lt;nombre del grupo de recursos&gt; hoja de usuarios, haga clic en **agregar** tooopen hello **agregar acceso** hoja.
8. Hola **agregar acceso** hoja, haga clic en **seleccione un rol**y, a continuación, seleccione hello **colaborador** rol.  
   ![Seleccionar un rol](./media/log-analytics-sccm/sccm-azure05.png)  
9. Haga clic en **agregar usuarios**, seleccione el usuario de Configuration Manager de hello, haga clic en **seleccione**y, a continuación, haga clic en **Aceptar**.  
   ![Agregar usuarios](./media/log-analytics-sccm/sccm-azure06.png)  

## <a name="add-an-oms-connection-tooconfiguration-manager"></a>Agregar un tooConfiguration de connection Manager de OMS
En orden tooadd una conexión de OMS, su entorno de Configuration Manager debe tener un [punto de conexión de servicio](https://technet.microsoft.com/library/mt627781.aspx) configurado para el modo en línea.

1. Hola **administración** área de trabajo de Configuration Manager, seleccione **conector de OMS**. Se abrirá hello **agregar Asistente para la conexión a OMS**. Seleccione **Siguiente**.
2. En hello **General** , confirme que ha hecho Hola siguientes acciones y que tiene detalles de cada artículo, a continuación, seleccione **siguiente**.

   1. En Hola Portal de administración de Azure, Configuration Manager se ha registrado como una aplicación de la aplicación Web o API Web y que ha Hola [Id. de cliente en el registro de hello](../active-directory/active-directory-integrating-applications.md).
   2. En el Portal de administración de Azure hello, ha creado una clave secreta de la aplicación para la aplicación registrada hello en Azure Active Directory.  
   3. Hola Portal de administración de Azure, que ha proporcionado la aplicación web registrado de hello con permiso tooaccess OMS.  
      ![Página de conexión tooOMS generales del Asistente](./media/log-analytics-sccm/sccm-console-general01.png)
3. En hello **Azure Active Directory** pantalla, configurar su tooOMS de configuración de conexión, debe proporcionar su **inquilino** , **Id. de cliente** , y **clave secreta de cliente**  , a continuación, seleccione **siguiente**.  
   ![Página de conexión tooOMS Asistente para Azure Active Directory](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)
4. Si esto se logra Hola todos los otros procedimientos correctamente, Hola, a continuación, obtener información acerca de hello **la configuración de conexión de OMS** pantalla aparecerán automáticamente en esta página. Debe aparecer la información de configuración de conexión de Hola para su **suscripción de Azure** , **grupo de recursos de Azure** , y **el área de trabajo de Operations Management Suite**.  
   ![Página de Asistente para la conexión a OMS de conexión tooOMS](./media/log-analytics-sccm/sccm-wizard-configure04.png)
5. Asistente de Hello conecta toohello servicio OMS con información de hello que ha especificado. Seleccione las recopilaciones de dispositivos de Hola que desee toosync con OMS y, a continuación, haga clic en **agregar**.  
   ![Selección de recopilaciones](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)
6. Compruebe la configuración de conexión en hello **resumen** pantalla, a continuación, seleccione **siguiente**. Hola **progreso** pantalla muestra el estado de la conexión de hello, a continuación, debe **completar**.

> [!NOTE]
> Debe conectarse el sitio de nivel superior de toohello OMS en la jerarquía. Si se conecta un sitio primario OMS tooa independiente y, a continuación, agregar un entorno de tooyour de sitio de administración central, podrá tener toodelete y volver a crear la conexión a OMS Hola dentro de la nueva jerarquía de Hola.
>
>

Después de haber vinculado tooOMS de Configuration Manager, puede agregar o quitar colecciones y ver las propiedades de Hola de hello conexión a OMS.

## <a name="update-oms-connection-properties"></a>Actualización de las propiedades de conexión de OMS
Si una clave secreta de cliente o la contraseña nunca expira o se pierde, deberá propiedades de conexión de OMS de toomanually actualización Hola.

1. En el Administrador de configuración, navegue demasiado**servicios en la nube** , a continuación, seleccione **conector de OMS** tooopen hello **propiedades de conexión de OMS** página.
2. En esta página, haga clic en hello **Azure Active Directory** ficha tooview su **inquilino**, **Id. de cliente**, **caducidad de clave secreta de cliente**. **Compruebe** si ha expirado la **clave secreta de cliente**.

## <a name="download-and-install-hello-agent"></a>Descargue e instale el agente de Hola
1. Portal de OMS de hello, [archivo de instalación de agente de Hola de descarga de OMS](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms).
2. Utilice uno de hello siguiendo métodos tooinstall y configurar el agente de hello en equipo de Hola que se ejecuta el rol de sistema del sitio de punto de conexión de hello Configuration Manager service:
   * [Instalación de agentes de hello mediante el programa de instalación](log-analytics-windows-agents.md#install-the-agent-using-setup)
   * [Instalar a agente de hello mediante la línea de comandos de Hola](log-analytics-windows-agents.md#install-the-agent-using-the-command-line)
   * [Instalar a agente de hello con DSC en automatización de Azure](log-analytics-windows-agents.md#install-the-agent-using-dsc-in-azure-automation)

## <a name="import-collections"></a>Importación de recopilaciones
Después de que has agregado una tooConfiguration de connection Manager de OMS e instalado el agente de hello en equipo de hello con conexión de servicio de Configuration Manager de hello punto rol de sistema de sitio, Hola siguiente paso es tooimport colecciones de Configuration Manager en OMS como los grupos de equipos.

Después de la importación está habilitada, se recupera la información de pertenencia a la colección Hola cada tres horas tookeep Hola pertenencias a la colección actuales. Puede elegir toodisable importación en cualquier momento.

1. En el portal de OMS de hello, haga clic en **configuración**.
2. Haga clic en hello **grupos de equipos** ficha y, a continuación, haga clic en hello **SCCM** ficha.
3. Seleccione **Importar pertenencias de la recopilación de Configuration Manager** y, después, haga clic en **Guardar**.  
   ![Grupos de equipos: pestaña SCCM](./media/log-analytics-sccm/sccm-computer-groups01.png)

## <a name="view-data-from-configuration-manager"></a>Visualización de datos de Configuration Manager
Después de que has agregado una tooConfiguration de connection Manager de OMS e instalar a agente de hello en equipo de hello con rol de sistema del sitio de punto de conexión de hello Configuration Manager service, se envían a los datos desde el agente de hello tooOMS. En OMS, las recopilaciones de Configuration Manager aparecen como [grupos de equipos](log-analytics-computer-groups.md). Puede ver los grupos de Hola de hello **Configuration Manager** página en **grupos de equipos** en **configuración**.

Después de Hola se importan las colecciones, puede ver cuántos equipos con pertenencias a la colección se han detectado. También puede ver el número de Hola de colecciones que se han importado.

![Grupos de equipos: pestaña SCCM](./media/log-analytics-sccm/sccm-computer-groups02.png)

Al hacer clic en cualquiera de ellos, se abre de búsqueda, mostrar todo de hello importa grupos o todos los equipos que pertenecen tooeach grupo. Mediante [Búsqueda de registros](log-analytics-log-searches.md), puede iniciar un análisis exhaustivo de datos de Configuration Manager.

## <a name="next-steps"></a>Pasos siguientes
* Use [Log Search](log-analytics-log-searches.md) tooview información detallada sobre los datos de Configuration Manager.
