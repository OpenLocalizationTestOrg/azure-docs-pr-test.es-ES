---
title: "aaaSecuring los datos almacenados en el almacén de Azure Data Lake | Documentos de Microsoft"
description: "Obtenga información acerca de cómo listas de control de datos de toosecure en el almacén de Data Lake de Azure con grupos y acceso"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ca35e65f-3986-4f1b-bf93-9af6066bb716
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 2b4ed7e322e1843ca47d6968ec8801ac19ea6399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="securing-data-stored-in-azure-data-lake-store"></a>Protección de los datos almacenados en el Almacén de Azure Data Lake
Para proteger los datos en el Almacén de Azure Data Lake, se adopta un enfoque de tres pasos.

1. Comience creando grupos de seguridad en Azure Active Directory (AAD). Se utilizan estos grupos de seguridad tooimplement control de acceso basado en roles (RBAC) en el Portal de Azure. Para obtener más información, consulte [Control de acceso basado en roles de Azure Active Directory](../active-directory/role-based-access-control-configure.md).
2. Asigne grupos de seguridad de hello AAD toohello almacén de Azure Data Lake cuenta. Esta propiedad controla cuenta de almacén de Data Lake toohello de acceso de operaciones de portal de administración de Hola desde el portal de Hola o las API.
3. Asignar a grupos de seguridad AAD de hello como las listas de control de acceso (ACL) en el sistema de archivos de almacén de Data Lake Hola.
4. Además, también puede establecer un intervalo de direcciones IP para los clientes que pueden tener acceso a datos de hello en el almacén de Data Lake.

Este artículo proporciona instrucciones sobre cómo toouse Hola Hola tooperform portal Azure por encima de las tareas. Para obtener información detallada sobre cómo almacén de Data Lake implementa la seguridad en nivel de datos y cuenta de hello, consulte [seguridad en el almacén de Azure Data Lake](data-lake-store-security-overview.md). Para una información detallada acerca de cómo se implementan las ACL en Azure Data Lake Store, consulte [Información general de Access Control en Data Lake Store](data-lake-store-access-control.md).

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe tener el siguiente hello:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Una cuenta de Almacén de Azure Data Lake**. Para obtener instrucciones sobre cómo toocreate un, consulte [empezar a trabajar con el almacén de Azure Data Lake](data-lake-store-get-started-portal.md)

## <a name="create-security-groups-in-azure-active-directory"></a>Creación de grupos de seguridad en Azure Active Directory
Para obtener instrucciones acerca de cómo los grupos de seguridad AAD toocreate y cómo tooadd grupo de toohello de usuarios, consulte [administrar grupos de seguridad de Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).

> [!NOTE] 
> Puede agregar usuarios y otro grupo de tooa grupos de Azure AD utilizando Hola portal de Azure. Sin embargo, en orden tooadd un grupo de tooa principal de servicio, use [módulo de PowerShell de Azure AD](../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md).
> 
> ```powershell
> # Get hello desired group and service principal and identify hello correct object IDs
> Get-AzureADGroup -SearchString "<group name>"
> Get-AzureADServicePrincipal -SearchString "<SPI name>"
> 
> # Add hello service principal toohello group
> Add-AzureADGroupMember -ObjectId <Group object ID> -RefObjectId <SPI object ID>
> ```
 
## <a name="assign-users-or-security-groups-tooazure-data-lake-store-accounts"></a>Asignar usuarios o grupos de seguridad de las cuentas de almacén de Data Lake tooAzure
Cuando se asignan a los usuarios o grupos de seguridad de las cuentas de almacén de Data Lake tooAzure, puede controlar las operaciones de administración de acceso toohello en la cuenta de hello mediante Hola portal de Azure y las API del Administrador de recursos de Azure. 

1. Abra una cuenta de Almacén de Azure Data Lake. En el panel izquierdo de hello, haga clic en **examinar**, haga clic en **almacén de Data Lake**y, a continuación, desde la hoja de almacén de Data Lake hello, haga clic en toowhich de nombre de cuenta de hello desea tooassign un usuario o grupo de seguridad.

