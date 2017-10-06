---
title: "áreas de trabajo de aaaManage de portal de OMS hello y análisis de registros de Azure | Documentos de Microsoft"
description: "Puede administrar áreas de trabajo de análisis de registros de Azure y Hola portal de OMS mediante una serie de tareas administrativas en los usuarios, cuentas, áreas de trabajo y cuentas de Azure."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: d0e5162d-584b-428c-8e8b-4dcaa746e783
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/06/2017
ms.author: magoedte
ms.openlocfilehash: 570e6c1f13ad28f120ecd65052d00c4ca986ac98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-workspaces"></a>Administración de áreas de trabajo

toomanage acceso tooLog análisis, realizar diversas tareas administrativas a relacionadas tooworkspaces. Este artículo proporciona recomienda consejos y procedimientos toomanage áreas de trabajo. Un área de trabajo es básicamente un contenedor que incluye información de la cuenta e información de configuración sencilla para la cuenta de hello. Usted u otros miembros de su organización pueden usar varias áreas de trabajo toomanage distintos conjuntos de datos que se recopilan de todas o de partes de su infraestructura de TI.

toocreate un área de trabajo, debe:

1. Tener una suscripción a Azure.
2. Elegir un nombre de área de trabajo.
3. Asociar el área de trabajo de Hola a su suscripción.
4. Elegir una ubicación geográfica.

## <a name="determine-hello-number-of-workspaces-you-need"></a>Determinar el número de Hola de áreas de trabajo que necesita
Un área de trabajo es un recurso de Azure y es un contenedor donde datos se recopilan, agregan, analizan y presentan en hello portal de Azure.

Puede tener varias áreas de trabajo por suscripción de Azure y puede tener acceso toomore a un área de trabajo. Número de hello minimizar de áreas de trabajo permite tooquery y correlacionar Hola mayoría de los datos, ya que no es posible tooquery en varias áreas de trabajo. Esta sección describe cuándo puede ser útil toocreate más de un área de trabajo.

En la actualidad, un área de trabajo proporciona:

* Una ubicación geográfica para el almacenamiento de datos
* Granularidad para la facturación
* Aislamiento de datos
* Ámbito de configuración

En función de hello anterior características, puede que desee toocreate varias áreas de trabajo si:

* Una empresa internacional que necesita que los datos estén almacenados en regiones concretas por motivos de soberanía de datos o cumplimiento normativo.
* Usa Azure y desea que la transferencia de datos de salida tooavoid cargos por tener un área de trabajo Hola misma región como Hola recursos de Azure que administra.
* Desea toodifferent departamentos de tooallocate cargos o grupos de negocios según su uso. Cuando se crea un área de trabajo para cada departamento o grupo de negocios, la instrucción de facturación y uso de Azure muestra los cargos de Hola de cada área de trabajo por separado.
* Es un proveedor de servicios administrados y necesita datos de análisis de registro de hello tookeep para cada cliente que se administran aislada de los datos de otro cliente.
* Administrar varios clientes y desea que cada cliente / departamento / business group toosee sus propios datos, pero no los datos de Hola para que otros usuarios.

Cuando se usan datos de toocollect de agentes, también puede [configurar cada tooone de tooreport de agente o más áreas de trabajo](log-analytics-windows-agents.md).

Si usa System Center Operations Manager, cada grupo de administración de Operations Manager se puede conectar con una sola área de trabajo. Puede instalar Hola Microsoft Monitoring Agent en equipos administrados por Operations Manager y tener Hola agente informe tooboth Operations Manager y otra área de trabajo de análisis de registros.

### <a name="workspace-information"></a>Información del área de trabajo

Puede ver detalles sobre el área de trabajo en hello portal de Azure. También puede ver detalles en el portal de OMS Hola.

#### <a name="view-workspace-information-in-hello-azure-portal"></a>Ver información de área de trabajo en hello portal de Azure

