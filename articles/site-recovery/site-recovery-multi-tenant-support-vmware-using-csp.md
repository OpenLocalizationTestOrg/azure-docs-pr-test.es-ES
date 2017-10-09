---
title: "compatibilidad con aaaMulti inquilino tooAzure de replicación de VM de VMware (programa CSP) | Documentos de Microsoft"
description: "Describe cómo toodeploy Azure Site Recovery en un entorno de varios inquilinos tooorchestrate, conmutación por error y de recuperación de local tooAzure de máquinas virtuales (VM) de VMware a través del programa de hello CSP mediante el uso de hello portal de Azure"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: manayar
ms.openlocfilehash: 9be555c9a438f66e6d3dfcdc9f507a84763846d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-support-in-azure-site-recovery-for-replicating-vmware-virtual-machines-tooazure-through-csp"></a>Compatibilidad con varios inquilinos en Azure Site Recovery para la replicación de tooAzure de máquinas virtuales de VMware a través de CSP

Azure Site Recovery admite entornos multiinquilino en suscripciones de inquilino. También admite la arquitectura multiempresa para suscripciones de los inquilinos que se crean y administran a través del programa de proveedor de soluciones de nube de Microsoft (CSP) de Hola. En este artículo se detalla instrucciones Hola para implementar y administrar escenarios de VMware en Azure de varios inquilinos. También se describe la creación y la administración de suscripciones de inquilino mediante CSP.

Esta guía se dibuja con un alto grado de la documentación existente de Hola para replicar tooAzure de máquinas virtuales de VMware. Para obtener más información, consulte [tooAzure de máquinas virtuales de VMware replicar con Site Recovery](site-recovery-vmware-to-azure.md).

## <a name="multi-tenant-environments"></a>Entornos multiinquilino
Existen tres modelos principales multiinquilino:

* **Comparten el proveedor de servicios de alojamiento (HSP)**: asociado de hello posee la infraestructura física de Hola y usa recursos compartidos (vCenter, centros de datos, almacenamiento físico y así sucesivamente) toohost máquinas virtuales de varios inquilinos en Hola misma infraestructura. socio de Hello puede proporcionar administración de recuperación ante desastres como un servicio administrado o inquilino Hola puede ser propietario de la recuperación ante desastres como una solución de autoservicio.

* **Dedicado de proveedor de servicios de Hosting**: Hola asociado es el propietario de infraestructura física Hola pero utiliza recursos dedicados (varios vCenter, almacenes de datos físico y así sucesivamente) toohost las máquinas virtuales de cada inquilino en una infraestructura independiente. socio de Hello puede proporcionar administración de recuperación ante desastres como un servicio administrado o inquilino Hola puede poseer como una solución de autoservicio.

* **Administrar proveedores de servicios (MSP)**: cliente hello posee infraestructura física Hola que hospeda máquinas virtuales de Hola y asociado de hello proporciona administración y habilitación de la recuperación ante desastres.

## <a name="shared-hosting-multi-tenant-guidance"></a>Guía para entornos multiinquilino: hospedaje compartido
Esta sección trata el escenario de hospedaje compartido de hello en detalle. Hello otros dos escenarios son subconjuntos del escenario de hospedaje compartido de Hola y usan Hola mismos principios. Hola diferencias se describen final Hola de orientación de hospedaje compartido de Hola.

Hello requisito básico en un escenario de varios inquilinos es tooisolate Hola varios inquilinos. Un inquilino no debe ser capaz de tooobserve lo que tenga especificado hosted otro inquilino. En un entorno administrado por un asociado, este requisito no es tan importante como en el entorno de autoservicio, donde puede ser crítico. En esta guía se da por supuesto que se requiere el aislamiento de inquilinos.

arquitectura de Hola se presenta en hello siguiente diagrama:

![HSP compartido con un vCenter](./media/site-recovery-multi-tenant-support-vmware-using-csp/shared-hosting-scenario.png)  
**Escenario de hospedaje compartido con un vCenter**

Tal como se muestra en hello anterior diagrama, cada cliente tiene un servidor de administración independientes. Esta configuración límites inquilino acceso tootenant específico las máquinas virtuales y habilita el aislamiento de inquilinos. Un escenario de replicación de máquina virtual de VMware utiliza Hola Configuración servidor toomanage cuentas toodiscover máquinas virtuales e instalar agentes. Seguimos Hola mismos principios para entornos de varios inquilinos, con la adición de Hola de restringir la detección de máquina virtual a través de vCenter el control de acceso.

