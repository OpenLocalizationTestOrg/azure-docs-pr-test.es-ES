---
title: "clústeres de HDInsight Unidos a un dominio de aaaConfigure - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset una copia de seguridad y configurar clústeres de HDInsight Unidos a un dominio"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 0cbb49cc-0de1-4a1a-b658-99897caf827c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 8c4b3d269a7662d27a49b839e5cd05a3e24f7023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview"></a>Configuración de clústeres de HDInsight unidos a un dominio (versión preliminar)

Obtenga información acerca de cómo agrupar tooset seguridad un HDInsight de Azure con Azure Active Directory (Azure AD) y [Apache Cazador](http://hortonworks.com/apache/ranger/) tootake aprovechar una autenticación firme y las directivas de acceso enriquecido basado en roles (RBAC) del control.  HDInsight unido a un dominio solo se puede configurar en clústeres basados en Linux. Para más información, consulte [Introduce Domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md) (Introducción a los clústeres de HDInsight unidos a dominio (versión preliminar))

> [!IMPORTANT]
> Oozie no está habilitado en HDInsight unido a un dominio.

Este artículo es el primer tutorial de una serie de hello:

* Crear un clúster conectado HDInsight, tooAzure AD (a través de la capacidad de servicios de dominio de Azure Directory hello) con Cazador Apache habilitado.
* Crear y aplicar directivas de Hive a través de Apache Cazador y permitir a los usuarios (por ejemplo, los científicos de datos) tooHive tooconnect con herramientas basadas en ODBC, por ejemplo, Excel, Tableau etcetera. Microsoft está trabajando en agregar otras cargas de trabajo, como HBase, Spark y Storm, HDInsight unido tooDomain pronto.

Un ejemplo de topología final de hello tiene el siguiente aspecto:

![Topología de HDInsight unido a un dominio](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

Dado que Azure AD actualmente solo admite redes virtuales clásicas (VNet) y los clústeres de HDInsight basados en Linux solo admiten Azure Resource Manager basado en redes virtuales, la integración de Azure AD de HDInsight requiere dos redes virtuales y un emparejamiento entre ellas. Para obtener información de comparación Hola entre modelos de implementación de hello dos, consulte [Azure Resource Manager frente a la implementación clásica: comprender los modelos de implementación y Hola estado de los recursos](../azure-resource-manager/resource-manager-deployment-model.md). Hola dos redes virtuales deben estar en hello misma región que hello Azure AD DS.

Los nombres de servicio de Azure deben ser únicos globalmente. Hola después de nombres se utiliza en este tutorial. Contoso es un nombre ficticio. Debe reemplazar *contoso* con un nombre diferente al seguir el tutorial de Hola. 

**Nombres:**

| Propiedad | Valor |
| --- | --- |
| Red virtual de Azure AD |contosoaadvnet |
| Grupo de recursos de red virtual de Azure AD |contosoaadrg |
| Directorio de Azure AD |contosoaaddirectory |
| Nombre de dominio de Azure AD |contoso (contoso.onmicrosoft.com) |
| Red virtual de HDInsight |contosohdivnet |
| Grupo de recursos de red virtual de HDInsight |contosohdirg |
| Clúster de HDInsight |contosohdicluster |

Este tutorial ofrece pasos de Hola para configurar un clúster de HDInsight Unidos a un dominio. Cada sección contiene artículos de tooother de vínculos con más información.

## <a name="prerequisite"></a>Requisito previo:
* Familiarícese con [Servicios de dominio de Azure AD](https://azure.microsoft.com/services/active-directory-ds/) y su estructura de [precios](https://azure.microsoft.com/pricing/details/active-directory-ds/).
* Asegúrese de que la suscripción está en la lista blanca para esta versión preliminar pública. Puede hacerlo mediante el envío de un correo electrónico toohdipreview@microsoft.com con su identificador de suscripción.
* Un certificado SSL firmado por una autoridad de firma para el dominio. se requiere el certificado de Hello mediante la configuración de LDAP seguro. Los certificados autofirmados no se pueden usar.

## <a name="procedures"></a>Procedimientos
1. Cree una red virtual clásica de Azure para su Azure AD.  
2. Cree y configure Azure AD y Azure AD DS.
3. Crear una HDInsight VNet en modo de administración de recursos de Azure Hola.
4. Elemento del mismo nivel Hola dos redes virtuales.
5. Cree un clúster de HDInsight.

> [!NOTE]
> En este tutorial se supone que no tiene una cuenta de Azure AD. Si tiene uno, puede omitir la parte de hello en el paso 2.
> 
> 

Hay un script de PowerShell que automatiza los pasos 3 al 7.  Para más información, consulte [Configuración de clústeres de HDInsight unidos a un dominio con Azure PowerShell](hdinsight-domain-joined-configure-use-powershell.md).

## <a name="create-an-azure-virtual-network-classic"></a>Creación de una instancia de Azure Virtual Network (clásico)
En esta sección, creará una red virtual (clásica) mediante Hola portal de Azure. En la siguiente sección hello, habilita hello Azure AD DS para Azure AD, en la red virtual de Hola. Para obtener más información acerca de hello siguiendo el procedimiento y mediante otros métodos de creación de la red virtual, vea [crear una red virtual (clásica) mediante el uso de hello portal de Azure](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).

**toocreate una red virtual clásica**

1. Inicio de sesión toohello [portal de Azure](https://portal.azure.com). 
2. Haga clic en **Nuevo** > **Redes** > **Red virtual**.
3. En **Seleccionar un modelo de implementación**, seleccione **Clásico** y luego haga clic en **Crear**.
4. Escriba o seleccione Hola siguientes valores:
   
   * **Nombre**: contosoaadvnet
   * **Espacio de direcciones**: 10.1.0.0/16
   * **Nombre de subred**: Subnet1
   * **Intervalo de direcciones de subred**: 10.1.0.0/24
   * **Suscripción**: (Seleccione una suscripción usada para crear esta red virtual.)
   * **ResourceGroup**: contosoaadrg
   * **Ubicación**: (Seleccione una región para el clúster de HDInsight.)
     
     > [!IMPORTANT]
     > Debe elegir una ubicación compatible con Azure AD DS. Para más información, consulte [Productos disponibles por región](https://azure.microsoft.com/en-us/regions/services/). 
     > 
     > Ambos Hola clásico red virtual y hello red virtual del grupo de recursos debe tener Hola misma región que hello Azure AD DS.
     > 
     > 
5. Haga clic en **crear** toocreate Hola red virtual.

## <a name="create-and-configure-azure-ad-ds-for-your-azure-ad"></a>Creación y configuración de Azure AD DS para Azure AD
En esta sección:

1. Creará Azure AD.
2. Creará usuarios de Azure AD. Estos usuarios son usuarios de dominio. Utilice el primer usuario de Hola para configurar el clúster de HDInsight de hello con hello Azure AD.  Hello otros dos usuarios son opcionales para este tutorial. Se usarán en [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Configuración de directivas de Hive para clústeres de HDInsight unidos a un dominio) al configurar las directivas de Apache Ranger.
3. Crear grupo de administradores de controlador de dominio de AAD de Hola y agregar grupo de toohello de usuarios de Azure AD Hola. Utilice esta unidad organizativa de usuario toocreate Hola.
4. Habilitar los servicios de dominio de Active Directory de Azure (Azure AD DS) para hello Azure AD.
5. Configurar LDAPS para hello Azure AD. Hola Lightweight Directory Access Protocol (LDAP) es usado tooread de y escribir tooAzure AD.

Si lo prefiere toouse un anuncio de Azure existente, puede omitir los pasos 1 y 2.

**toocreate un Azure AD**

1. De hello [portal de Azure clásico](https://manage.windowsazure.com), haga clic en **New** > **servicios de aplicaciones** > **Active Directory**  >  **Directorio** > **creación personalizada**. 
2. Escriba o seleccione Hola siguientes valores:
   
   * **Nombre**: contosoaaddirectory
   * **Nombre de dominio**: contoso.  Este nombre debe ser único globalmente.
   * **País o región**: Seleccione el país o región.
3. Haga clic en **Completo**.

**Para crear un usuario de Azure AD**

1. De hello [portal de Azure clásico](https://manage.windowsazure.com), haga clic en **Active Directory** -> **contosoaaddirectory**. 
2. Haga clic en **usuarios** de menú superior Hola.
3. Haga clic en **Agregar usuario**.
4. Escriba un nombre en **Nombre de usuario** y haga clic en **Siguiente**. 
5. Configure el perfil de usuario; en **Rol**, seleccione **Administrador global** y haga clic en **Siguiente**.  rol de administrador Global de Hello es necesario toocreate las unidades organizativas.
6. Haga clic en **crear** tooget una contraseña temporal.
7. Realizar una copia de la contraseña de hello y, a continuación, haga clic en **completar**. Más adelante en este tutorial, usará este clúster de HDInsight de administrador global usuario toocreate Hola.

Seguimiento Hola mismo toocreate procedimiento más dos usuarios con hello **usuario** rol, hiveuser1 y hiveuser2. Hello usuarios siguientes se utilizarán en [Hive configurar directivas para clústeres de HDInsight Unidos al dominio](hdinsight-domain-joined-run-hive.md).

**toocreate Hola grupo Administradores del controlador de dominio de AAD y agregar un usuario de Azure AD**

1. De hello [portal de Azure clásico](https://manage.windowsazure.com), haga clic en **Active Directory** > **contosoaaddirectory**. 
2. Haga clic en **grupos** de menú superior Hola.
3. Haga clic en **Agregar un grupo** o **Agregar grupo**.
4. Escriba o seleccione Hola siguientes valores:
   
   * **Nombre**: Administradores de controlador de dominio de AAD.  No cambie el nombre del grupo de Hola.
   * **Tipo de grupo**: Seguridad.
5. Haga clic en **Completo**.
6. Haga clic en **administradores de controlador de dominio de AAD** grupo de hello tooopen.
7. Haga clic en **Agregar miembros**.
8. Seleccione usuario primera Hola creado en el paso anterior de hello y, a continuación, haga clic en **completar**.
9. Hola repetición llama a otro grupo mismo toocreate pasos **HiveUsers**, y agregue Hola dos Hive usuarios toohello grupo.

Para obtener más información, consulte [servicios de dominio de AD de Azure (vista previa): crear hello 'Administradores de controlador de dominio de AAD' grupo](../active-directory-domain-services/active-directory-ds-getting-started.md).

**tooenable Azure AD DS para Azure AD**

1. De hello [portal de Azure clásico](https://manage.windowsazure.com), haga clic en **Active Directory** > **contosoaaddirectory**. 
2. Haga clic en **configurar** de menú superior Hola.
3. Desplácese hacia abajo demasiado**los servicios de dominio**, y después de hello de conjunto de valores:
   
   * **Habilitar Servicios de dominio para este directorio**: Sí.
   * **Nombre de dominio DNS de servicios de dominio**: muestra nombre DNS predeterminado de Hola de hello directorio de Azure. Por ejemplo, contoso.onmicrosoft.com.
   * **Conectar la red virtual de toothis de servicios de dominio**: seleccione Hola clásico red virtual que creó anteriormente, es decir, **contosoaadvnet**.
4. Haga clic en **guardar** desde el final Hola Hola. Verá **pendientes...**  siguiente demasiado**habilitar los servicios de dominio para este directorio**.  
5. Espere hasta que **Pendiente...** desaparezca y **Dirección IP** se rellene. Se rellenarán dos direcciones IP. Se trata de direcciones IP de Hola Hola de controladores de dominio aprovisionados por servicios de dominio. Cada dirección IP será visible cuando el controlador de dominio correspondiente de Hola se ha aprovisionado y listo. Escriba las direcciones IP de hello dos. Las necesitará más adelante.

Para más información, consulte [Servicios de dominio de Azure AD (versión preliminar) - Habilitación de Servicios de dominio de Azure AD](../active-directory-domain-services/active-directory-ds-getting-started-enableaadds.md).

**contraseña de toosynchronize**

Si usa su propio dominio, necesita toosynchronize Hola contraseña. Vea [habilite servicios de dominio de tooAzure AD de sincronización de contraseña de un solo en la nube Azure directorio AD](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md).

**tooconfigure LDAPS para hello Azure AD**

1. Obtenga un certificado SSL firmado por una autoridad de firma para el dominio. Si desea toouse un certificado autofirmado, póngase en contacto toohdipreview@microsoft.com para una excepción.
2. De hello [portal de Azure clásico](https://manage.windowsazure.com), haga clic en **Active Directory** > **contosoaaddirectory**. 
3. Haga clic en **configurar** de menú superior Hola.
4. Desplácese demasiado**servicios de dominio de**.
5. Haga clic en **Configurar certificado**.
6. Siga el archivo de certificado de hello instrucciones toospecify hello y la contraseña de Hola. Verá **pendientes...**  siguiente demasiado**habilitar los servicios de dominio para este directorio**.  
7. Espere hasta que **Pendiente...** desaparezca y **Certificado LDAP seguro** se rellene.  Esto puede tardar hasta 10 minutos o más.

> [!NOTE]
> Si algunas tareas en segundo plano se está ejecutando en hello Azure AD DS, puede ver un error al cargar certificado - <i>hay una operación que se realiza para este inquilino. Inténtelo de nuevo más tarde</i>.  En caso de que se produzca este error, inténtelo de nuevo más tarde. Hola que segundo IP del controlador de dominio puede tardar hasta too3 horas toobe aprovisionado.
> 
> 

Para más información, consulte [Configuración de LDAP seguro (LDAPS) para un dominio administrado con Servicios de dominio de Azure AD](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md).

## <a name="create-a-resource-manager-vnet-for-hdinsight-cluster"></a>Creación de una red virtual de Resource Manager para un clúster de HDInsight
En esta sección, creará un administrador de recursos de Azure VNet que se usará para el clúster de HDInsight Hola. Para más información sobre la creación de una red virtual de Azure utilizando otros métodos, consulte [Creación de una red virtual](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

Después de crear la red virtual de hello, configurará Hola, Administrador de recursos VNet toouse Hola mismos servidores DNS que para hello red virtual de Azure AD. Si ha seguido los pasos de hello en este tutorial toocreate Hola clásico hello Azure AD y red virtual de servidores DNS de hello son 10.1.0.4 y 10.1.0.5.

**toocreate una VNet el Administrador de recursos**

1. Inicio de sesión toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **Nuevo**, **Redes** y, a continuación, en **Red virtual**. 
3. En **Seleccionar un modelo de implementación**, seleccione **Resource Manager** y haga clic en **Crear**.
4. Escriba o seleccione Hola siguientes valores:
   
   * **Nombre**: contosohdivnet
   * **Espacio de direcciones**: 10.2.0.0/16. Asegúrese de que el intervalo de direcciones de hello no puede solaparse con el intervalo de direcciones IP de Hola de hello clásico red virtual.
   * **Nombre de subred**: Subnet1
   * **Intervalo de direcciones de subred**: 10.2.0.0/24
   * **Suscripción**: (Seleccione su suscripción de Azure.)
   * **Grupo de recursos**: contosohdirg
   * **Ubicación**: (seleccione Hola misma ubicación como Hola red virtual de AD de Azure, es decir, contosoaadvnet).
5. Haga clic en **Crear**.

**tooconfigure DNS para hello VNet el Administrador de recursos**

1. De hello [portal de Azure](https://portal.azure.com), haga clic en **más servicios** -> **redes virtuales**. Asegúrese de no tooclick **redes virtuales (clásicas)**.
2. Haga clic en **contosohdivnet**.
3. Haga clic en **servidores DNS** de hello parte izquierda de la nueva hoja de Hola.
4. Haga clic en **personalizada**y, a continuación, escriba Hola siguientes valores:
   
   * 10.1.0.4
   * 10.1.0.5
     
     Estas direcciones IP del servidor DNS deben coincidir con los servidores DNS toohello Hola red virtual de Azure AD (clásico red virtual).
5. Haga clic en **Guardar**.

## <a name="peer-hello-azure-ad-vnet-and-hello-hdinsight-vnet"></a>Del mismo nivel Hola red virtual de Azure AD y Hola HDInsight VNet
**toopeer Hola dos red virtual**

1. Inicio de sesión toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **más servicios** desde el menú de la izquierda Hola.
3. Haga clic en **Redes virtuales**. No haga clic en **Redes virtuales (clásico)**.
4. Haga clic en **contosohdivnet**.  Se trata de hello HDInsight VNet.
5. Haga clic en **emparejamientos** en el menú de la izquierda Hola de hoja de Hola.
6. Haga clic en **agregar** desde el menú superior Hola. Se abre hello **agregar emparejamiento** hoja.
7. En hello **agregar emparejamiento** hoja, establecido o seleccione Hola siguientes valores:
   
   * **Nombre**: ContosoAADHDIVNetPeering
   * **Modelo de implementación de red virtual**: Clásico
   * **Suscripción**: seleccione el nombre de suscripción que utiliza para la red virtual de hello clásico (Azure AD).
   * **Red virtual**: contosoaadvnet.
   * **Permitir acceso a red virtual**: (Comprobar)
   * **Permitir tráfico reenviado**: (Comprobar). Deje Hola otras dos casillas de verificación no está activada.
8. Haga clic en **Aceptar**.

## <a name="create-hdinsight-cluster"></a>Creación de un clúster de HDInsight
En esta sección, creará un clúster basado en Linux, Hadoop en HDInsight con cualquier portal de Azure de Hola o [plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Para otros métodos de creación de clúster y descripción de la configuración de hello, consulte [HDInsight crear clústeres](hdinsight-hadoop-provision-linux-clusters.md). Para obtener más información acerca de cómo utilizar el Administrador de recursos plantilla toocreate Hadoop los clústeres de HDInsight, vea [Hadoop crear clústeres de HDInsight con plantillas de administrador de recursos](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

**toocreate un clúster de HDInsight Unidos a un dominio con Hola portal de Azure**

1. Inicio de sesión toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **Nuevo**, **Inteligencia y análisis** y luego en **HDInsight**.
3. De hello **HDInsight nuevo clúster** hoja, escriba o seleccione Hola siguientes valores:
   
   * **Nombre del clúster**: escriba un nuevo nombre de clúster para el clúster de HDInsight Unidos a un dominio de Hola.
   * **Suscripción**: Seleccione una suscripción de Azure usada para crear este clúster.
   * **Configuración de clúster**:
     
     * **Tipo de clúster**: Hadoop. HDInsight unido a un dominio actualmente solo es compatible con clústeres de Hadoop.
     * **Sistema operativo**: Linux.  HDInsight unido a un dominio solo se admite en clústeres de HDInsight basado en Linux.
     * **Versión**: HDI 3.6. HDInsight unido a un dominio solo se admite en clústeres de HDInsight versión 3.6.
     * **Tipo de clúster**: PREMIUM
       
       Haga clic en **seleccione** cambios de hello toosave.
   * **Credenciales**: configurar las credenciales de hello para el usuario del clúster de Hola y usuario SSH Hola.
   * **Origen de datos**: crear una nueva cuenta de almacenamiento o usar una cuenta de almacenamiento existente como Hola cuenta de almacenamiento predeterminada para el clúster de HDInsight Hola. ubicación de Hello debe ser Hola igual que Hola dos redes virtuales.  Hola ubicación es también Hola Hola del clúster de HDInsight.
   * **Precios**: seleccione Hola número de nodos de trabajador del clúster.
   * **Configuraciones avanzadas**: 
     
     * **Unión a un dominio y red virtual o subred**: 
       
       * **Configuración de dominio**: 
         
         * **Nombre de dominio**: contoso.onmicrosoft.com
         * **Nombre de usuario de dominio**: Escriba un nombre de usuario de dominio. Este dominio debe tener Hola siguientes privilegios: unirse a dominio de toohello máquinas y colocarlos en la unidad de organización de Hola que especifique durante la creación del clúster; Crear a entidades de servicio dentro de la unidad de organización de Hola que especifique durante la creación del clúster; Crear entradas DNS inversas. Este usuario de dominio se convertirá en Administrador de Hola de este clúster de HDInsight Unidos a un dominio.
         * **Contraseña de dominio**: escriba la contraseña de usuario de dominio de Hola.
         * **La unidad organizativa**: escriba Hola nombre distintivo de hello unidad organizativa que desea toouse con clúster de HDInsight. Por ejemplo: OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com. Si no existe esta OU, clúster de HDInsight intentará toocreate esta OU. Asegúrese de que Hola OU ya está presente o cuenta de dominio de hello tiene permisos toocreate uno nuevo. Si utiliza la cuenta de dominio de Hola que forma parte de los administradores de AADDC, tendrá permisos necesarios toocreate Hola OU.
         * **Dirección URL de LDAPS**: ldaps://contoso.onmicrosoft.com:636
         * **Grupo de usuarios de acceso**: especifique el grupo de seguridad de hello cuyos usuarios desea toosync toohello clúster. Por ejemplo, HiveUsers.
           
           Haga clic en **seleccione** cambios de hello toosave.
           
           ![Configuración del dominio del portal de HDInsight unido a un dominio](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-portal-domain-setting.png)
       * **Red virtual**: contosohdivnet
       * **Subred**: Subnet1
         
         Haga clic en **seleccione** cambios de hello toosave.        
         Haga clic en **seleccione** cambios de hello toosave.
   * **Grupo de recursos**: grupo de recursos de hello seleccione destinada hello HDInsight VNet (contosohdirg).
4. Haga clic en **Crear**.  

Otra opción para crear el clúster de HDInsight Unidos a un dominio es toouse plantilla de administración de recursos de Azure. Hola procedimiento muestra lo siguiente:

**toocreate un clúster de HDInsight Unidos a un dominio mediante una plantilla de administración de recursos**

1. Haga clic en hello después imagen tooopen una plantilla de administrador de recursos en hello portal de Azure. plantilla de administrador de recursos de Hola se encuentra en un contenedor de blobs públicos. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. De hello **parámetros** hoja, escriba Hola siguientes valores:
   
   * **Suscripción**: (Seleccione su suscripción de Azure).
   * **Grupo de recursos**: haga clic en **utilizar existente**y especifique Hola mismo grupo de recursos que se ha utilizado.  Por ejemplo, contosohdirg. 
   * **Ubicación**: Especifique una ubicación del grupo de recursos.
   * **Nombre del clúster**: escriba un nombre para el clúster de Hadoop de Hola que va a crear. Por ejemplo, contosohdicluster.
   * **Tipo de clúster**: seleccione un tipo de clúster.  es el valor predeterminado de Hello **hadoop**.
   * **Ubicación**: seleccione una ubicación para el clúster de Hola.  cuenta de almacenamiento de Hello predeterminada utiliza Hola la misma ubicación.
   * **El número de nodos de trabajador del clúster**: seleccione Hola número de nodos de trabajador.
   * **Nombre de inicio de sesión y la contraseña del clúster**: nombre de inicio de sesión predeterminado de hello es **administración**.
   * **SSH username y password**: nombre de usuario de hello predeterminada es **sshuser**.  Puede cambiarlo. 
   * **Id. de red virtual**: /subscriptions/&lt;Id.Suscripción&gt;/resourceGroups/&lt;NombreGrupoRecursos&gt;/providers/Microsoft.Network/virtualNetworks/&lt;NombreRedVirtual&gt;
   * **Subred de la red virtual**: /subscriptions/&lt;Id.Suscripción&gt;/resourceGroups/&lt;NombreGrupoRecursos&gt;/providers/Microsoft.Network/virtualNetworks/&lt;NombreRedVirtual&gt;/subnets/Subnet1
   * **Nombre de dominio**: contoso.onmicrosoft.com
   * **DN de unidad organizativa**: OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com
   * **Nombres de dominio del grupo de usuarios del clúster**: [\"HiveUsers\"]
   * **LDAPUrls**: ["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: (nombre de usuario de administrador de entrar Hola dominio)
   * **DomainAdminPassword**: (escriba la contraseña de usuario de administrador de dominio de hello)
   * **Muestro mi conformidad toohello términos y condiciones indicadas anteriormente**: (comprobar)
   * **PIN toodashboard**: (comprobar)
3. Haga clic en **Comprar**. Verá un icono nuevo llamado **Implementación para la implementación de plantilla**. Se tarda aproximadamente toocreate de aproximadamente 20 minutos de un clúster. Una vez creado el clúster de hello, haga clic en hoja de clúster de hello en tooopen portal Hola se.

Después de completar el tutorial de hello, conviene clúster de hello toodelete. Con HDInsight, los datos se almacenan en Almacenamiento de Azure, por lo que puede eliminar un clúster de forma segura cuando no está en uso. También se le cargará por un clúster de HDInsight aunque no esté en uso. Puesto que los cargos de Hola de clúster de hello son muchas veces más que los cargos de hello para el almacenamiento, conviene económico toodelete clústeres cuando no están en uso. Para obtener instrucciones de hello de la eliminación de un clúster, consulte [Hadoop administrar clústeres de HDInsight mediante el uso de Hola portal de Azure](hdinsight-administer-use-management-portal.md#delete-clusters).

## <a name="next-steps"></a>Pasos siguientes
* Para configurar directivas de Hive y ejecución de consultas de Hive, consulte [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Configuración de directivas de los clústeres de HDInsight unidos a dominio).
* Para usar clústeres de HDInsight unido tooDomain SSH tooconnect, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Linux, Unix y OS X](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).

