---
title: roles de Control de acceso basado en roles personalizados aaaCreate y asignar toointernal y los usuarios externos de Azure | Documentos de Microsoft
description: Asignar roles personalizados de RBAC creados con PowerShell y la CLI para usuarios internos y externos
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a>Introducción al control de acceso basado en roles

Control de acceso basado en roles es una característica sola portal Azure permitir a los propietarios de Hola de una suscripción tooassign roles granulares tooother quienes pueden administrar ámbitos de recurso específico en su entorno.

RBAC permite una mejor administración de seguridad para las organizaciones grandes y para PYMES trabajar con colaboradores externos, proveedores o autónomos que necesitan tener acceso a recursos de toospecific en su entorno, pero no necesariamente toda la infraestructura de toohello o cualquier ámbitos relacionados con la facturación. RBAC ofrece flexibilidad de Hola de propietario de una suscripción de Azure administrada por la cuenta de administrador de hello (rol de administrador de servicio en un nivel de suscripción) y haber varios toowork usuarios invitados en Hola misma suscripción pero sin cualquier administrativas derechos para él. Desde una perspectiva de facturación y administración, característica RBAC Hola demuestra toobe una opción eficaz administración y tiempo para el uso de Azure en distintos escenarios.

## <a name="prerequisites"></a>Requisitos previos
El uso de RBAC en hello entorno de Azure requiere:

* Tener una independiente de suscripción de Azure toohello usuario asignado como propietario (rol de suscripción)
* Tiene el rol de propietario de Hola de hello suscripción de Azure
* Tener acceso toohello [portal de Azure](https://portal.azure.com)
* Asegúrese de que hello toohave después de proveedores de recursos registrado para la suscripción de usuario de hello: **Microsoft.Authorization**. Para obtener más información sobre cómo tooregister Hola proveedores de recursos, consulte [proveedores del Administrador de recursos, regiones, versiones de API y esquemas](/azure-resource-manager/resource-manager-supported-services.md).

> [!NOTE]
> Las suscripciones de Office 365 o licencias de Azure Active Directory (por ejemplo: obtener acceso a Active Directory tooAzure) aprovisionado desde Hola Office 365 portal no calidad usar RBAC.

## <a name="how-can-rbac-be-used"></a>Uso de RBAC
RBAC puede aplicarse en tres ámbitos diferentes de Azure. De hello mayor ámbito toohello más baja, son las siguientes:

* Suscripción (más alto)
* Grupos de recursos
* Ámbito de recursos (Hola menor nivel de acceso oferta permisos destino tooan ámbito de recursos individuales de Azure)

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a>Asignar roles RBAC en el ámbito de la suscripción de Hola
Hay dos ejemplos comunes (entre otros) en los que se utiliza RBAC:

* Tener usuarios externos de organizaciones de hello (que no forma parte del inquilino de Azure Active Directory del usuario del Administrador de hello) invitó toomanage determinados recursos o suscripción todo Hola
* Trabajar con los usuarios dentro de la organización de hello (forman parte del inquilino de Azure Active Directory del usuario de hello), pero parte de los distintos equipos o grupos que necesiten acceso granular cualquier toohello suscripción completa o grupos de recursos de toocertain o el recurso ámbitos Hola entorno de

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a>Conceder acceso en el nivel de suscripción para un usuario fuera de Azure Active Directory
Solo se pueden conceder roles RBAC **propietarios** de suscripción de hello, por tanto, el usuario de administrador de hello debe haber iniciado con un nombre de usuario que tiene este rol asignado previamente o creó Hola suscripción de Azure.

De hello portal de Azure, después de iniciar sesión como administrador, seleccione "Suscripciones" y seleccione Hola habían deseado uno.
![hoja de suscripción en el portal de Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) de forma predeterminada, si ha adquirido el usuario de administrador de Hola Hola suscripción de Azure, usuario Hola se mostrará como **Administrador de la cuenta**, que se va a rol de la suscripción de Hola. Para obtener más detalles sobre las funciones de suscripción de Azure de hello, consulte [agregar o cambiar roles de administrador de Azure que administran la suscripción de Hola o servicios](/billing/billing-add-change-azure-subscription-administrator.md).

En este ejemplo, Hola usuario "alflanigan@outlook.com" es hello **propietario** de hello "Gratuita" suscripción en hello AAD inquilinos "Default inquilino de Azure". Puesto que este usuario es el creador de Hola de hello suscripción de Azure con hello inicial Account de Microsoft "Outlook" (Microsoft Account = Outlook, etc. en vivo) será el nombre de dominio predeterminado de Hola para todos los demás usuarios que agregó en este inquilino **"@alflaniganuoutlook.onmicrosoft.com"**. De forma predeterminada, sintaxis de Hola de nuevo dominio de hello está formado por que reúnan Hola nombre de usuario y nombre de dominio del usuario de Hola que creó el inquilino de Hola y Agregar extensión de hello **". onmicrosoft.com"**.
Además, los usuarios pueden iniciar sesión con un nombre de dominio personalizado en el inquilino de hello después de agregar y comprobar de nuevo inquilino de Hola. Para obtener más detalles sobre cómo tooverify un nombre de dominio personalizado en un inquilino de Azure Active Directory, vea [agregar un directorio de tooyour de nombre de dominio personalizado](/active-directory/active-directory-add-domain).

En este ejemplo, el directorio de Hola "inquilino predeterminado Azure" contiene solo los usuarios con el nombre de dominio de Hola "@alflanigan.onmicrosoft.com".

Después de seleccionar la suscripción de hello, debe hacer clic en el usuario de administrador de hello **Control de acceso (IAM)** y, a continuación, **agregar un nuevo rol**.





![Característica de control de acceso IAM en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![Agregar un nuevo usuario en la característica de control de acceso IAM en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

Hola siguiente paso es tooselect Hola rol toobe asignado y usuario de Hola que se asignará el rol RBAC Hola a. Hola **rol** usuario de administrador de Hola de menú desplegable ve solo Hola RBAC funciones integradas que están disponibles en Azure. Para obtener explicaciones detalladas de cada rol y sus ámbitos asignables, consulte [Roles integrados en el control de acceso basado en roles de Azure](/active-directory/role-based-access-built-in-roles.md).

usuario de administrador de Hello, a continuación, debe tooadd dirección de correo electrónico de Hola de usuario externo Hola. Hola espera comportamiento es Hola usuario externo toonot aparecen en hello existente inquilino. Una vez se ha invitado usuario externo hello, estarán visible en **suscripciones > Control de acceso (IAM)** con todos los usuarios actuales de Hola que están asignados actualmente a un rol de RBAC en hello ámbito de la suscripción.





![Agregar permisos toonew RBAC rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![Lista de roles RBAC en el nivel de suscripción](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

usuario Hola "chessercarlton@gmail.com" se ha invitado toobe una **propietario** para suscripción de "Prueba gratuita" hello. Después de enviar la invitación de hello, usuario externo Hola recibirá una confirmación por correo electrónico con un vínculo de activación.
![invitación por correo electrónico para el rol de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)

Que se va a organización toohello externo, Hola nuevo usuario no tiene los atributos existentes en el directorio de "Default inquilino de Azure" Hola. Se creará una vez que concede al usuario externo de hello toobe de consentimiento que se registran en el directorio Hola que está asociado a la suscripción de Hola que se ha asignado un rol para.





![Mensaje de invitación por correo electrónico para el rol de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

usuario externo Hello muestra de Hola inquilino de Azure Active Directory de ahora en adelante como usuario externo y se puede ver en hello portal de Azure y en el portal clásico de Hola.





![Hoja de usuarios de Azure Active Directory en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![Hoja de usuarios de Azure Active Directory en el Portal de Azure clásico](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

Hola **usuarios** vista en ambos usuarios externos de portales Hola puede ser reconocida por:

* tipo de icono diferente de Hola Hola portal de Azure
* Hola diferente subcontratación punto en el portal clásico de Hola

Sin embargo, conceder **propietario** o **colaborador** usuario externo de acceso tooan en hello **suscripción** ámbito, no permite que el directorio del usuario de administrador de hello acceso toohello, a menos que hello **administrador Global** lo permite. En Propiedades del usuario hello, Hola **usuario tipo** que tiene dos parámetros comunes, **miembro** y **invitado** pueden identificarse. Un miembro es un usuario que está registrado en el directorio de hello mientras un invitado es un directorio de toohello de usuario invitado desde un origen externo. Para más información, consulte [¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?](/active-directory/active-directory-b2b-admin-add-users)

> [!NOTE]
> Asegúrese de que, después de escribir las credenciales de hello en el portal de hello, usuario externo Hola selecciona directorio correcto de hello toosign en. Hello mismo usuario puede tener acceso toomultiple directorios y puede seleccionar cualquiera de ellas haciendo clic en el nombre de usuario de hello en el lado derecho superior de Hola Hola portal de Azure y, a continuación, elija directorio adecuado de hello en lista de desplegable de Hola.

Al que se va a un invitado en el directorio de hello, usuario externo Hola puede administrar todos los recursos para hello suscripción de Azure, pero no puede obtener acceso a directorio Hola.





![portal de Azure active directory acceso restringido tooazure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

Azure Active Directory y una suscripción de Azure no tienen una relación de primario-secundario como tienen otros recursos de Azure (por ejemplo: las máquinas virtuales, las redes virtuales, las aplicaciones web, el almacenamiento, etc.) en una suscripción de Azure. Todos Hola este último se crea, administra y factura en una suscripción de Azure, mientras que una suscripción de Azure es toomanage usado Hola acceso tooan directorio de Azure. Para obtener más información, consulte [suscripción de Azure cómo está relacionado tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).

Todas las funciones RBAC de hello integrados, **propietario** y **colaborador** ofrecen acceso a la administración completa tooall recursos en entorno de hello, Hola diferencia es que no se puede crear un colaborador y delete nueva Funciones RBAC. Hello otras funciones integradas, como **colaborador de la máquina Virtual** ofrecen acceso a la administración completa únicamente los recursos de toohello indicados por el nombre de hello, independientemente de hello **grupo de recursos** se están creando a.

Rol Hola RBAC integrado asignación de **colaborador de la máquina Virtual** en un nivel de suscripción, significa que ese rol de Hola Hola asignados al usuario:

* Puede ver todas las máquinas virtuales independientemente de sus implementación hello y fecha de grupos de recursos que forman parte de
* Tiene máquinas virtuales de administración completa acceso toohello de suscripción de Hola
* No se puede ver otros tipos de recursos de suscripción de Hola
* No puede realizar ningún cambio desde la perspectiva de facturación.

> [!NOTE]
> Que se va a una característica única portal Azure de RBAC, no concede portal clásico de toohello de acceso.

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a>Asignar a un usuario externo de RBAC rol tooan integrado
Para un escenario diferente en esta prueba, Hola usuario externo "alflanigan@gmail.com" se agrega como un **colaborador de la máquina Virtual**.




![Rol integrado de colaborador de la máquina virtual](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

el comportamiento normal de este usuario externo a este rol integrada de Hello es toosee y administrar solo las máquinas virtuales y su adyacentes Administrador de recursos solo recursos necesario al implementar. De forma predeterminada, estos roles limitados proporcionan acceso solo tootheir de recursos correspondiente creados en hello portal de Azure, a pesar de todo algunos todavía se pueden implementar en el portal de clásico de hello (por ejemplo: máquinas virtuales).





![Información general sobre el rol de colaborador de la máquina virtual en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a>Conceder acceso en un nivel de suscripción de un usuario en hello mismo directorio
flujo del proceso de Hello es idéntico tooadding un usuario externo, tanto de hello perspectiva concediendo Hola RBAC el rol Administrador, así como usuario Hola se concede el rol de acceso toohello. Hola diferencia es que el usuario invitado de hello no recibirán las invitaciones de correo electrónico ya que todos los ámbitos de recursos de hello dentro de suscripción de hello estarán disponibles en el panel de hello tras iniciar sesión en.

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a>Asignar roles RBAC en el ámbito de grupo de recursos de Hola
Asignar un rol de RBAC en una **grupo de recursos** ámbito tiene un proceso idéntico para la asignación de rol de hello en nivel de suscripción de hello, para ambos tipos de usuarios: internos o externos (parte de hello mismo directorio). Hola a los usuarios que se asignan roles RBAC hello es toosee en su entorno solo el grupo de recursos de hello les ha asignado acceso de hello **grupos de recursos** icono Hola portal de Azure.

## <a name="assign-rbac-roles-at-hello-resource-scope"></a>Asignar roles RBAC en el ámbito de recursos de Hola
Asignar un rol RBAC en un ámbito de recursos en Azure tiene un proceso idéntico para la asignación de rol de hello en nivel de suscripción de Hola o en el nivel de grupo de recursos de hello, siguiente Hola mismo flujo de trabajo para ambos escenarios. Una vez más, los usuarios de Hola que se asignan roles RBAC Hola pueden ver únicamente los elementos de Hola que les ha asignado acceso a cualquier hello en **todos los recursos** ficha o directamente en su panel.

Es un aspecto importante de RBAC tanto en el ámbito de grupo de recursos o ámbito de recursos para el directorio correcto de hello usuarios toomake seguro toosign de toohello.





![Inicio de sesión en un directorio en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a>Asignación de roles de RBAC en un grupo de Azure Active Directory
Todos los escenarios de hello mediante RBAC en tres ámbitos diferentes hello en los privilegios de Hola de oferta de Azure de administrar, implementar y administrar diversos recursos como un usuario asignado sin Hola de necesitan de la administración de una suscripción personal. Se asigna el rol RBAC de hello sin tener en cuenta para una suscripción, el grupo de recursos o el ámbito de recursos, todos los recursos de hello creados más adelante los usuarios de hello asignado se facturan en hello una suscripción de Azure donde los usuarios de hello tienen acceso a. De esta manera, hello los usuarios que tienen permisos de administrador para esa suscripción de Azure completo de facturación tiene información general completa en el consumo de hello, sin tener en cuenta que va a administrar recursos de Hola.

Para las organizaciones grandes, se pueden aplicar funciones RBAC en hello igual en grupos de Azure Active Directory teniendo en cuenta la perspectiva de hello ese usuario de administrador de hello desea acceso granular de toogrant Hola para equipos o departamentos completos, no individualmente para cada usuario, por lo tanto teniendo en cuenta, como mucho tiempo y la administración eficaz opción. tooillustrate este ejemplo, hello **colaborador** rol se ha agregado tooone de grupos de hello en el inquilino de hello en nivel de suscripción de Hola.





![Agregar rol de RBAC para grupos de AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

Estos grupos son grupos de seguridad que se aprovisionan y administran únicamente dentro de Azure Active Directory.

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a>Crear un tooopen compatibilidad personalizada de RBAC rol solicitudes mediante PowerShell
Hola integrada RBAC las funciones que están disponibles en Azure Asegúrese de determinados niveles de permiso basados en los recursos disponibles en el entorno de Hola Hola. Sin embargo, si ninguno de estos roles se ajustan a las necesidades del usuario del Administrador de hello, hay acceso de toolimit de opción de hello aún más mediante la creación de roles personalizados de RBAC.

Crear roles personalizados de RBAC requiere tootake un rol integrado, modificarlo y, a continuación, importarlo en el entorno de Hola. descarga de Hola y la carga de rol de Hola se administran mediante PowerShell o CLI.

Es importante toounderstand Hola requisitos previos de creación de una función personalizada que pueden conceder acceso granular en nivel de suscripción de Hola y también permiten Hola invitado usuario Hola flexibilidad de abrir solicitudes de soporte técnico.

Para este rol integradas de ejemplo Hola **lector** que permite a los usuarios acceso tooview todos los recursos de hello ámbitos pero no tooedit o crear nuevos ha sido personalizado tooallow Hola Hola opción de usuario de las solicitudes de soporte técnico de apertura.

Hola la primera acción de exportación de hello **lector** rol necesidades toobe completado en PowerShell se ejecutaron con permisos elevados como administrador.

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Captura de pantalla de PowerShell para el rol Lector de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

A continuación, debe tooextract plantilla JSON Hola de rol de Hola.





![Plantilla JSON para el rol personalizado Lector de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

Un rol de RBAC típico se compone de tres secciones principales, **Actions**, **NotActions** y **AssignableScopes**.

Hola **acción** sección se enumeran todas las operaciones permitidas para este rol de Hola. Es importante toounderstand que se asigna cada acción desde un proveedor de recursos. En este caso, para crear Hola de incidencias de soporte técnico **Microsoft.Support** debe aparecer el proveedor de recursos.

toobe puede toosee Hola a todos los proveedores de recursos disponibles y registrados en su suscripción, puede usar PowerShell.
```
Get-AzureRMResourceProvider

```
Además, puede comprobar para hello todos Hola disponible PowerShell cmdlets toomanage Hola proveedores de recursos.
    ![Captura de pantalla de PowerShell para la administración de proveedores de recursos](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)

toorestrict todos Hola acciones para un rol determinado de RBAC, recursos proveedores aparecen en la sección de hello **NotActions**.
Por último, es obligatorio que ese rol RBAC hello contiene suscripción explícita Hola identificadores que se utiliza. Hello Id. de suscripción aparecen en hello **AssignableScopes**, en caso contrario no se permitirán rol de hello tooimport en su suscripción.

Después de crear y personalizar Hola RBAC rol, debe toobe entorno de hello atrás importados.

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

En este ejemplo, nombre personalizado de Hola para este rol RBAC es "Reader soporte vales nivel de acceso" Permitir Hola usuario tooview todo en suscripción de Hola y también las solicitudes de soporte técnico de tooopen.

> [!NOTE]
> son Hello solo dos funciones RBAC integradas que permiten acción Hola de apertura de solicitudes de soporte técnico **propietario** y **colaborador**. Para una solicitud de soporte de usuario toobe tooopen capaz de debe asignarse un rol RBAC solo en el ámbito de la suscripción de hello, ya que todas las solicitudes de soporte técnico se crean en función de una suscripción de Azure.

Este nuevo rol de seguridad se ha asignado el usuario tooan de hello mismo directorio.





![captura de pantalla de roles personalizados de RBAC importó Hola portal de Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![captura de pantalla de asignación personalizada importada RBAC rol toouser Hola mismo directorio](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![Captura de pantalla de los permisos de un rol importado personalizado de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

ejemplo de Hola ha sido aún más detallada tooemphasize Hola límites de este rol RBAC personalizado como se indica a continuación:
* Puede crear nuevas solicitudes de soporte técnico
* No puede crear nuevos ámbitos de recursos (por ejemplo: máquinas virtuales)
* No puede crear nuevos grupos de recursos





![Captura de pantalla de un rol personalizado de RBAC que puede crear solicitudes de soporte técnico](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![captura de pantalla de funciones RBAC personalizado no se puede toocreate máquinas virtuales](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![captura de pantalla de funciones RBAC personalizado no se puede toocreate RGs nueva](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a>Crear un tooopen compatibilidad personalizada de RBAC rol solicitudes mediante la CLI de Azure
La ejecución en un equipo Mac y sin necesidad de acceso tooPowerShell, CLI de Azure es Hola forma toogo.

Hola pasos toocreate un rol personalizado son Hola igual, con excepción de hello único que usan CLI rol hello no se pueden descargar en una plantilla JSON, pero puede verse en hello CLI.

En este ejemplo he elegido rol integrado de Hola de **lector de copia de seguridad**.

```

azure role show "backup reader" --json

```





![Captura de pantalla de la CLI que muestra un rol de lector de copia de seguridad](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

Editar rol hello en Visual Studio después de copiar propiedades de hello en una plantilla JSON, Hola **Microsoft.Support** proveedor de recursos se ha agregado en hello **acciones** secciones para que puedan abrir este usuario solicitudes de soporte técnico mientras continúa toobe un lector para almacenes de copia de seguridad de Hola. Nuevo es Id. de suscripción de hello tooadd necesarios donde se usará este rol en hello **AssignableScopes** sección.

```

azure role create --inputfile <path>

```





![Captura de pantalla de la CLI con la importación de un rol personalizado de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

nuevo rol de Hello ahora está disponible en hello portal de Azure y proceso de assignation Hola Hola mismo como en ejemplos anteriores Hola.





![Captura de pantalla de Azure Portal de un rol personalizado de RBAC creado con la CLI 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

A partir de hello 2017 de compilación más reciente, Hola Shell en la nube de Azure está generalmente disponible. Shell de nube de Azure es un complemento tooIDE y Hola Portal de Azure. Con este servicio, tiene un shell basado en explorador, autenticado y hospedado en Azure, que puede usar en lugar de la CLI instalada en su equipo.





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