1. Si aún no lo ha hecho, inicie sesión en toohello [portal de Azure](https://portal.azure.com) con su suscripción de Azure.
2. En hello **concentrador** menú, haga clic en **más servicios** y en la lista de Hola de recursos, escriba **análisis de registros**. Cuando empiece a escribir, Hola filtros de la lista con los datos especificados. Haga clic en **Log Analytics**.  
    ![Menú central de Azure](./media/log-analytics-manage-access/hub.png)  
3. En la hoja de suscripciones de análisis de registros de hello, seleccione un área de trabajo.
4. hoja de área de trabajo de Hello muestra detalles sobre el área de trabajo de Hola y vínculos para obtener información adicional.  
    ![detalles de área de trabajo](./media/log-analytics-manage-access/workspace-details.png)  


## <a name="manage-accounts-and-users"></a>Administración de cuentas y usuarios
Cada área de trabajo puede tener varias cuentas asociadas con él, y cada cuenta (cuenta de Microsoft o cuenta profesional) puede tener acceso a áreas de trabajo de toomultiple.

De forma predeterminada, cuenta de Microsoft de Hola o cuenta profesional que crea el área de trabajo de Hola se convierte en Administrador del área de trabajo de Hola Hola.

Hay dos modelos de permiso que controlan el área de trabajo de análisis de registros de tooa de acceso:

1. Roles de usuario heredados de Log Analytics
2. [Acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md)

Hello en la tabla siguiente resume el acceso de Hola que se pueden establecer con cada modelo de permisos:

|                          | Portal de Log Analytics | Azure Portal | API (incluido PowerShell) |
|--------------------------|----------------------|--------------|----------------------------|
| Roles de usuario de Log Analytics | Sí                  | No           | No                         |
| Acceso basado en roles de Azure  | Sí                  | Sí          | Sí                        |

> [!NOTE]
> Análisis de registros refiere a toouse acceso basado en roles de Azure como modelo de permisos de hello, reemplazando los roles de usuario de análisis de registros de Hola.
>
>

Hello heredados roles de usuario de análisis de registros solo controlan tooactivities de acceso que se realizan en hello [portal de análisis de registros](https://mms.microsoft.com).

Hola siguiendo las actividades también requiere permisos de Azure:

| Acción                                                          | Permisos de Azure necesarios | Notas |
|-----------------------------------------------------------------|--------------------------|-------|
| Agregar y quitar soluciones de administración                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/*` <br> `Microsoft.OperationsManagement/*` <br> `Microsoft.Automation/*` <br> `Microsoft.Resources/deployments/*/write` | |
| Cambiar el nivel de precios de Hola                                       | `Microsoft.OperationalInsights/workspaces/*/write` | |
| Ver los datos en hello *copia de seguridad* y *Site Recovery* iconos de las soluciones | Administrador o coadministrador | Recursos de accesos implementan utilizando el modelo de implementación clásica de Hola |
| Crear un área de trabajo en hello portal de Azure                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/workspaces/*` ||


### <a name="managing-access-toolog-analytics-using-azure-permissions"></a>Administrar acceso tooLog análisis con permisos de Azure
toogrant acceso toohello análisis de registros área de trabajo mediante permisos de Azure, siga los pasos de hello en [usar recursos de suscripción de Azure de rol asignaciones toomanage acceso tooyour](../active-directory/role-based-access-control-configure.md).

Azure tiene dos roles de usuario integrados para Log Analytics:
- Lector de Log Analytics
- Colaborador de Log Analytics

Los miembros de hello *registro del log Analytics* rol puede:
- Ver y buscar todos los datos de supervisión 
- Ver configuración de supervisión, como ver la configuración de Hola de diagnósticos de Azure en todos los recursos de Azure.

| Tipo    | Permiso | Descripción |
| ------- | ---------- | ----------- |
| Acción | `*/read`   | Capacidad tooview todos los recursos y la configuración de recursos. Incluye la visualización de: <br> Estado de la extensión de la máquina virtual <br> Configuración de Azure Diagnostics en los recursos <br> Todas las propiedades y opciones de configuración de todos los recursos |
| Acción | `Microsoft.OperationalInsights/workspaces/analytics/query/action` | Consultas de tooperform v2 de búsqueda de registros de capacidad |
| Acción | `Microsoft.OperationalInsights/workspaces/search/action` | Consultas de tooperform v1 de búsqueda de registros de capacidad |
| Acción | `Microsoft.Support/*` | Casos de soporte técnico de tooopen de capacidad |
|No acción | `Microsoft.OperationalInsights/workspaces/sharedKeys/read` | Evita la lectura del área de trabajo clave toouse necesario Hola datos colección API y tooinstall agentes |


Los miembros de hello *colaborador de análisis de registro* rol puede:
- Leer todos los datos de supervisión 
- Crear y configurar cuentas de Automation
- Agregar y quitar soluciones de administración
- Leer las claves de las cuentas de almacenamiento 
- Configurar la recopilación de registros de Azure Storage
- Editar la configuración de supervisión de los recursos de Azure:
  - Agregar tooVMs de extensión VM de Hola
  - Configurar Azure Diagnostics en todos los recursos de Azure

> [!NOTE] 
> Puede usar Hola capacidad tooadd un máquina virtual extensión tooa máquina virtual toogain control total sobre una máquina virtual.

| Permiso | Descripción |
| ---------- | ----------- |
| `*/read`     | Capacidad tooview todos los recursos y la configuración de recursos. Incluye la visualización de: <br> Estado de la extensión de la máquina virtual <br> Configuración de Azure Diagnostics en los recursos <br> Todas las propiedades y opciones de configuración de todos los recursos |
| `Microsoft.Automation/automationAccounts/*` | Capacidad toocreate y configurar cuentas de automatización de Azure, incluido cómo agregar y editar runbooks |
| `Microsoft.ClassicCompute/virtualMachines/extensions/*` <br> `Microsoft.Compute/virtualMachines/extensions/*` | Agregar, actualizar y quitar extensiones de máquina virtual, incluida la extensión de Microsoft Monitoring Agent de Hola y Hola agente de OMS para Linux extensión |
| `Microsoft.ClassicStorage/storageAccounts/listKeys/action` <br> `Microsoft.Storage/storageAccounts/listKeys/action` | Clave de cuenta de almacenamiento de Hola de vista. Necesario tooread registros de análisis de registros de tooconfigure de cuentas de almacenamiento de Azure |
| `Microsoft.Insights/alertRules/*` | Agregar, actualizar y eliminar reglas de alertas |
| `Microsoft.Insights/diagnosticSettings/*` | Agregar, actualizar y eliminar la configuración de diagnósticos en los recursos de Azure |
| `Microsoft.OperationalInsights/*` | Agregar, actualizar y eliminar la configuración de áreas de trabajo de Log Analytics |
| `Microsoft.OperationsManagement/*` | Agregar y eliminar soluciones de administración |
| `Microsoft.Resources/deployments/*` | Crear y eliminar implementaciones. Necesario para agregar y eliminar soluciones, áreas de trabajo y cuentas de Automation |
| `Microsoft.Resources/subscriptions/resourcegroups/deployments/*` | Crear y eliminar implementaciones. Necesario para agregar y eliminar soluciones, áreas de trabajo y cuentas de Automation |

tooadd y quitar usuarios tooa rol de usuario, es necesario toohave `Microsoft.Authorization/*/Delete` y `Microsoft.Authorization/*/Write` permiso.

Utilice estos usuarios toogive de roles de acceso en distintos ámbitos:
- Suscripción: áreas de trabajo de acceso tooall de suscripción de Hola
- Grupo de recursos: área de trabajo de Access tooall en grupo de recursos de Hola
- Especifica el recurso - Hola de acceso tooonly área de trabajo

Use [roles personalizados](../active-directory/role-based-access-control-custom-roles.md) toocreate roles con permisos concretos Hola necesarios.

### <a name="azure-user-roles-and-log-analytics-portal-user-roles"></a>Roles de usuario de Azure y roles de usuario del portal de Log Analytics
Si tiene en Azure menos permiso de lectura en el área de trabajo de hello análisis de registros, puede abrir el portal de análisis de registros de hello haciendo clic en hello **Portal de OMS** al ver el área de trabajo de análisis de registros de Hola de tareas.

Al abrir el portal de análisis de registros de hello, cambie las funciones de usuario de toousing Hola heredadas análisis de registros. Si no tiene una asignación de roles en el portal de análisis de registros de hello, Hola servicio [Hola de comprobaciones de permisos de Azure tiene en el área de trabajo de Hola](https://docs.microsoft.com/rest/api/authorization/permissions#Permissions_ListForResource).
La asignación de roles en el portal de análisis de registros de Hola se determina según como se indica a continuación:

| Condiciones                                                   | Rol de usuario asignado de Log Analytics | Notas |
|--------------------------------------------------------------|----------------------------------|-------|
| La cuenta pertenece el rol de usuario de análisis de registros heredado tooa     | Hola especifica el rol de usuario de análisis de registros | |
| La cuenta no pertenece tooa heredado rol de usuario de análisis de registros <br> El área de trabajo de Azure completo permisos toohello (`*` permiso <sup>1</sup>) | Administrador ||
| La cuenta no pertenece tooa heredado rol de usuario de análisis de registros <br> El área de trabajo de Azure completo permisos toohello (`*` permiso <sup>1</sup>) <br> *sin acciones* de `Microsoft.Authorization/*/Delete` y `Microsoft.Authorization/*/Write` | Colaborador ||
| La cuenta no pertenece tooa heredado rol de usuario de análisis de registros <br> Permiso de lectura de Azure | Solo lectura ||
| La cuenta no pertenece tooa heredado rol de usuario de análisis de registros <br> Los permisos de Azure no se entienden | Solo lectura ||
| Para suscripciones administradas por el Proveedor de soluciones en la nube (CSP) <br> Hola cuenta con la que inició sesión con está en el área de trabajo de hello Azure Active Directory vinculado toohello | Administrador | Normalmente los clientes de Hola de un CSP |
| Para suscripciones administradas por el Proveedor de soluciones en la nube (CSP) <br> Hola cuenta con la que inició sesión con no está en el área de trabajo de hello Azure Active Directory vinculado toohello | Colaborador | Normalmente Hola CSP |

<sup>1</sup> consulte demasiado[permisos de Azure](../active-directory/role-based-access-control-custom-roles.md) para obtener más información sobre las definiciones de roles. Al evaluar funciones, una acción de `*` no es equivalente demasiado`Microsoft.OperationalInsights/workspaces/*`.

Algunos tookeep puntos en cuenta sobre Hola portal de Azure:

* Al iniciar sesión en el portal OMS de toohello con http://mms.microsoft.com, vea hello **seleccionar un área de trabajo** lista. Esta lista solo contiene áreas de trabajo en las que tiene un rol de usuario de Log Analytics. áreas de trabajo de toosee hello tiene acceso a toowith Azure suscripciones, deberá toospecify un inquilino como parte de la dirección URL de Hola. Por ejemplo: `mms.microsoft.com/?tenant=contoso.com`. identificador del inquilino de Hello es a menudo esa última parte de dirección de correo electrónico de Hola que usan toosign en.
* Si desea toonavigate directamente toousing Azure de acceso al portal de tooa que tiene permisos, tendrá que recurso de hello toospecify como parte de la dirección URL de Hola. Es posible tooget esta dirección URL con PowerShell.

  Por ejemplo: `(Get-AzureRmOperationalInsightsWorkspace).PortalUrl`.

  dirección URL de Hello tiene el siguiente aspecto:`https://eus.mms.microsoft.com/?tenant=contoso.com&resource=%2fsubscriptions%2faaa5159e-dcf6-890a-a702-2d2fee51c102%2fresourcegroups%2fdb-resgroup%2fproviders%2fmicrosoft.operationalinsights%2fworkspaces%2fmydemo12`

### <a name="managing-users-in-hello-oms-portal"></a>Administración de usuarios en el portal de OMS Hola
Administrar usuarios y grupos en hello **administrar usuarios** pestaña hello **cuentas** pestaña en la página de configuración de Hola.   

![administrar usuarios](./media/log-analytics-manage-access/setup-workspace-manage-users.png)


#### <a name="add-a-user-tooan-existing-workspace"></a>Agregar un área de trabajo de usuario tooan existente
Usar hello siguiendo los pasos tooadd un área de trabajo de tooa de usuario o grupo.

1. En el portal de OMS de hello, haga clic en hello **configuración** icono.
2. Haga clic en hello **cuentas** ficha y, a continuación, haga clic en hello **administrar usuarios** ficha.
3. Hola **administrar usuarios** sección, elija tooadd de tipo de cuenta de hello: **cuenta profesional**, **Account Microsoft**, **Microsoft Support**.

   * Si elige Microsoft Account, escriba la dirección de correo electrónico de Hola de hello asociados con hello Account de Microsoft.
   * Si elige cuenta profesional, escriba parte del usuario de Hola / alias de correo electrónico o el nombre del grupo y una lista de usuarios y grupos de coincidencia aparece en un cuadro de lista desplegable. Seleccione un usuario o grupo.
   * Usar Microsoft Support toogive un ingeniero de Microsoft Support u otro toohelp de área de trabajo de Microsoft empleado acceso temporal tooyour a solucionar el problema.

     > [!NOTE]
     > Para obtener el mejor rendimiento de hello, limitar el número de Hola de grupos de Active Directory asociados con una sola toothree de cuenta OMS: uno para administradores, uno para los colaboradores y otro para usuarios de solo lectura. Uso de más grupos puede afectar al rendimiento de Hola de análisis de registros.
     >
     >
4. Elegir tipo de Hola de usuario o grupo tooadd: **administrador**, **colaborador**, o **usuario ReadOnly**.  
5. Haga clic en **Agregar**.

   Si va a agregar una cuenta de Microsoft, un área de trabajo de invitación toojoin Hola se envía correo electrónico de toohello que proporcionó. Después de que el usuario de hello sigue las instrucciones de hello en hello invitación toojoin OMS, usuario Hola puede tener acceso a área de trabajo de Hola.
   Si va a agregar una cuenta profesional, Hola usuario puede tener acceso a análisis de registros inmediatamente.  

#### <a name="edit-an-existing-user-type"></a>Edición de un tipo de usuario existente
Puede cambiar el rol de la cuenta de hello para un usuario asociado a su cuenta de OMS. Tener Hola siguientes opciones de rol:

* *Administrador*: puede administrar usuarios, ver y actuar en todas las alertas y agregar y quitar servidores
* *Colaborador*: puede ver y actuar en todas las alertas y agregar y quitar servidores
* *Usuario de solo lectura*: los usuarios con este rol no podrán hacer lo siguiente:

  1. Agregar o quitar soluciones. Galería de soluciones de Hello está oculto.
  2. Agregar, modificar o eliminar iconos en **Mi panel**.
  3. Hola de vista **configuración** páginas. páginas de Hello están ocultos.
  4. En la vista de búsqueda de hello, configuración de Power BI, búsquedas guardadas y alertas, las tareas están ocultas.

#### <a name="tooedit-an-account"></a>tooedit una cuenta
1. En el portal de OMS de hello, haga clic en hello **configuración** icono.
2. Haga clic en hello **cuentas** ficha y, a continuación, haga clic en hello **administrar usuarios** ficha.
3. Seleccione el rol de hello para el usuario de Hola que desea toochange.
4. En el cuadro de diálogo de confirmación de hello, haga clic en **Sí**.

### <a name="remove-a-user-from-a-workspace"></a>Eliminación de un usuario de un área de trabajo
Usar hello siguiendo los pasos tooremove un usuario de un área de trabajo. Quitar usuario hello no Cerrar área de trabajo de Hola. En su lugar, elimina Hola asociación entre ese usuario y el área de trabajo de Hola. Si un usuario está asociado a varias áreas de trabajo, ese usuario todavía puede iniciar sesión en tooOMS y vea sus otras áreas de trabajo.

1. En el portal de OMS de hello, haga clic en hello **configuración** icono.
2. Haga clic en hello **cuentas** ficha y, a continuación, haga clic en hello **administrar usuarios** ficha.
3. Haga clic en **quitar** siguiente nombre de usuario de toohello que desea tooremove.
4. En el cuadro de diálogo de confirmación de hello, haga clic en **Sí**.

### <a name="add-a-group-tooan-existing-workspace"></a>Agregar un área de trabajo de grupo tooan existente
1. Hola "tooadd un área de trabajo de usuario tooan existente" de la sección anterior, siga los pasos 1-4.
2. En **Elegir usuario/grupo**, seleccione **Grupo**.  
   ![Agregar un área de trabajo de grupo tooan existente](./media/log-analytics-manage-access/add-group.png)
3. Escriba la dirección de correo electrónico o nombre para mostrar de hello para el grupo de hello le gustaría tooadd.
4. Seleccione el grupo de hello en resultados de la lista de hello y, a continuación, haga clic en **agregar**.

## <a name="link-an-existing-workspace-tooan-azure-subscription"></a>Vincular un tooan de área de trabajo existente suscripción de Azure
Todas las áreas de trabajo creadas después de 26 de septiembre de 2016 deben estar vinculado tooan suscripción de Azure en tiempo de creación. Áreas de trabajo creadas antes de esta fecha deben ser el área de trabajo vinculado tooa al iniciar sesión. Al crear el área de trabajo de Hola de hello portal de Azure, o al vincular su suscripción de Azure de área de trabajo tooan, Azure Active Directory se vincula con su cuenta organizativa.

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-oms-portal"></a>toolink una suscripción de Azure en el portal de OMS hello tooan de área de trabajo

- Al iniciar sesión en el portal de OMS Hola, son tooselect solicitada una suscripción de Azure. Seleccione la suscripción de Hola que desea que el área de trabajo de toolink tooyour y, a continuación, haga clic en **vínculo**.  
    ![Vínculo a la suscripción de Azure](./media/log-analytics-manage-access/required-link.png)

    > [!IMPORTANT]
    > toolink un área de trabajo, su cuenta de Azure ya debe tener acceso de área de trabajo toohello le gustaría toolink.  En otras palabras, la cuenta de hello usar tooaccess Hola portal de Azure debe **Hola mismo** como cuenta de hello que use el área de trabajo de tooaccess Hola. Si no es así, consulte [agregar un área de trabajo existente de usuario tooan](#add-a-user-to-an-existing-workspace).

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-azure-portal"></a>toolink una suscripción de Azure en el portal de Azure hello tooan de área de trabajo
1. Inicio de sesión en hello [portal de Azure](http://portal.azure.com).
2. Busque **Log Analytics** y selecciónelo.
3. Aparecerá una lista con las áreas de trabajo existentes. Haga clic en **Agregar**.  
   ![lista de áreas de trabajo](./media/log-analytics-manage-access/manage-access-link-azure01.png)
4. En **OMS Workspace** (Área de trabajo de OMS), haga clic en **Or link existing** (O vincular existente).  
   ![vincular existente](./media/log-analytics-manage-access/manage-access-link-azure02.png)
5. Haga clic en **Configurar los valores obligatorios**.  
   ![configure required settings](./media/log-analytics-manage-access/manage-access-link-azure03.png)
6. Vea la lista de Hola de áreas de trabajo que no están vinculados aún tooyour cuenta de Azure. Seleccione un área de trabajo.  
   ![seleccionar áreas de trabajo](./media/log-analytics-manage-access/manage-access-link-azure04.png)
7. Si es necesario, puede cambiar los valores de hello siguientes elementos:
   * La suscripción
   * Grupos de recursos
   * Ubicación
   * Plan de tarifa   
     ![cambiar valores](./media/log-analytics-manage-access/manage-access-link-azure05.png)
8. Haga clic en **Aceptar**. área de trabajo de Hello ya está vinculado tooyour cuenta de Azure.

> [!NOTE]
> Si no ve el área de trabajo de hello le gustaría toolink, a continuación, la suscripción de Azure no tiene acceso de área de trabajo toohello que haya creado mediante el portal de OMS Hola.  cuenta de acceso toothis de toogrant Hola portal de OMS, consulte [agregar un área de trabajo existente de usuario tooan](#add-a-user-to-an-existing-workspace).
>
>

## <a name="upgrade-a-workspace-tooa-paid-plan"></a>Actualizar un tooa de área de trabajo plan de pago
En OMS, existen tres tipos de planes de áreas de trabajo: **Free** (Gratis), **Standalone** (Independiente) y **OMS**.  Si se encuentra en hello *libre* planear, hay un límite de 500 MB de datos por día enviados tooLog análisis.  Si se supera esta cantidad, debe toochange su tooavoid del plan de tooa de pago de área de trabajo no está recopilando datos una vez alcanzado este límite. Puede cambiar de tipo de plan en cualquier momento.  Para más información sobre los precios de OMS, consulte [Precios de Operations Management Suite](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-pricing).

### <a name="using-entitlements-from-an-oms-subscription"></a>Uso de los derechos de una suscripción de OMS
derechos de hello toouse que proceden de compra OMS E1, OMS E2 OMS o un complemento de OMS para System Center, elija hello *OMS* plan de análisis de registros de OMS.

Al adquirir una suscripción de OMS, derechos de Hola se agregan tooyour contrato Enterprise. Cualquier suscripción de Azure que se crea en este contrato puede usar los derechos de Hola. Todas las áreas de trabajo en estas suscripciones utilice derechos de OMS Hola.

tooensure que el uso de un área de trabajo es tooyour aplicado derechos de hello suscripción de OMS, debe:

1. Crear el área de trabajo en una suscripción de Azure que forma parte del contrato Enterprise que incluye una suscripción de OMS Hola Hola
2. Seleccione hello *OMS* plan para el área de trabajo de Hola

> [!NOTE]
> Si se creó el área de trabajo antes de 26 de septiembre de 2016 y su plan de precios de análisis de registros es *Premium*, a continuación, esta área de trabajo usa derechos de hello complemento de OMS para System Center. También puede usar los derechos cambiando toohello *OMS* nivel de precios.
>
>

derechos de suscripción de Hello OMS no son visibles en hello Azure o el portal de OMS. Puede ver los derechos y uso en hello Enterprise Portal.  

Si necesita toochange Hola suscripción de Azure que está vinculada el área de trabajo, puede usar hello Azure PowerShell [Move-AzureRmResource](https://msdn.microsoft.com/library/mt652516.aspx) cmdlet.

### <a name="using-azure-commitment-from-an-enterprise-agreement"></a>Uso del compromiso de Azure en contratos Enterprise
Si no tiene una suscripción de OMS, se paga por separado para cada componente de OMS y el uso de hello aparece en la factura de Azure.

Si tiene Azure compromiso monetario en hello enterprise inscripción toowhich están vinculadas a las suscripciones de Azure, uso de análisis de registros se débito automáticamente contra Hola restantes confirmación monetario.

Si necesita toochange hello suscripción de Azure que Hola área de trabajo está vinculada, puede usar hello Azure PowerShell [Move-AzureRmResource](https://msdn.microsoft.com/library/mt652516.aspx) cmdlet.  

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-azure-portal"></a>Cambiar un tooa de área de trabajo de tarifa de pago en hello portal de Azure
1. Inicio de sesión en hello [portal de Azure](http://portal.azure.com).
2. Busque **Log Analytics** y selecciónelo.
3. Aparecerá una lista con las áreas de trabajo existentes. Seleccione un área de trabajo.  
4. En la hoja de área de trabajo de hello, en **General**, haga clic en **tarifa**.  
5. En **Plan de tarifa**, seleccione un plan de tarifa y haga clic en **Seleccionar**.  
    ![seleccionar plan](./media/log-analytics-manage-access/manage-access-change-plan03.png)
6. Al actualizar la vista en hello portal de Azure, consulte **tarifa** actualizado para el nivel de Hola que seleccionó.  
    ![plan actualizado](./media/log-analytics-manage-access/manage-access-change-plan04.png)

> [!NOTE]
> Si el área de trabajo está vinculado tooan cuenta de automatización, antes de que se puede seleccionar hello *independiente (por GB)* tarifa debe eliminar cualquier **automatización y Control** soluciones y desvincular Hola automatización cuenta. En la hoja de área de trabajo de hello, en **General**, haga clic en **soluciones** soluciones toosee y delete. Hola toounlink cuenta de automatización, haga clic en nombre de Hola de hello cuenta de automatización en hello **tarifa** hoja.
>
>

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-oms-portal"></a>Cambiar un tooa de área de trabajo de tarifa de pago en el portal de OMS Hola

toochange Hola tarifa mediante Hola portal OMS, debe tener una suscripción de Azure.

1. En el portal de OMS de hello, haga clic en hello **configuración** icono.
2. Haga clic en hello **cuentas** ficha y, a continuación, haga clic en hello **suscripción de Azure y los datos del Plan** ficha.
3. Haga clic en hello desea toouse de nivel de precios.
4. Haga clic en **Guardar**.  
   ![suscripción y planes de datos](./media/log-analytics-manage-access/subscription-tab.png)

Su nuevo plan de datos se muestra en hello la cinta de opciones de portal de OMS en parte superior de saludo de la página web.

![cinta de opciones de OMS](./media/log-analytics-manage-access/data-plan-changed.png)


## <a name="change-how-long-log-analytics-stores-data"></a>Cambio de la duración del almacenamiento de datos de Log Analytics

En hello al nivel de precios gratis, análisis de registros hace Hola disponible últimos siete días de datos.
En el nivel de precios estándar de hello, análisis de registros hace disponible Hola últimos 30 días de datos.
En el nivel de precios Premium de hello, análisis de registros hace disponible Hola últimos 365 días de datos.
En hello independiente y OMS precios niveles, de forma predeterminada, análisis de registros hace disponible Hola últimos 31 días de datos.

Cuando usas Hola independiente y los niveles de precios de OMS, puede mantenerse too2 años de datos (730 días). Datos almacenados durante más tiempo que el valor predeterminado es Hola 31 días incurre en un cargo de retención de datos. Para más información sobre los precios, consulte [Costos del uso por encima del límite](https://azure.microsoft.com/pricing/details/log-analytics/).

longitud de hello toochange de retención de datos:

1. Inicio de sesión en hello [portal de Azure](http://portal.azure.com).
2. Busque **Log Analytics** y selecciónelo.
3. Aparecerá una lista con las áreas de trabajo existentes. Seleccione un área de trabajo.  
4. En la hoja de área de trabajo de hello en **General**, haga clic en **retención**.  
5. Utilizar tooincrease de control deslizante de Hola o reduzca Hola número de días de retención y, a continuación, haga clic en **guardar**.  
    ![Cambio de la retención](./media/log-analytics-manage-access/manage-access-change-retention01.png)

## <a name="change-an-azure-active-directory-organization-for-a-workspace"></a>Cambio de la organización de Azure Active Directory para un área de trabajo

Puede cambiar la organización de Azure Active Directory para un área de trabajo. Hola cambiante organización de Azure Active Directory le permite tooadd a los usuarios y grupos de esa área de trabajo de toohello de directorio.

### <a name="toochange-hello-azure-active-directory-organization-for-a-workspace"></a>Hola toochange organización de Azure Active Directory para un área de trabajo

1. En la página de configuración de hello en el portal de OMS hello, haga clic en **cuentas** y, a continuación, haga clic en hello **administrar usuarios** ficha.  
2. Revise la información de hello sobre cuentas organizativas y, a continuación, haga clic en **cambio organización**.  
    ![cambiar organización](./media/log-analytics-manage-access/manage-access-add-adorg01.png)
3. Escriba Hola información de identidad Hola Administrador de dominio de Active Directory de Azure. A continuación, verá una confirmación que indica que el área de trabajo está vinculado tooyour dominio de Active Directory de Azure.  
    ![confirmación de área de trabajo vinculada](./media/log-analytics-manage-access/manage-access-add-adorg02.png)


## <a name="delete-a-log-analytics-workspace"></a>Eliminación de un área de trabajo de Log Analytics
Al eliminar un área de trabajo de análisis de registros, todos los datos relacionados con el área de trabajo de tooyour se elimina de hello servicio OMS durante los 30 días.

Si es administrador y hay varios usuarios asociados con el área de trabajo de hello, se interrumpirá la asociación de hello entre dichos usuarios y el área de trabajo de Hola. Si los usuarios de hello están asociados a otras áreas de trabajo, podrán seguir usando OMS con las otras áreas de trabajo. No obstante, si no están asociados a otras áreas de trabajo deben toocreate un toouse de área de trabajo OMS.

### <a name="toodelete-a-workspace"></a>toodelete un área de trabajo
1. Inicio de sesión en hello [portal de Azure](http://portal.azure.com).
2. Busque **Log Analytics** y selecciónelo.
3. Aparecerá una lista con las áreas de trabajo existentes. Seleccione el área de trabajo de Hola que desee toodelete.
4. En la hoja de área de trabajo de hello, haga clic en **eliminar**.  
    ![delete](./media/log-analytics-manage-access/delete-workspace01.png)
5. Cuadro de diálogo de confirmación de hello Eliminar área de trabajo, haga clic en **Sí**.

## <a name="next-steps"></a>Pasos siguientes
* Vea [tooLog de equipos de Windows conectarse análisis](log-analytics-windows-agents.md) tooadd agentes y recopilar los datos.
* [Adición de soluciones de análisis de registros desde la Galería de soluciones de hello](log-analytics-add-solutions.md) tooadd funcionalidad y recopilar datos.
* [Configurar ajustes del proxy y firewall de análisis de registros](log-analytics-proxy-firewall.md) si su organización usa un servidor proxy o firewall para que los agentes puedan comunicarse con servicio de análisis de registros de hello.
