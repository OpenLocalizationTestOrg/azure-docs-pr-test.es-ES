---
title: portal de servicios Web de Azure Machine Learning hello aaaUse | Documentos de Microsoft
description: "Administrar el acceso a áreas de trabajo de aprendizaje automático de tooAzure, implementar y administrar los servicios web de API de aprendizaje automático"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: jhubbard
editor: cgronlun
ms.assetid: b62cf2ca-dd2a-4a83-bb54-469f948fb026
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: v-donglo
ms.openlocfilehash: 04b49027fc0ab227382b320310088bb66aafacc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-service-using-hello-azure-machine-learning-web-services-portal"></a>Administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning Hola
Puede administrar los servicios Web clásico y aprendizaje de máquina nueva mediante el portal de servicios Web de Microsoft Azure Machine Learning Hola. Dado que los servicios web clásicos y nuevos se basan en tecnologías subyacentes distintas, cada uno de ellos presenta funciones de administración ligeramente diferentes.

En el portal de servicios Web de aprendizaje de máquina de hello, puede:

* Supervisar cómo se usa el servicio web de Hola.
* Configurar la descripción de hello, actualizar las claves de hello web hello (solo para nuevo) de servicio, actualice su almacenamiento cuenta clave (sólo para el nuevo), habilitar el registro y habilitar o deshabilitar datos de ejemplo.
* Eliminar servicio web de Hola.
* Crear, eliminar o actualizar planes de facturación (solo en los nuevos)
* Agregar y eliminar puntos de conexión (solo en los clásicos)

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="permissions-toomanage-new-resources-manager-based-web-services"></a>Permisos toomanage nuevo administrador de recursos en función de los servicios web

Los nuevos servicios web se implementan como recursos de Azure. Por lo tanto, debe tener toodeploy de permisos correcto de Hola y administrar nuevos servicios web.  toodeploy o administrar los nuevos servicios web debe tener asignado un colaborador o se implementa el rol de administrador en el servicio web de hello suscripción toowhich Hola. Si se invitar a otra área de trabajo de aprendizaje de automático de tooa de usuario, debe asignarlos tooa rol Colaborador o administrador de suscripción de Hola para poder implementar o administrar los servicios web. 

Si Hola usuario no tiene Hola corregir recursos de tooaccess de permisos en el portal de servicios Web de Azure Machine Learning hello, recibirán Hola tras error al tratar de toodeploy un servicio web:

*Error de implementación de servicio web. Esta cuenta no tiene suficiente acceso toohello suscripción de Azure que contiene Hola área de trabajo. En orden toodeploy un tooAzure de servicio Web, debe ser la misma cuenta de hello invitó toohello área de trabajo y ser toohello de acceso determinada suscripción de Azure contiene Hola área de trabajo.*

Para obtener más información sobre cómo crear un área de trabajo, consulte cómo [crear y compartir un área de trabajo de Azure Machine Learning](machine-learning-create-workspace.md).

Para obtener más información sobre cómo establecer permisos de acceso, consulte [ver las asignaciones de acceso para usuarios y grupos en el portal de Azure - versión preliminar pública de hello](../active-directory/role-based-access-control-manage-assignments.md).


## <a name="manage-new-web-services"></a>Administración de servicios web nuevos
toomanage los servicios Web nuevo:

1. Inicie sesión en toohello [servicios Web de Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portal con su cuenta de Microsoft Azure - cuenta de hello de usuario que está asociado a Hola suscripción de Azure.
2. En el menú de hello, haga clic en **servicios Web**.

Se mostrará una lista de los servicios web implementados de la suscripción. 

toomanage un servicio Web, haga clic en servicios Web. Desde la página de servicios Web de hello hacer lo siguiente:

* Haga clic en toomanage de servicio web de Hola.
* Haga clic en hello Plan de facturación para hello web servicio tooupdate.
* Eliminar un servicio web
* Copiar un servicio web y lo implementará tooanother región.

Al hacer clic en un servicio web, abre la página de inicio rápido de servicio de hello web. página de inicio rápido del servicio de Hello web tiene dos opciones de menú que le permiten toomanage el servicio web:

* **PANEL** -permite el uso del servicio Web tooview.
* **CONFIGURAR** : le permite tooadd texto descriptivo, clave de actualización de Hola para asociados de cuenta de almacenamiento de Hola a Hola servicio Web y habilitar o deshabilitar datos de ejemplo.

### <a name="monitoring-how-hello-web-service-is-being-used"></a>Cómo se usa el servicio web de Hola de supervisión
Haga clic en hello **panel** ficha.

En el panel de hello, puede ver el uso general del servicio Web durante un período de tiempo. Puede seleccionar tooview período Hola desde el menú desplegable periodo de hello en la esquina superior derecha de Hola de gráficos de uso de Hola. panel de Hello muestra hello siguiente información:

* **Las solicitudes de un período** muestra un gráfico de paso del número de Hola de solicitudes Hola período de tiempo seleccionado. Puede ayudarlo a identificar si se están experimentando picos de uso.
* **Las solicitudes de solicitudes y respuestas** muestra hello número total de llamadas de solicitud-respuesta servicio Hola ha recibido a través hello período de tiempo seleccionado y no se pudo cuántos de ellos.
* **Promedio de tiempo de respuesta de solicitud de proceso** muestra un promedio de tiempo de hello necesarios tooexecute Hola recibe solicitudes.
* **Las solicitudes por lote** muestra hello el número total de servicio de Hola de solicitudes por lotes ha recibido a través Hola período de tiempo seleccionado y no se pudo cuántos de ellos.
* **Promedio de latencia de trabajo** muestra un promedio de tiempo de hello necesarios tooexecute Hola recibe solicitudes.
* **Errores** muestra agregación del número de errores que se han producido hello en el servicio web de llamadas a toohello.
* **Los costos de servicios** muestra hello cargos para el plan de facturación de hello asociado con el servicio de Hola.

### <a name="configuring-hello-web-service"></a>Configurar el servicio web de Hola
Haga clic en hello **configurar** opción de menú.

Puede actualizar Hola propiedades siguientes:

* **Descripción** permite tooenter una descripción para el servicio Web de Hola.
* **Título** permite tooenter un título para el servicio Web de Hola
* **Las claves** permite toorotate las claves de API principales y secundarias.
* **Clave de la cuenta de almacenamiento** permite tooupdate Hola clave Hola cuenta de almacenamiento asociada con los cambios de servicio Web de Hola. 
* **Habilitar los datos de ejemplo** permite tooprovide datos de ejemplo que puede usar tootest Hola respuesta de solicitud de servicio. Si ha creado el servicio web de hello en estudio de aprendizaje automático, datos de ejemplo de Hola procede de datos de hello su tootrain usa el modelo. Si ha creado el servicio de hello mediante programación, los datos de Hola se toman de los datos de ejemplo de Hola proporcionados como parte del paquete de hello JSON.

### <a name="managing-billing-plans"></a>Administración de planes de facturación
Haga clic en hello **planes** opción de menú de página de inicio rápido de hello web services. También puede hacer clic en plan Hola asociada toomanage de servicio Web específico que va.

* **Nueva** permite toocreate un nuevo plan.
* **Instancia de Plan de agregar o quitar** permite demasiado "escalar horizontalmente" una capacidad de tooadd de plan existente.
* **Actualizar o degradar** permite demasiado "escalar verticalmente" una capacidad de tooadd de plan existente.
* **Eliminar** permite toodelete un plan.

Haga clic en un plan tooview su panel. Hola panel proporciona el uso de instantáneas o plan durante un período de tiempo seleccionado. tooselect Hola tooview período de tiempo, haga clic en hello **período** lista desplegable situada en la esquina superior derecha del panel de Hola. 

panel de plan de Hello proporciona Hola siguiente información:

* **Descripción del plan** muestra información sobre los costos de Hola y capacidad asociados con el plan de Hola.
* **Planear el uso de** muestra hello número de transacciones y las horas de proceso que han realizado un cargo con respecto al plan de Hola.
* **Servicios Web** muestra el número de hello de servicios Web que usan este plan.
* **Principales por llamadas al servicio Web** muestra los servicios Web de hello cuatro principales que están realizando llamadas que se cobran con respecto al plan de Hola.
* **Principales servicios Web por horas de proceso** muestra los servicios Web de hello cuatro principales que usan los recursos del proceso que se cobran con respecto al plan de Hola.

## <a name="manage-classic-web-services"></a>Administración de servicios web clásicos
> [!NOTE]
> procedimientos de Hello en esta sección son servicios de web de clásico de toomanaging relevante a través del portal de servicios Web de Azure Machine Learning Hola. Para obtener información sobre la administración de Web clásico servicios a través de estudio de aprendizaje automático de Hola y Hola de Azure clásico portal, vea [administrar un área de trabajo de aprendizaje automático de Azure](machine-learning-manage-workspace.md).
> 
> 

toomanage los servicios Web clásico:

1. Inicie sesión en toohello [servicios Web de Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portal con su cuenta de Microsoft Azure - cuenta de hello de usuario que está asociado a Hola suscripción de Azure.
2. En el menú de hello, haga clic en **clásico servicios Web**.

Haga clic en un servicio Web clásico, toomanage **clásico servicios Web**. Desde la página de servicios Web clásico de hello hacer lo siguiente:

* Haga clic en puntos de conexión de hello web servicio tooview Hola asociado.
* Eliminar un servicio web

Al administrar un servicio Web clásico, administra cada uno de los extremos de Hola por separado. Al hacer clic en un servicio web en la página de servicios Web de hello, lista de Hola de puntos de conexión asociados con el servicio de Hola se abre. 

En la página de punto de conexión de servicio Web clásico de hello, puede agregar y eliminar puntos de conexión de servicio de Hola. Para más información sobre la incorporación de puntos de conexión, consulte [Creación de puntos de conexión](machine-learning-create-endpoint.md).

Haga clic en una página de inicio rápido del servicio de web de hello extremos tooopen Hola. En la página de inicio rápido de hello, hay dos opciones de menú que le permiten toomanage el servicio web:

* **PANEL** -permite el uso del servicio Web tooview.
* **CONFIGURAR** -permite tooadd texto descriptivo, activar el registro de error y desactivar clave de actualización de Hola para asociados de cuenta de almacenamiento de Hola a Hola servicio Web y habilitar y deshabilitar los datos de ejemplo.

### <a name="monitoring-how-hello-web-service-is-being-used"></a>Cómo se usa el servicio web de Hola de supervisión
Haga clic en hello **panel** ficha.

En el panel de hello, puede ver el uso general del servicio Web durante un período de tiempo. Puede seleccionar tooview período Hola desde el menú desplegable periodo de hello en la esquina superior derecha de Hola de gráficos de uso de Hola. panel de Hello muestra hello siguiente información:

* **Las solicitudes de un período** muestra un gráfico de paso del número de Hola de solicitudes Hola período de tiempo seleccionado. Puede ayudarlo a identificar si se están experimentando picos de uso.
* **Las solicitudes de solicitudes y respuestas** muestra hello número total de llamadas de solicitud-respuesta servicio Hola ha recibido a través hello período de tiempo seleccionado y no se pudo cuántos de ellos.
* **Promedio de tiempo de respuesta de solicitud de proceso** muestra un promedio de tiempo de hello necesarios tooexecute Hola recibe solicitudes.
* **Las solicitudes por lote** muestra hello el número total de servicio de Hola de solicitudes por lotes ha recibido a través Hola período de tiempo seleccionado y no se pudo cuántos de ellos.
* **Promedio de latencia de trabajo** muestra un promedio de tiempo de hello necesarios tooexecute Hola recibe solicitudes.
* **Errores** muestra agregación del número de errores que se han producido hello en el servicio web de llamadas a toohello.
* **Los costos de servicios** muestra hello cargos para el plan de facturación de hello asociado con el servicio de Hola.

### <a name="configuring-hello-web-service"></a>Configurar el servicio web de Hola
Haga clic en hello **configurar** opción de menú.

Puede actualizar Hola propiedades siguientes:

* **Descripción** permite tooenter una descripción para el servicio Web de Hola. La descripción es un campo obligatorio.
* **Registro** permite error tooenable o deshabilitar el registro en el extremo de Hola. Para obtener más información sobre el registro, consulte [Habilitación del registro para los servicios web Machine Learning](machine-learning-web-services-logging.md).
* **Habilitar los datos de ejemplo** permite tooprovide datos de ejemplo que puede usar tootest Hola respuesta de solicitud de servicio. Si ha creado el servicio web de hello en estudio de aprendizaje automático, datos de ejemplo de Hola procede de datos de hello su tootrain usa el modelo. Si ha creado el servicio de hello mediante programación, los datos de Hola se toman de los datos de ejemplo de Hola proporcionados como parte del paquete de hello JSON.

## <a name="grant-or-suspend-access-tooweb-services-for-users-in-hello-portal"></a>Conceder o suspender acceso tooWeb servicios para los usuarios en el portal de Hola
Hola portal de Azure clásico puede permitir o denegar el acceso a los usuarios de toospecific.

### <a name="access-for-users-of-new-web-services"></a>Acceso por parte de los usuarios de los servicios web nuevos
tooenable toowork de otros usuarios con los servicios Web en el portal de servicios Web de Azure Machine Learning hello, debe agregarlos como administradores de co en su suscripción de Azure.

Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com/) con su Microsoft Azure cuenta - usar cuenta de hello que esté asociada con hello suscripción de Azure.

1. En el panel de navegación de hello, haga clic en **configuración**, a continuación, haga clic en **administradores**.
2. En la parte inferior de Hola de ventana hello, haga clic en **agregar**. 
3. En el cuadro de diálogo ADD A CO-ADMINISTRATOR hello, escriba dirección de correo electrónico de Hola de persona Hola que desea tooadd como Coadministrador y suscripción hello, a continuación, seleccione que desea Hola tooaccess de coadministrador.
4. Haga clic en **Guardar**.

### <a name="access-for-users-of-classic-web-services"></a>Acceso por parte de los usuarios de servicios web clásicos
toomanage un área de trabajo:

Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com/) con su Microsoft Azure cuenta - usar cuenta de hello que esté asociada con hello suscripción de Azure.

