---
title: "aaa empezar a trabajar con automatización de Azure | Documentos de Microsoft"
description: "Este artículo proporciona información general del servicio de automatización de Azure de revisar los detalles de diseño e implementación de Hola Hola tooonboard de preparación de la oferta de Azure Marketplace."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 434e8ea28c55ff9bda1d2e46a7a6b8378a3baa0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation"></a>Introducción a Azure Automation

Esta guía de introducción presenta los principales conceptos relacionados toohello implementación de la automatización de Azure. Si tooAutomation nuevo en Azure o que tenga experiencia con el software de flujo de trabajo de automatización como System Center Orchestrator, esta guía le ayudará a entender cómo tooprepare y automatización de la incorporación.  Después, estará preparado toobegin runbooks para admitir las necesidades de automatización del proceso de desarrollo. 


## <a name="automation-architecture-overview"></a>Información general sobre la arquitectura de Automation

![Información general sobre Automatización de Azure](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Automatización de Azure es un software como una aplicación de servicio (SaaS) que proporciona varios inquilinos escalables y confiables, entorno tooautomate procesa con runbooks y administrar sistemas de Linux con la configuración de estado deseado y tooWindows de cambios de configuración (DSC) de servicios en la nube de Azure, otro o de forma local. Las entidades contenidas dentro de la cuenta de Automation, como runbooks, recursos y cuentas de ejecución están aisladas de otras cuentas de Automation dentro de la suscripción y de otras suscripciones.  

Los runbooks que ejecuta en Azure se ejecutan en espacios aislados de Automation que se hospedan en las máquinas virtuales de la plataforma como servicio (PaaS) de Azure.  Los espacios aislados de Automation proporcionan aislamiento de inquilinos para todos los aspectos de la ejecución del runbook: módulos, almacenamiento, memoria, comunicación de red, flujos de trabajo, etc. Esta función se administra mediante el servicio de hello y no es accesible desde su cuenta de Azure o la automatización de Azure para toocontrol.         

implementación de hello tooautomate y administración de recursos en el centro de datos local o de otros servicios en la nube, después de crear una cuenta de automatización, puede designar uno o más hello de toorun de máquinas [Hybrid Runbook Worker (HRW)](automation-hybrid-runbook-worker.md) rol.  Cada HRW requiere Hola agente de administración de Microsoft con un área de trabajo de análisis de registros de tooa de conexión y una cuenta de automatización.  Análisis de registros es instalación de hello toobootstrap usado, mantener Hola agente de administración de Microsoft y supervisar la funcionalidad de Hola de hello HRW.  entrega de Hola de hello y runbooks toorun instrucción que ellos se realizan mediante la automatización de Azure.

Puede implementar varios HRW tooprovide alta de disponibilidad para sus runbooks, trabajos de runbook de equilibrio de carga y en algunos casos los dedicar para las cargas de trabajo determinados o entornos.  Hola Microsoft Monitoring Agent en hello HRW inicia la comunicación con el servicio de automatización de hello en el puerto TCP 443 y no hay ningún requisito de firewall de entrada.  Una vez que tiene runbook con un HRW dentro del entorno de Hola y desea tareas de administración de hello runbook tooperform con otros equipos o servicios dentro de ese entorno, puede ser otros puertos que Hola necesita acceso a runbook.  Si las directivas de seguridad de TI no permitir que los equipos en su toohello de tooconnect de la red Internet, revise el artículo de hello [puerta de enlace de OMS](../log-analytics/log-analytics-oms-gateway.md), que actúa como un proxy para hello HRW toocollect estado del trabajo y recibir información de configuración de la cuenta de automatización.

Runbooks que se ejecutan en un HRW ejecutar en el contexto de hello de la cuenta de sistema local de hello en el equipo de hello, que se Hola recomienda contexto de seguridad al realizar acciones administrativas en el equipo de Windows local Hola. Si desea que las tareas de hello runbook toorun respecto a recursos fuera de la máquina local hello, deberá toodefine activos de segura de credenciales de cuenta de automatización que puede acceder desde runbook hello y usar tooauthenticate con un recurso externo Hola Hola. Puede usar [credencial](automation-credentials.md), [certificado](automation-certificates.md), y [conexión](automation-connections.md) activos en su runbook con los cmdlets que permiten credenciales toospecify por lo que puede autenticar a ellos.

Las configuraciones de DSC almacenadas en automatización de Azure pueden ser tooAzure aplicada directamente las máquinas virtuales. Otras máquinas físicas y virtuales pueden solicitar configuraciones de servidor de extracción de DSC de automatización de Azure Hola.  Para administrar las configuraciones de los locales sistemas físicos o virtuales Windows y Linux, no necesita toodeploy cualquier servidor extracción de infraestructura toosupport Hola DSC de automatización, sólo acceso saliente a Internet desde cada toobe sistema administrado por DSC de automatización , comunicarse a través de servicio de OMS de toohello de puerto 443 de TCP.   

## <a name="prerequisites"></a>Requisitos previos

### <a name="automation-dsc"></a>DSC de Automation
DSC de automatización de Azure puede ser usado toomanage diversos equipos:

* Máquinas virtuales de Azure (modelo clásico) con Windows o Linux
* Máquinas virtuales de Azure con Windows o Linux
* Máquinas virtuales de Amazon Web Services (AWS) con Windows o Linux
* Equipos físicos o virtuales con Windows, locales o en una nube que no sea Azure ni AWS
* Equipos físicos o virtuales con Linux, locales o en una nube que no sea Azure ni AWS

debe tener instalada la última versión de Hola de WMF 5 para el agente de DSC de PowerShell de Hola para Windows toobe puede toocommunicate con automatización de Azure. versión más reciente de Hola de hello [agente DSC de PowerShell para Linux](https://www.microsoft.com/en-us/download/details.aspx?id=49150) debe estar instalado para Linux toobe puede toocommunicate con automatización de Azure.

### <a name="hybrid-runbook-worker"></a>Hybrid Runbook Worker  
Al designar un runbook de equipo toorun híbrida trabajos, este equipo debe tener el siguiente de hello:

* Windows Server 2012 o superior
* Windows PowerShell 4.0 o posterior.  Se recomienda instalar Windows PowerShell 5.0 en el equipo de Hola para ofrecer mayor confiabilidad. Puede descargar la nueva versión de hello de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=50395)
* Dos núcleos como mínimo
* 4 GB de RAM como mínimo

### <a name="permissions-required-toocreate-automation-account"></a>Permisos necesario toocreate cuenta de automatización
toocreate o una cuenta de automatización de la actualización, debe tener Hola después determinados privilegios y permisos necesarios toocomplete en este tema.   
 
* En orden toocreate una cuenta de automatización, su cuenta de usuario de AD necesita toobe tooa agregado rol con el rol de propietario de toohello equivalente de permisos para los recursos de Microsoft.Automation tal como se describe en el artículo [control de acceso basado en roles en automatización de Azure ](automation-role-based-access-control.md).  
* Si los registros de aplicación Hola configuración se establece demasiado**Sí**, los usuarios sin derechos administrativos en el inquilino de Azure AD pueden [registrar aplicaciones AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions).  Si los registros de aplicación Hola configuración se establece demasiado**n**, usuario Hola realizar esta acción debe ser un administrador global de Azure AD. 

Si no eres un miembro de instancia de Active Directory de la suscripción de hello antes de que se agreguen toohello global administrador o coadministrator-administrator roles de suscripción de hello, se agregan tooActive directorio como invitado. En este caso, recibirá un "no tiene permisos toocreate..." Advertencia de hello **agregar una cuenta de automatización** hoja. Los usuarios que se agregaron toohello global administrador o coadministrator-administrator roles en primer lugar se pueden quitar de la instancia de Active Directory de la suscripción de Hola y vuelva a agregan toomake a un usuario en Active Directory completo. tooverify esta situación, hello **Azure Active Directory** panel Hola portal de Azure, seleccione **usuarios y grupos**, seleccione **todos los usuarios** y, después de seleccionar Hola un usuario específico, seleccione **perfil**. Hola valo hello **tipo de usuario** atributo en el perfil de los usuarios de hello no debería ser igual **invitado**.

## <a name="authentication-planning"></a>Planeamiento de la autenticación
Automatización de Azure permite tooautomate tareas con los recursos en Azure, de forma local y con otros proveedores de nube.  En orden para un runbook tooperform las acciones necesarias, deben tener permisos toosecurely acceso Hola recursos tenga derechos mínimos Hola requeridos dentro de la suscripción de Hola.  

### <a name="what-is-an-automation-account"></a>¿Qué es una cuenta de Automation? 
Todas las tareas de automatización de hello que realizar con los recursos mediante cmdlets de Azure de hello en automatización de Azure autentican tooAzure con autenticación de basada en credenciales de identidad organizativa de Azure Active Directory.  Una cuenta de automatización es independiente de la cuenta de hello usa toosign en toohello portal tooconfigure y utiliza recursos de Azure.  Incluido con una cuenta de recursos de automatización son siguientes de hello:

* **Certificados**: contiene un certificado utilizado para la autenticación desde un runbook o configuración de DSC o para agregarlos.
* **Las conexiones** -contiene autenticación y configuración tooconnect de información necesaria tooan servicio externo o una aplicación desde un runbook o la configuración de DSC.
* **Credenciales** -es un objeto PSCredential que contiene las credenciales de seguridad, como un nombre de usuario y contraseña necesarios tooauthenticate desde un runbook o la configuración de DSC.
* **Módulos de integración** -son módulos de PowerShell incluidos con un uso de cmdlets de runbooks y las configuraciones de DSC toomake de cuentas de automatización de Azure.
* **Programaciones**: contiene programaciones que inician o detienen un runbook en un momento especificado, incluidas las frecuencias de repetición.
* **Variables**: contiene valores que están disponibles desde un runbook o una configuración de DSC.
* **Las configuraciones de DSC** -son scripts de PowerShell que describe cómo tooconfigure una característica del sistema operativo o configurar o instalar una aplicación en un equipo Windows o Linux.  
* **Runbooks**: son un conjunto de tareas que realizan algún proceso automatizado en Azure Automation basado en Windows PowerShell.    

recursos de automatización de Hola para cada cuenta de automatización están asociados con una sola región de Azure, pero las cuentas de automatización pueden administrar todos los recursos de hello en su suscripción. Crear cuentas de automatización en regiones diferentes si tiene directivas que requieran datos y recursos toobe tooa aislado específico la región.

> [!NOTE]
> Cuentas de automatización y recursos Hola contienen que se crean en hello portal de Azure, no son accesibles en hello portal de Azure clásico. Si desea que toomanage estas cuentas o sus recursos con Windows PowerShell, debe usar módulos de hello Azure Resource Manager.
> 

Cuando se crea una cuenta de automatización en hello portal de Azure, se crean automáticamente dos entidades de autenticación:

* Una cuenta de ejecución. Esta cuenta crea una entidad de servicio en Azure Active Directory (Azure AD) y un certificado. También asigna control de acceso basado en roles de colaborador de hello (RBAC), que administra los recursos del Administrador de recursos mediante el uso de runbooks.
* Una cuenta de ejecución clásica. Esta cuenta carga un certificado de administración, que es toomanage usa los recursos clásicos mediante runbooks.

Control de acceso basado en roles está disponible con toogrant de Azure Resource Manager permite la cuenta de usuario de Azure AD de acciones tooan y cuenta de ejecución y autenticar esa entidad de seguridad de servicio.  Lectura [el control de acceso basado en roles en el artículo de automatización de Azure](automation-role-based-access-control.md) para obtener más información toohelp desarrolle su modelo para administrar permisos de automatización.  

#### <a name="authentication-methods"></a>Métodos de autenticación
Hello siguiente tabla resume Hola distintos métodos de autenticación para cada entorno compatible con automatización de Azure.

| Método | Environment 
| --- | --- | 
| Cuenta de ejecución y cuenta de ejecución de Azure clásico |Implementación de Azure Resource Manager e implementación clásica |  
| Cuenta de usuario de Azure AD |Implementación de Azure Resource Manager e implementación clásica |  
| Autenticación de Windows |Centro de datos local u otro proveedor de nube mediante Hola Hybrid Runbook Worker |  
| Credenciales de AWS |Amazon Web Services |  

En hello **cómo to\Authentication y seguridad** sección, son compatibles con artículos proporciona pasos Introducción e implementación de autenticación de tooconfigure para estos entornos, ya sea con una existente o nueva cuenta Dedique para ese entorno.  Hello Azure identificación y cuenta de identificación clásico, Hola tema [actualización automatización de la cuenta de ejecución](automation-create-runas-account.md) describe cómo tooupdate su cuenta de automatización existente con hello ejecutar como cuentas de portal de Hola o mediante PowerShell si aún no se se configuró originalmente con una cuenta de ejecución o identificación clásico. Si desea toocreate ejecutar como y una cuenta de identificación clásico con un certificado emitido por la entidad de certificación (CA) empresarial, revise esta toolearn artículo cómo toocreate Hola cuentas con esta configuración.     
 
## <a name="network-planning"></a>Planeamiento de red
Para hello register de tooand tooconnect de Runbook Worker híbrido con Microsoft Operations Management Suite (OMS), debe tener el número de puerto de acceso toohello y hello las direcciones URL se describen a continuación.  Esto es además toohello [puertos y las direcciones URL necesarias para Hola Microsoft Monitoring Agent](../log-analytics/log-analytics-windows-agents.md#network) tooconnect tooOMS. Si utiliza un servidor proxy para la comunicación entre el agente de Hola y el servicio OMS hello, deberá tooensure que los recursos adecuados de hello son accesibles. Si usa un toohello de acceso de firewall toorestrict Internet, deberá tooconfigure el acceso de toopermit firewall.

información de Hello debajo de puerto Hola de lista y las direcciones URL que son necesarias para hello Hybrid Runbook Worker toocommunicate con la automatización.

* Puerto: solo se requiere el puerto TCP 443 para el acceso a Internet
* URL global: *.azure-automation.net

Si tiene una cuenta de automatización definida para una región específica y desea toorestrict comunicación con ese centro de datos regional, hello tabla siguiente proporciona registro DNS de Hola para cada región.

| **Región** | **Registro DNS** |
| --- | --- |
| Centro-Sur de EE. UU |scus-jobruntimedata-prod-su1.azure-automation.net |
| Este de EE. UU. 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| Centro occidental de EE.UU. | wcus-jobruntimedata-prod-su1.azure-automation.net |
| Europa occidental |we-jobruntimedata-prod-su1.azure-automation.net |
| Europa del Norte |ne-jobruntimedata-prod-su1.azure-automation.net |
| Centro de Canadá |cc-jobruntimedata-prod-su1.azure-automation.net |
| Sudeste de Asia |sea-jobruntimedata-prod-su1.azure-automation.net |
| India Central |cid-jobruntimedata-prod-su1.azure-automation.net |
| Este de Japón |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Sudeste de Australia |ase-jobruntimedata-prod-su1.azure-automation.net |
| Sur del Reino Unido 2 | uks-jobruntimedata-prod-su1.azure-automation.net |
| Gobierno de EE. UU. - Virginia | usge-jobruntimedata-prod-su1.azure-automation.us |

Para obtener una lista de direcciones IP en lugar de nombres, descargue y revise hello [dirección IP del centro de datos de Azure](https://www.microsoft.com/download/details.aspx?id=41653) archivo xml de hello Microsoft Download Center. 

> [!NOTE]
> Este archivo contiene Hola intervalos de direcciones IP (incluidos los intervalos de proceso, SQL y almacenamiento) utilizados en hello centros de datos de Microsoft Azure. Un archivo actualizado se publica una vez que refleja los intervalos de Hola implementada actualmente y los intervalos de IP toohello próximos cambios. Nuevos intervalos que aparecen en el archivo hello no se utilizará en los centros de datos de Hola durante al menos una semana. Por favor, descarga Hola nuevo xml archivo cada semana y realizar los cambios necesarios de hello en el sitio toocorrectly identificar servicios que se ejecutan en Azure. Los usuarios de ruta rápidos pueden tenga en cuenta que este archivo usa tooupdate Hola publicidad de BGP de Azure espacio Hola primera semana de cada mes. 
> 

## <a name="creating-an-automation-account"></a>Creación de una cuenta de Automation

Hay diferentes maneras de que crear una cuenta de automatización en hello portal de Azure.  Hello en la tabla siguiente presenta a cada tipo de experiencia de implementación y las diferencias entre ellos.  

|Método | Descripción |
|-------|-------------|
| Seleccione el Control y automatización de hello Marketplace | Una oferta, que crea una cuenta de automatización y el área de trabajo OMS vinculado tooone otra en Hola mismo grupo de recursos y la región.  Integración con OMS también incluye la ventaja de hello del uso de análisis de registros toomonitor y analizar secuencias de estado y el trabajo del trabajo de runbook con el tiempo y utilizar características avanzadas tooescalate o investigar los problemas. Hola oferta también implementa soluciones de hello seguimiento de cambios y administración de actualizaciones, que están habilitadas de forma predeterminada. |
| Seleccione automatización de hello Marketplace | Crea una cuenta de automatización en un grupo de recursos nuevo o existente que no está vinculado tooan área de trabajo OMS y no incluye ninguna solución disponible de la oferta de automatización y Control de Hola. Esto es una configuración básica que le presenta tooAutomation y puede ayudarle a aprender cómo toowrite runbooks y las configuraciones de DSC, use Hola funciones de servicio de Hola. |
| Soluciones de administración seleccionadas | Si selecciona una solución:  **[administración de actualizaciones](../operations-management-suite/oms-solution-update-management.md)**,  **[máquinas virtuales de inicio/detención durante horas de poca actividad](automation-solution-vm-management.md)**, o  **[ Seguimiento de cambios](../log-analytics/log-analytics-change-tracking.md)**  solicitará que el área de trabajo OMS y tooselect una automatización existente, o para ofrecer Hola toocreate opción como necesarios para hello solución toobe implementado en su suscripción. |

Este tema explica cómo crear un área de trabajo OMS y cuenta de automatización de la oferta de automatización y Control de incorporación Hola.  una cuenta de automatización de pruebas o toopreview Hola un servicio, Hola de revisión del artículo siguiente independiente toocreate [crear cuenta de automatización independiente](automation-create-standalone-account.md).  

### <a name="create-automation-account-integrated-with-oms"></a>Creación de una cuenta de Automation integrada con OMS
Hola recomienda tooonboard método que automatización está seleccionando la oferta de automatización y Control de Hola de hello Marketplace.  Esto crea una cuenta de automatización y establece la integración de hello con un área de trabajo OMS, incluidos Hola opción tooinstall Hola soluciones de administración que están disponibles con la oferta de Hola.  

1. Inicie sesión en toohello portal de Azure con una cuenta que sea miembro del rol de los administradores de suscripciones de Hola y Coadministrador de suscripción de Hola.

2. Haga clic en **Nuevo**.<br><br> ![Seleccione la opción Nuevo en Azure Portal](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  

3. Busque **automatización** y, a continuación, en hello resultados de la búsqueda seleccione **Control y automatización***.<br><br> ![Busque y seleccione Automation and Control en Marketplace](media/automation-offering-get-started/automation-portal-martketplace-select-automationandcontrol.png).<br>   

4. Después de leer la descripción de Hola para oferta de hello, haga clic en **crear**.  

5. En hello **Control y automatización** hoja de configuración, seleccione **área de trabajo de OMS**.  En hello **áreas de trabajo de OMS** hoja, seleccione un toohello de área de trabajo vinculado de OMS misma suscripción de Azure que Hola cuenta de automatización está en o cree un área de trabajo OMS.  Si no tiene un área de trabajo OMS, seleccione **crear nueva área de trabajo** y en hello **área de trabajo de OMS** hoja realizar siguiente hello: 
   - Especifique un nombre para el nuevo hello **área de trabajo de OMS**.
   - Seleccione un **suscripción** toolink tooby selección de lista desplegable de hello si predeterminado Hola seleccionado no es adecuado.
   - Para **Grupo de recursos**, puede crear un grupo de recursos o seleccionar uno existente.  
   - Seleccione una **ubicación**.  Actualmente Hola únicas ubicaciones a disponibles son **sudeste de Australia**, **UU**, **sudeste de Asia**, **oeste Ee.uu. Central**y  **Europa occidental**.
   - Seleccione un **plan de tarifa**.  solución de Hola se ofrece en dos niveles: libre y niveles por nodo (OMS).  nivel gratis Hello tiene un límite de cantidad de Hola de datos recopilados diariamente, período de retención y minutos de tiempo de ejecución del trabajo de runbook.  Hola por nodo (OMS) nivel no tiene un límite de cantidad de Hola de datos recopilados diariamente.  
   - Seleccione **Cuenta de Automation**.  Si va a crear una nueva área de trabajo OMS, es necesario tooalso crear una cuenta de automatización que se asocia a Hola nueva área de trabajo OMS especificado anteriormente, incluida su suscripción de Azure, el grupo de recursos y la región.  Puede seleccionar **crear una cuenta de automatización** y en hello **cuenta de automatización** hoja, proporciona Hola siguiente: 
  - Hola **nombre** , escriba el nombre de Hola de hello cuenta de automatización.

    Todas las demás opciones se rellenan automáticamente basándose en el área de trabajo OMS de hello seleccionado y no se puede modificar estas opciones.  Una cuenta de identificación de Azure es método de autenticación predeterminado de Hola para oferta de Hola.  Una vez que pulses **Aceptar**, se validan las opciones de configuración de Hola y Hola cuenta de automatización se crea.  Puede realizar un seguimiento de su progreso en **notificaciones** en el menú de Hola. 

    En caso contrario, seleccione una cuenta de ejecución de Automation existente.  cuenta de Hello seleccionada ya no puede ser vinculado tooanother área de trabajo OMS, en caso contrario, se presenta un mensaje de notificación en la hoja de Hola.  Si ya está vinculado, necesita tooselect una cuenta de identificación de automatización diferente o crear uno.

    Después de completar la información de hello necesaria, haga clic en **crear**.  se comprueba la información de Hola y se crean las cuentas de automatización de la cuenta y la ejecución de Hola.  Se devuelven toohello **área de trabajo OMS** hoja automáticamente.  

6. Después de proporcionar información de hello necesario en hello **área de trabajo de OMS** hoja, haga clic en **crear**.  Mientras se comprueba la información de Hola y crea el área de trabajo de hello, puede realizar un seguimiento de su progreso en **notificaciones** en el menú de Hola.  Se devuelven toohello **Agregar solución** hoja.  

7. En hello **Control y automatización** hoja de configuración, confirme la tooinstall Hola recomienda soluciones seleccionadas previamente. Si anula la selección de alguna de ellas puede instalarlas individualmente más adelante.  

8. Haga clic en **crear** tooproceed con automatización de la incorporación y un área de trabajo OMS. Se validan todas las opciones y, a continuación, intenta hello toodeploy oferta en su suscripción.  Este proceso puede tardar unos segundos toocomplete y se puede realizar un seguimiento de su progreso en **notificaciones** en el menú de Hola. 

Una vez oferta Hola incorporado, puede empezar a crear soluciones de administración que habilitado de runbooks, trabajar con hello, implementar un [Runbook worker híbrido](automation-hybrid-runbook-worker.md) rol o empezar a trabajar con [análisis de registros](https://docs.microsoft.com/azure/log-analytics) datos de toocollect generados por los recursos en su entorno de nube o local.   

## <a name="next-steps"></a>Pasos siguientes
* Puede confirmar la nueva cuenta de Automation para autenticarse con recursos de Azure mediante la revisión del artículo [Comprobación de la autenticación con la cuenta de ejecución de Azure Automation](automation-verify-runas-authentication.md).
* tooget se inicia con la creación de runbooks, primero consulte hello [tipos de runbook de automatización](automation-runbook-types.md) compatible y relacionados con las consideraciones antes de empezar a crear.