requisito de aislamiento de los datos de Hello necesita que toda la información confidencial de infraestructura (por ejemplo, las credenciales de acceso) se mantengan tootenants no revelado. Por este motivo, se recomienda que todos los componentes del servidor de administración de hello permanecen bajo control exclusivo de Hola de asociado de Hola. componentes del servidor de administración de Hello son:
* Servidor de configuración (CS)
* Servidor de proceso (PS)
* Servidor de destino maestro (MT) 

Un PS de escalado horizontal también está bajo control de hello asociado.

### <a name="every-cs-in-hello-multi-tenant-scenario-uses-two-accounts"></a>Cada CS en el escenario de varios inquilinos de hello usa dos cuentas

- **cuenta de acceso de vCenter**: usar este inquilino de toodiscover cuenta las máquinas virtuales. Tiene permisos de acceso de vCenter asignados tooit (como se describe en la sección siguiente de hello). toohelp evitar pérdidas de acceso accidental, se recomienda que socios escribir estas credenciales por sí mismos en la herramienta de configuración de Hola.

- **Cuenta de acceso de la máquina virtual**: Use este agente de movilidad de cuenta tooinstall hello en las máquinas virtuales de inquilinos de Hola a través de una inserción automática. Suele ser una cuenta de dominio que un inquilino puede proporcionar a tooa asociado o que, de forma alternativa, socio Hola puede administrar directamente. Si un inquilino no desea que los tooshare Hola detalles asociado de hello directamente, que se permita las credenciales de Hola de tooenter a través de un tiempo limitado acceso toohello CS o, con la asistencia del asociado de hello, instalación manualmente agentes de movilidad.

### <a name="requirements-for-a-vcenter-access-account"></a>Requisitos para una cuenta de acceso a vCenter

Como se mencionó en la sección anterior de hello, debe configurar Hola CS con una cuenta que tenga un tooit especial rol asignado. debe ser la asignación de roles de Hello aplican toohello vCenter cuenta de acceso para cada objeto de vCenter y no se propagan toohello los objetos secundarios. Esta configuración garantiza el aislamiento de inquilinos, ya que puede dar lugar a propagación de acceso en objetos de acceso accidental tooother.

![opción de objetos de propagar tooChild Hola](./media/site-recovery-multi-tenant-support-vmware-using-csp/assign-permissions-without-propagation.png)

alternativa de Hello es la cuenta de usuario de tooassign Hola y el rol en el objeto de centro de datos de Hola y propagarlos toohello los objetos secundarios. A continuación, dar cuenta de hello un *sin acceso* rol para cada objeto (por ejemplo, las máquinas virtuales de otros inquilinos) que se debe inquilino determinado tooa inaccesible. Esta configuración es complicada y expone controles de acceso accidental, dado que cada nuevo objeto secundario se concede acceso a los que se hereda del elemento primario de hello también automáticamente. Por lo tanto, se recomienda utilizar el primer enfoque de Hola.

procedimiento de acceso a la cuenta de Hello vCenter es como sigue:

1. Crear un nuevo rol mediante la clonación de hello predefinido *de sólo lectura* rol y, a continuación, asígnele un nombre adecuado (por ejemplo, Azure_Site_Recovery, tal como se muestra en este ejemplo).

2. Asignar Hola siguiendo el rol de toothis de permisos:

    * **Almacén de datos**: asignar espacio, examinar almacén de datos, operaciones de archivo de bajo nivel, quitar archivo, actualizar archivos de máquina virtual

    * **Red**: asignación de red

    * **Recursos**: grupo de tooresource asignar VM, migrar apagada la máquina virtual, migrar con Bing Maps en VM

    * **Tareas**: crear tarea, actualizar tarea

    * **Máquina virtual**: 
        * Configuración > Todos
        * Interacción > Responder a pregunta, Conexión de dispositivos, Configurar soporte de CD, Configurar soporte de disquete, Apagar, Encender, Instalación de herramientas de VMware
        * Inventario > Crear a partir de existente, Crear nuevo, Registrar, Anular registro
        * Máquina virtual > Permitir descarga de máquina virtual, Permitir carga de archivos de máquina virtual
        * Administración de instantáneas > Eliminar instantáneas

    ![cuadro de diálogo Editar rol Hola](./media/site-recovery-multi-tenant-support-vmware-using-csp/edit-role-permissions.png)

3. Asignar niveles toohello vCenter cuenta de acceso (que se usa en el inquilino de hello CS) diversos objetos, como sigue:

>| Objeto | Rol | Comentarios |
>| --- | --- | --- |
>| vCenter | Solo lectura | Necesita tener acceso solo vCenter tooallow para administrar los diferentes objetos. Puede quitar este permiso si nunca la cuenta de hello va toobe proporciona a tooa inquilino o usa para las operaciones de administración en hello vCenter. |
>| Centro de datos | Azure_Site_Recovery |  |
>| Host y clúster de hosts | Azure_Site_Recovery | Volver a garantiza que el acceso está en el nivel de objeto de hello, para que solo accesibles hosts tengan inquilino máquinas virtuales antes de la conmutación por error y después de la conmutación por recuperación. |
>| Almacén de datos y clúster de almacenes de datos | Azure_Site_Recovery | Igual que el anterior. |
>| Red | Azure_Site_Recovery |  |
>| Servidor de administración | Azure_Site_Recovery | Incluye componentes de acceso a tooall (CS, PS y MT) si alguno está fuera de la máquina de hello CS. |
>| Máquinas virtuales de inquilinos | Azure_Site_Recovery | Garantiza que cualquier inquilino nuevas máquinas virtuales de un inquilino determinado también obtendrá este acceso, o no podrán detectables a través de hello portal de Azure. |

acceso a la cuenta de Hello vCenter está ahora completo. Este paso cumple las operaciones de conmutación por recuperación de hello permisos mínimos requisito toocomplete. Estos permisos de acceso también pueden usarse con las directivas existentes. Sólo tiene que modificar los permisos de rol existente de tooinclude conjunto de permisos del paso 2, detallados anteriormente.

las operaciones de recuperación ante desastres de toorestrict hasta que el estado de conmutación por error de hello (es decir, sin las capacidades de conmutación por recuperación), siga Hola anterior procedimiento, con una excepción: en lugar de asignar Hola *Azure_Site_Recovery* rol cuenta de acceso de vCenter toohello, asigne solo un *de sólo lectura* toothat cuenta del rol. Este conjunto de permisos permite la replicación de máquinas virtuales y la conmutación por error, y no permite la conmutación por recuperación. Todo lo demás en hello anterior proceso permanece tal cual. tooensure aislamiento de inquilinos y restringir la detección de máquina virtual, todavía está asignado todos los permisos en objetos de nivel toochild únicamente y no propagado objeto Hola.

## <a name="other-multi-tenant-environments"></a>Otros entornos multiinquilino

Hola anterior sección se describe cómo tooset un entorno de varios inquilinos para una solución de hospedaje compartida. Hello otras dos soluciones principales son hospedaje dedicado y servicio administrado. arquitectura de Hola para estas soluciones se describe en las secciones siguientes de Hola.

### <a name="dedicated-hosting-solution"></a>Solución de hospedaje dedicado

Como se muestra en hello siguiente diagrama, diferencias de arquitectura de hello en una solución de hospedaje dedicada es que la infraestructura de cada inquilino está configurada para únicamente ese inquilino. Debido a los inquilinos están aislados a través de vCenter independiente, proveedor de hospedaje de hello debe seguir Hola CSP proporcionados los pasos para hospedaje compartido, pero no necesita tooworry sobre el aislamiento de inquilinos. La configuración del CSP permanece sin cambios.

![architecture-shared-hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/dedicated-hosting-scenario.png)  
**Escenario de hospedaje dedicado con varios vCenters**

### <a name="managed-service-solution"></a>Solución de servicios administrados

Como se muestra en hello siguiente diagrama, la diferencia de arquitectura de hello en una solución de servicio administrada es que la infraestructura de cada inquilino también es físicamente separada de la infraestructura de otros inquilinos. Este escenario normalmente existe al inquilino de hello es propietario de infraestructura de Hola y desea que una recuperación de desastres de toomanage de proveedor de soluciones. De nuevo, debido a los inquilinos están físicamente aislados a través de diferentes infraestructuras, socio Hola necesita toofollow Hola CSP proporcionan los pasos para hospedaje compartido pero no necesita tooworry sobre el aislamiento de inquilinos. El aprovisionamiento del CSP permanece sin cambios.

![architecture-shared-hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/managed-service-scenario.png)  
**Escenario de servicios administrados con varios vCenters**