1. En el panel de servicios de Microsoft Azure hello, haga clic en **aprendizaje automático**.
2. Haga clic en el área de trabajo de hello desee toomanage.
3. Haga clic en hello **configurar** ficha.

Desde la ficha de configuración de hello, puede suspender el área de trabajo de access toohello aprendizaje automático, haga clic en **DENY**. Los usuarios ya no estará tooopen capaz de área de trabajo hello en estudio de aprendizaje automático. acceso de toorestore, haga clic en **permitir**.

usuarios de toospecific:

toomanage cuentas adicionales que tengan acceso toohello área de trabajo en estudio de aprendizaje automático, haga clic en **inicio de sesión tooML Studio** en hello **panel** ficha. Se abre el área de trabajo de hello en estudio de aprendizaje automático. Desde aquí, haga clic en hello **configuración** ficha y, a continuación, **usuarios**. Puede hacer clic en **invitar a más usuarios** toogive a los usuarios tener acceso a área de trabajo de toohello, o seleccione un usuario y haga clic en **quitar**.

> [!NOTE]
> Hola **inicio de sesión tooML Studio** vínculo abre estudio de aprendizaje automático con hello Account Microsoft ha iniciado sesión en. Hola Account Microsoft utiliza toosign en toohello toocreate portal clásico un área de trabajo de Azure no automáticamente tiene permiso tooopen esa área de trabajo. tooopen un área de trabajo, debe iniciar sesión en toohello Account de Microsoft que se ha definido como propietario de hello del área de trabajo de Hola o necesita tooreceive una invitación de área de trabajo de hello propietario toojoin Hola.
> 
> 