2. En la hoja de configuración de su cuenta de Data Lake Store, haga clic en **Control de acceso (IAM)**. hoja de Hello mediante listas de forma predeterminada **los administradores de suscripciones** grupo como propietario.
   
    ![Asignar la cuenta de almacén de Data Lake de tooAzure de grupo de seguridad](./media/data-lake-store-secure-data/adl.select.user.icon.png "asignar la cuenta de almacén de Data Lake de tooAzure de grupo de seguridad")

    Hay tooadd de dos maneras de un grupo y asignarles los roles correspondientes.
   
    * Agregar una cuenta de usuario o grupo toohello y, a continuación, asignar un rol, o
    * Agregar un rol y, a continuación, asignar usuarios o grupos toorole.
     
    En esta sección, veremos primer enfoque Hola y de agregar un grupo y, a continuación, asignar roles. Puede realizar similar pasos toofirst seleccione un rol y, a continuación, asigne el rol de toothat de grupos.
4. Hola **usuarios** hoja, haga clic en **agregar** tooopen hello **agregar acceso** hoja. Hola **agregar acceso** hoja, haga clic en **seleccione un rol**y, a continuación, seleccione un rol de usuario o grupo de Hola.
   
    ![Agregar un rol de usuario de hello](./media/data-lake-store-secure-data/adl.add.user.1.png "agregar un rol de usuario de Hola")
   
    Hola **propietario** y **colaborador** rol proporciona acceso tooa diversas funciones de administración en la cuenta de hello data lake. Para los usuarios que interactúan con datos en lake de hello datos, puede agregarlos toohello ** lector ** rol. ámbito de Hola de estas funciones es limitado toohello administración operaciones relacionadas toohello cuenta de almacén de Azure Data Lake.
   
    Para los datos permisos de sistema de archivos individuales de operaciones definen qué pueden hacer los usuarios de Hola. Por lo tanto, un usuario que tenga un rol de lector puede solo vista configuraciones administrativas asociadas con la cuenta de hello pero podría leer y escribir datos en función de los permisos del sistema de archivos asignados toothem. Permisos de sistema de archivos de almacén de Data Lake pueden consultarse en [asignar el grupo de seguridad como las ACL toohello sistema de archivos de almacén de Azure Data Lake](#filepermissions).
5. Hola **agregar acceso** hoja, haga clic en **agregar usuarios** tooopen hello **agregar usuarios** hoja. En esta hoja, busque el grupo de seguridad de Hola que creó anteriormente en Azure Active Directory. Si tiene muchos grupos toosearch desde, utilice el cuadro de texto de hello en hello toofilter superior en el nombre del grupo de Hola. Haga clic en **Seleccionar**.
   
    ![Agregar un grupo de seguridad](./media/data-lake-store-secure-data/adl.add.user.2.png "Agregar un grupo de seguridad")
   
    Si desea tooadd un grupo o usuario que no aparece, puede invitar a ellos mediante el uso de hello **invitar a** icono y especificar la dirección de correo electrónico Hola Hola/grupo de usuarios.
6. Haga clic en **Aceptar**. Debería ver el grupo de seguridad de hello agregar tal y como se muestra a continuación.
   
    ![Grupo de seguridad agregado](./media/data-lake-store-secure-data/adl.add.user.3.png "Grupo de seguridad agregado")

7. El grupo de seguridad del usuario tiene ahora la cuenta de acceso de almacén de Azure Data Lake toohello. Si desea que los usuarios de tooprovide access toospecific, puede agregarlos toohello grupo de seguridad. De forma similar, si desea acceso toorevoke para un usuario, puede quitarlos del grupo de seguridad de Hola. También puede asignar a varios grupos de seguridad tooan cuenta. 

## <a name="filepermissions"></a>Asignar usuarios o grupos de seguridad como las ACL toohello sistema de archivos de almacén de Azure Data Lake
Mediante la asignación de grupos de seguridad del usuario o sistema de archivos de Azure Data Lake toohello, establecer el control de acceso en los datos de hello almacenados en el almacén de Azure Data Lake.

1. En la hoja de su cuenta de Almacén de Data Lake, haga clic en **Explorador de datos**.
   
    ![Creación de directorios en una cuenta de Data Lake Store](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Creación de directorios en una cuenta de Data Lake Store")
2. Hola **Explorador de datos** hoja, haga clic en el archivo de Hola o una carpeta para el que desea tooconfigure Hola ACL y, a continuación, haga clic en **acceso**. archivo de tooa de tooassign ACL, debe hacer clic **acceso** de hello **vista previa del archivo** hoja.
   
    ![Configuración de ACL en el sistema de archivos de Data Lake](./media/data-lake-store-secure-data/adl.acl.1.png "Configuración de ACL en el sistema de archivos de Data Lake")
3. Hola **acceso** hoja enumera acceso estándar hello y acceso personalizado ya asignado toohello raíz. Haga clic en hello **agregar** icono tooadd personalizada basada en la ACL.
   
    ![Lista de accesos estándar y personalizados](./media/data-lake-store-secure-data/adl.acl.2.png "Lista de accesos estándar y personalizados")
   
   * **Acceso estándar** es hello estilo UNIX acceso, donde se especifican leer, escribir, ejecutar las clases de usuario distintas de toothree (rwx): propietario, grupo y otras personas.
   * **Acceso personalizado** corresponde toohello POSIX ACL que permite tooset permisos para usuarios con nombre específicos o grupos y no solo Hola propietario o grupo del archivo. 
     
     Para obtener más información, consulte la página sobre las [ACL de HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists). Para más información sobre cómo se implementan las ACL en Data Lake Store, consulte [Control de acceso en Data Lake Store](data-lake-store-access-control.md).
4. Haga clic en hello **agregar** Hola de icono tooopen **agregar acceso de personalizado** hoja. En esta hoja, haga clic en **Seleccionar usuario o grupo**y, a continuación, en **Seleccionar usuario o grupo** hoja, busque el grupo de seguridad de Hola que creó anteriormente en Azure Active Directory. Si tiene muchos grupos toosearch desde, utilice el cuadro de texto de hello en hello toofilter superior en el nombre del grupo de Hola. Haga clic en grupo de Hola que desee tooadd y, a continuación, haga clic en **seleccione**.
   
    ![Incorporación de un grupo](./media/data-lake-store-secure-data/adl.acl.3.png "Incorporación de un grupo")
5. Haga clic en **permisos Select**, seleccionar los permisos de Hola y si desea que los permisos de hello tooassign como una ACL predeterminada, tener acceso a ACL, o ambos. Haga clic en **Aceptar**.
   
    ![Asignar permisos toogroup](./media/data-lake-store-secure-data/adl.acl.4.png "asignar permisos toogroup")
   
    Para obtener más información sobre los permisos de Data Lake Store y ACL y las ACL predeterminadas y de acceso, consulte [Control de acceso en Data Lake Store](data-lake-store-access-control.md).
6. Hola **agregar acceso de personalizado** hoja, haga clic en **Aceptar**. Hola recién agregado grupo con permisos de hello asociado, ahora se mostrarán en hello **acceso** hoja.
   
    ![Asignar permisos toogroup](./media/data-lake-store-secure-data/adl.acl.5.png "asignar permisos toogroup")
   
   > [!IMPORTANT]
   > En la versión actual de hello, solo puede tener 9 entradas en **acceso personalizado**. Si desea tooadd más de 9 a los usuarios, debe crear grupos de seguridad, agregar grupos de usuarios toosecurity, agregue proporcionar acceso a los grupos de seguridad de toothose Hola cuenta de almacén de Data Lake.
   > 
   > 
7. Si es necesario, también puede modificar los permisos de acceso de hello después de haber agregado el grupo de Hola. Hola Active o desactive casilla de verificación para cada permiso de tipo (lectura, escritura y ejecución) en función de si desea que tooremove o asignar a dicho grupo de seguridad de toohello de permiso. Haga clic en **guardar** toosave cambios de hello, o **descartar** cambios de hello tooundo.

## <a name="set-ip-address-range-for-data-access"></a>Configuración del intervalo de direcciones IP para el acceso a los datos
Almacén de Data Lake de Azure le permite bloquear toofurther de almacén de datos de tooyour de acceso en el nivel de red. Puede habilitar el firewall, especificar una dirección IP o definir un intervalo de direcciones IP para los clientes de confianza. Una vez habilitada, solo los clientes que tengan direcciones IP de hello dentro del intervalo definido pueden conectarse toohello almacén.

![Configuración del firewall y acceso a IP](./media/data-lake-store-secure-data/firewall-ip-access.png "Configuración del firewall y dirección IP")

## <a name="remove-security-groups-for-an-azure-data-lake-store-account"></a>Quitar grupos de seguridad de una cuenta de Almacén de Azure Data Lake
Al quitar grupos de seguridad de las cuentas de almacén de Azure Data Lake, sólo estará cambiando las operaciones de administración de acceso toohello en la cuenta de hello mediante Hola Portal de Azure y las API del Administrador de recursos de Azure.

1. En la hoja de su cuenta de Data Lake Store, haga clic en **Configuración**. De hello **configuración** hoja, haga clic en **usuarios**.
   
    ![Asignar la cuenta de Data Lake de tooAzure de grupo de seguridad](./media/data-lake-store-secure-data/adl.select.user.icon.png "asignar la cuenta de Data Lake de tooAzure de grupo de seguridad")
2. Hola **usuarios** hoja, haga clic en grupo de seguridad de Hola que desee tooremove.
   
    ![Tooremove de grupo de seguridad](./media/data-lake-store-secure-data/adl.add.user.3.png "tooremove del grupo de seguridad")
3. En la hoja de hello para el grupo de seguridad de hello, haga clic en **quitar**.
   
    ![Grupo de seguridad quitado](./media/data-lake-store-secure-data/adl.remove.group.png "Grupo de seguridad quitado")

## <a name="remove-security-group-acls-from-azure-data-lake-store-file-system"></a>Quitar las ACL de grupo de seguridad del sistema de archivos del Almacén de Azure Data Lake
Al quitar grupos de seguridad de ACL del sistema de archivos de almacén de Azure Data Lake, cambiar toohello acceder a los datos en el almacén de Data Lake Hola.

1. En la hoja de su cuenta de Almacén de Data Lake, haga clic en **Explorador de datos**.
   
    ![Crear directorios en una cuenta de Data Lake](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Crear directorios en una cuenta de Data Lake")
2. Hola **Explorador de datos** hoja, haga clic en archivo de Hola o una carpeta que se desea tooremove Hola ACL y, a continuación, en la hoja de la cuenta, haga clic en hello **acceso** icono. tooremove ACL para un archivo, debe hacer clic **acceso** de hello **vista previa del archivo** hoja.
   
    ![Configuración de ACL en el sistema de archivos de Data Lake](./media/data-lake-store-secure-data/adl.acl.1.png "Configuración de ACL en el sistema de archivos de Data Lake")
3. Hola **acceso** hoja de hello **acceso personalizado** sección, haga clic en grupo de seguridad de Hola que desee tooremove. Hola **acceso personalizado** hoja, haga clic en **quitar** y, a continuación, haga clic en **Aceptar**.
   
    ![Asignar permisos toogroup](./media/data-lake-store-secure-data/adl.remove.acl.png "asignar permisos toogroup")

## <a name="see-also"></a>Otras referencias
* [Información general del Almacén de Azure Data Lake](data-lake-store-overview.md)
* [Copiar los datos de almacén de Blobs de Azure almacenamiento Lake tooData](data-lake-store-copy-data-azure-storage-blob.md)
* [Uso de Análisis de Azure Data Lake con el Almacén de Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Uso de HDInsight de Azure con el Almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Introducción al Almacén de Azure Data Lake mediante PowerShell](data-lake-store-get-started-powershell.md)
* [Introducción al Almacén de Azure Data Lake mediante .NET SDK](data-lake-store-get-started-net-sdk.md)
* [Acceso a los registros de diagnóstico de Azure Data Lake Store](data-lake-store-diagnostic-logs.md)