## <a name="csp-program-overview"></a>Información general del programa CSP
Hola [programa CSP](https://partner.microsoft.com/en-US/cloud-solution-provider) fomenta el mejor juntos casos que ofrecen a los partners todos los servicios de nube de Microsoft, incluido Microsoft Azure, Office 365 y Enterprise Mobility Suite. Con CSP, nuestros partners poseen la relación de hello-to-end con los clientes y se convierten en punto de contacto de hello relación principal. Socios comerciales pueden implementar las suscripciones de Azure para los clientes y combinar las suscripciones de hello con sus propias ofertas de valor añadidos y personalizados.

Con Azure Site Recovery, asociados pueden administrar la solución completa de recuperación ante desastres de Hola para los clientes directamente a través de CSP. O bien, puede usar CSP tooset entornos de Site Recovery y permiten a los clientes administrar sus propias necesidades de recuperación ante desastres de una manera de autoservicio. En ambos escenarios, asociados son enlace Hola entre recuperación del sitio y sus clientes. Asociados de relación entre el cliente Hola de servicio y facturar a los clientes para el uso de Site Recovery.

## <a name="create-and-manage-tenant-accounts"></a>Creación y administración de cuentas de inquilino

### <a name="step-0-prerequisite-check"></a>Paso 0: Comprobación de requisitos previos

Hello requisitos previos de la máquina virtual se Hola mismo tal y como se describe en hello [documentación de Azure Site Recovery](site-recovery-vmware-to-azure.md). En los requisitos previos de suma toothose, debe haber Hola controles de acceso mencionadas en su lugar antes de continuar con la administración de inquilinos a través de CSP. Para cada inquilino, cree un servidor de administración independientes que puede comunicarse con las máquinas virtuales de inquilinos de Hola y vCenter del socio. Socio de hello solo tiene servidor de toothis de derechos de acceso.

### <a name="step-1-create-a-tenant-account"></a>Paso 1: Creación de una cuenta de inquilino

1. A través de [Microsoft Partner Center](https://partnercenter.microsoft.com/), inicie sesión en la cuenta de tooyour CSP. 
 
2. En hello **panel** menú, seleccione **clientes**.

    ![vínculo de los clientes de Microsoft Partner Center Hola](./media/site-recovery-multi-tenant-support-vmware-using-csp/csp-dashboard-display.png)

3. En la página Hola que se abre, haga clic en hello **Agregar cliente** botón.

    ![botón Add Customer de Hola](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-new-customer.png)

4. En hello **nuevo cliente** página, rellene los detalles de información de la cuenta de hello para el inquilino de hello y, a continuación, haga clic en **siguiente: suscripciones**.

    ![página de información de la cuenta de Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-add-filled.png)

5. En la página de selección de las suscripciones de hello, seleccione hello **Microsoft Azure** casilla de verificación. Puede agregar otras suscripciones ahora o en cualquier otro momento.

    ![casilla de verificación de suscripción de Microsoft Azure Hola](./media/site-recovery-multi-tenant-support-vmware-using-csp/azure-subscription-selection.png)

6. En hello **revisión** página, confirme los detalles de inquilino de hello y, a continuación, haga clic en **enviar**.

    ![página de revisión de Hola](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-summary-page.png)  

    Después de crear cuenta de inquilino de hello, aparece una página de confirmación, mostrar detalles de Hola de hello cuenta predeterminada y Hola contraseña para esa suscripción. 

7. Guardar información de Hola y cambiar la contraseña de hello más tarde según sea necesario a través de hello Azure página de inicio de sesión en portal.  
 
    Puede compartir esta información con el inquilino de hello tal cual, o puede crear y compartir una cuenta independiente si es necesario.

### <a name="step-2-access-hello-tenant-account"></a>Paso 2: Obtener acceso a la cuenta de inquilino de Hola

Puede tener acceso a suscripción del inquilino de Hola a través de hello panel del centro de Partner de Microsoft, como se describe en "paso 1: crear una cuenta de inquilino." 

1. Vaya toohello **clientes** página y, a continuación, haga clic en hello nombre de cuenta de inquilino de Hola.

2. En hello **suscripciones** página de cuenta de inquilino de hello, puede supervisar las suscripciones de cuenta existente de Hola y agregar varias suscripciones, según sea necesario. Seleccione las operaciones de recuperación ante desastres del inquilino de toomanage hello, **todos los recursos (portal de Azure)**.

    ![vínculo de todos los recursos de Hola](./media/site-recovery-multi-tenant-support-vmware-using-csp/all-resources-select.png)  
    
    Haga clic en **todos los recursos** concede acceso suscripciones de Azure del inquilino de toohello. Puede comprobar el acceso haciendo clic en el vínculo de Azure Active Directory de hello en hello esquina superior derecha del programa Hola a portal de Azure.

    ![Vínculo de Azure Active Directory](./media/site-recovery-multi-tenant-support-vmware-using-csp/aad-admin-display.png)

Ahora puede realizar todas las operaciones de recuperación del sitio de inquilino de Hola a través del portal de Azure de Hola y administrar las operaciones de recuperación ante desastres de Hola. suscripción de inquilino de hello tooaccess a través de CSP para recuperación ante desastres administrado, seguimiento Hola descrito anteriormente proceso.

### <a name="step-3-deploy-resources-toohello-tenant-subscription"></a>Paso 3: Implementar la suscripción de inquilino de toohello de recursos
1. En hello portal de Azure, crear un grupo de recursos y, a continuación, implemente un almacén de servicios de recuperación por el proceso habitual de Hola. 
 
2. Descargue la clave de registro del almacén de Hola.

3. Registrar CS hello para el inquilino de hello mediante el uso de clave de registro del almacén de Hola.

4. Escriba las credenciales de Hola para cuentas de acceso de hello dos: cuenta de acceso de vCenter y VM acceder a la cuenta.

    ![Cuentas de servidor de Configuration Manager](./media/site-recovery-multi-tenant-support-vmware-using-csp/config-server-account-display.png)

### <a name="step-4-register-site-recovery-infrastructure-toohello-recovery-services-vault"></a>Paso 4: Infraestructura de recuperación del sitio de registro de servicios de recuperación de toohello almacén
1. En Hola portal de Azure, en el almacén de Hola que creó anteriormente, registre Hola vCenter server toohello CS que registró en el "paso 3: implementar la suscripción de recursos de inquilino toohello." Usar cuenta de acceso de hello vCenter para este propósito.
2. Finalizar el proceso de "Preparar la infraestructura" de hello para la recuperación del sitio por proceso habitual de Hola.
3. máquinas virtuales de Hola ahora están listo toobe replicado. Compruebe que solo hello máquinas virtuales del inquilino se muestran en hello **seleccionar las máquinas virtuales** hoja en hello **replicar** opción.

    ![Lista de las máquinas virtuales de inquilino en la hoja de hello seleccione las máquinas virtuales](./media/site-recovery-multi-tenant-support-vmware-using-csp/tenant-vm-display.png)

### <a name="step-5-assign-tenant-access-toohello-subscription"></a>Paso 5: Asignar acceso toohello suscripción de inquilino

Recuperación ante desastres de autoservicio, proporcionar toohello inquilino detalles de la cuenta de hello, como se mencionó en el paso 6 de hello "paso 1: crear una cuenta de inquilino" sección. Realice esta acción después de socio de hello configura la infraestructura de recuperación ante desastres de Hola. Si el tipo de recuperación ante desastres de hello es administrado o de autoservicio, socios deben tener acceso a las suscripciones del inquilino a través del portal CSP Hola. Que configuración el almacén de propiedad asociado hello y registra las suscripciones de inquilinos de toohello de infraestructura.

Asociados de negocios también pueden agregar una nueva suscripción de inquilino de toohello de usuario a través del portal CSP Hola haciendo Hola siguiente:

1. Ir a página de suscripción de CSP del inquilino de toohello y, a continuación, seleccione hello **usuarios y licencias** opción.

    ![Hola página de suscripción del inquilino CSP](./media/site-recovery-multi-tenant-support-vmware-using-csp/users-and-licences.png)

    Ahora puede crear un nuevo usuario especificando detalles pertinentes de Hola y seleccionar permisos o Cargando lista de Hola de usuarios en un archivo CSV.

2. Después de crear un nuevo usuario, volver toohello Azure portal y, a continuación, en hello **suscripción** hoja, suscripción relevante Hola select.

3. En la hoja de Hola que se abre, seleccione **Control de acceso (IAM)**y, a continuación, haga clic en **agregar** tooadd un usuario con el nivel de acceso relevante Hola.      
    usuarios Hola que se crearon a través del portal CSP de Hola se muestran automáticamente en la hoja de Hola que se abre al hacer clic en un nivel de acceso.

    ![Adición de un usuario](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-user-subscription.png)

    Para la mayoría de las operaciones de administración, Hola *colaborador* rol es suficiente. Un usuario con este nivel de acceso puede hacerlo todo en una suscripción, excepto cambiar los niveles de acceso (para lo cual se necesita el nivel de acceso de *Propietario*). También puede ajustar los niveles de acceso de hello según sea necesario.
