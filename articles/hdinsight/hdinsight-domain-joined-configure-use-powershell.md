---
title: "aaaConfigure clústeres de HDInsight Unidos a un dominio con PowerShell - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset una copia de seguridad y configurar clústeres de HDInsight Unidos a un dominio con Azure PowerShell"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a13b2f7a-612d-4800-bc92-7fc0524f3e89
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 49da3439513d1e51171f0f7f7f9c3d967d55cb7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview-using-azure-powershell"></a>Configuración de clústeres de HDInsight unidos a un dominio (versión preliminar) con Azure PowerShell
Obtenga información acerca de cómo agrupar tooset seguridad un HDInsight de Azure con Azure Active Directory (Azure AD) y [Apache Cazador](http://hortonworks.com/apache/ranger/) con Azure PowerShell. Configuración de hello toomake más rápido y menos propenso a errores, se proporciona un script de PowerShell de Azure. HDInsight unido a un dominio solo se puede configurar en clústeres basados en Linux. Para más información, consulte [Introduce Domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md) (Introducción a los clústeres de HDInsight unidos a dominio (versión preliminar))

> [!IMPORTANT]
> Oozie no está habilitado en HDInsight unido a un dominio.

Una configuración típica de clúster de HDInsight Unidos a un dominio implica Hola pasos:

1. Cree una red virtual clásica de Azure para su Azure AD.  
2. Cree y configure Azure AD y Azure AD DS.
3. Agregar una máquina virtual toohello clásico red virtual para crear la unidad organizativa. 
4. Cree una unidad organizativa para Azure AD DS.
5. Crear una HDInsight VNet en modo de administración de recursos de Azure Hola.
6. Configurar zonas de DNS inverso para hello Azure AD DS.
7. Elemento del mismo nivel Hola dos redes virtuales.
8. Cree un clúster de HDInsight.

Hello secuencia de comandos de PowerShell proporcionada realiza los pasos del 3 al 7. Debe seguir los pasos 1 y 2 manualmente.  Si prefiere no toouse PowerShell de Azure, consulte [clústeres de HDInsight Unidos al dominio configurar](hdinsight-domain-joined-configure.md). 

Un ejemplo de topología final de hello tiene el siguiente aspecto:

![Topología de HDInsight unido a un dominio](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

Dado que Azure AD actualmente solo admite redes virtuales clásicas (VNet) y los clústeres de HDInsight basados en Linux solo admiten Azure Resource Manager basado en redes virtuales, la integración de Azure AD de HDInsight requiere dos redes virtuales y un emparejamiento entre ellas. Para obtener información de comparación Hola entre modelos de implementación de hello dos, consulte [Azure Resource Manager frente a la implementación clásica: comprender los modelos de implementación y Hola estado de los recursos](../azure-resource-manager/resource-manager-deployment-model.md). Hola dos redes virtuales deben estar en hello misma región que hello Azure AD DS.

> [!NOTE]
> En este tutorial se supone que no tiene una cuenta de Azure AD. Si tiene uno, puede omitir la parte de hello en el paso 2.
> 
> 

## <a name="prerequisites"></a>Requisitos previos
Debe tener Hola después toogo elementos a través de este tutorial:

* Familiarícese con [Servicios de dominio de Azure AD](https://azure.microsoft.com/services/active-directory-ds/) y su estructura de [precios](https://azure.microsoft.com/pricing/details/active-directory-ds/).
* Asegúrese de que la suscripción está en la lista blanca para esta versión preliminar pública. Puede hacerlo mediante el envío de un correo electrónico toohdipreview@microsoft.com con su identificador de suscripción.
* Un certificado SSL firmado por una autoridad de firma para el dominio. se requiere el certificado de Hello mediante la configuración de LDAP seguro. Los certificados autofirmados no se pueden usar.
* Azure PowerShell.  Consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).

## <a name="create-an-azure-classic-vnet-for-your-azure-ad"></a>Cree una red virtual clásica de Azure para su Azure AD.
Para obtener instrucciones de hello, consulte [aquí](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic).

## <a name="create-and-configure-azure-ad-and-azure-ad-ds"></a>Cree y configure Azure AD y Azure AD DS.
Para obtener instrucciones de hello, consulte [aquí](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).

## <a name="run-hello-powershell-script"></a>Ejecutar script de PowerShell de Hola
Hola script de PowerShell se puede descargar desde [GitHub](https://github.com/hdinsight/DomainJoinedHDInsight). Extraer el archivo zip de Hola y guardar archivos de hello localmente.

**Hola tooedit script de PowerShell**

1. Abra run.ps1 mediante Windows PowerShell ISE o cualquier editor de texto.
2. Rellenar los valores de hello para hello siguientes variables:
   
   * **$SubscriptionName** : hello nombre de hello suscripción de Azure donde desee toocreate su clúster de HDInsight. Ya se ha creado una red virtual clásica en esta suscripción y va a crear una red virtual de Azure Resource Manager para el clúster de HDInsight de hello en la suscripción.
   * **$ClassicVNetName** -red virtual clásica Hola que contiene hello Azure AD DS. Esta red virtual debe estar en hello misma suscripción que se proporciona anteriormente. Esta red virtual debe crearse utilizando Hola portal de Azure y no portal clásico. Si sigue las instrucciones de hello en [clústeres de HDInsight configurar-Unidos a un dominio (versión preliminar)](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic), Hola predeterminado se denomina contosoaadvnet.
   * **$ClassicResourceGroupName** : nombre del grupo de administrador de recursos de hello para la red virtual clásica Hola que esté mencionada anteriormente. Por ejemplo, contosoaadrg. 
   * **$ArmResourceGroupName** : nombre de grupo de recursos de hello dentro del cual, desea que el clúster de HDInsight de toocreate Hola. Puede usar hello mismo grupo de recursos como $ArmResourceGroupName.  Si no existe el grupo de recursos de hello, script de Hola crea el grupo de recursos de Hola.
   * **$ArmVNetName** -nombre de red virtual del Administrador de recursos Hola dentro del cual desea clúster de HDInsight de toocreate Hola. Esta red virtual se colocará en $ArmResourceGroupName.  Si Hola red virtual no existe, lo creará Hola script de PowerShell. Si existe, debe formar parte del grupo de recursos de Hola que proporcionan por encima.
   * **$AddressVnetAddressSpace** : hello espacio de direcciones de red virtual de hello Administrador de recursos de red. Asegúrese de que este espacio de direcciones está disponible. Este espacio de direcciones no puede superponer Hola clásico del espacio de direcciones. Por ejemplo, “10.1.0.0/16”
   * **$ArmVnetSubnetName** -nombre de subred de red virtual Hola Administrador de recursos dentro del cual desea que el clúster de HDInsight tooplace hello las máquinas virtuales. Si no existe la subred hello, Hola script de PowerShell lo creará. Si existe, debe formar parte de la red virtual de hello proporcionado anteriormente.
   * **$AddressSubnetAddressSpace** : hello intervalo de direcciones de subred de red virtual de hello Administrador de recursos de red. clúster de HDInsight de Hello que las direcciones IP de VM será desde este intervalo de direcciones de subred. Por ejemplo, “10.1.0.0/24”.
   * **$ActiveDirectoryDomainName** – a las VM de clúster de nombre de dominio de hello Azure AD que deseas hello toojoin HDInsight. Por ejemplo, “contoso.onmicrosoft.com”.
   * **$ClusterUsersGroups** – nombre común de Hola Hola de grupos de seguridad de AD que desea que el clúster de HDInsight de toosync toohello. usuarios Hola dentro de este grupo de seguridad será capaz de toolog en panel de clúster toohello con sus credenciales de dominio de active directory. Estos grupos de seguridad deben existir en active directory de Hola. Por ejemplo, "hiveusers" o "clusteroperatorusers".
   * **$OrganizationalUnitName** -unidad organizativa Hola Hola dominio, dentro del cual desea clúster de HDInsight tooplace hello las máquinas virtuales y Hola entidades de servicio utilizadas por el clúster de Hola. Hola script de PowerShell creará esta OU si no existe. Por ejemplo, "HDInsightOU".
3. Guarde los cambios de Hola.

**script de Hola toorun**

1. Ejecute **Windows PowerShell** como administrador.
2. Busque la carpeta toohello de run.ps1. 
3. Ejecutar script de Hola escribiendo el nombre de archivo de Hola y pulse **ENTRAR**.  Se muestran tres cuadros de diálogo de inicio de sesión:
   
   1. **Inicie sesión en el portal clásico de tooAzure** : escriba las credenciales que usa toosign en portal clásico de tooAzure. Debe haber creado Hola AD de Azure y Azure AD DS con estas credenciales.
   2. **Inicie sesión en el portal de administrador de recursos de tooAzure** : escriba las credenciales que usa toosign en tooAzure portal de administrador de recursos.
   3. **Nombre de usuario de dominio** : escriba las credenciales de Hola Hola dominio del nombre de usuario que desea que un administrador de clúster de HDInsight de hello toobe. Si creó una instancia de Azure AD de cero, debe haber creado este usuario usando esta documentación. 
      
      > [!IMPORTANT]
      > Escriba el nombre de usuario de hello en este formato: 
      > 
      > NombreDominio\nombreUsuario (por ejemplo, contoso.onmicrosoft.com\clusteradmin)
      > 
      > 
      
      Este usuario debe tener privilegios de 3: toojoin máquinas toohello proporciona el dominio de Active Directory; entidades de servicio toocreate y los objetos de equipo dentro de hello proporcionan a unidad organizativa; y reglas de proxy DNS inversas tooadd.

Al crear las zonas DNS inversas, script de Hola le solicitará que del Id. de una red de tooenter Este identificador de red debe ser el prefijo de dirección de la red virtual de hello Administrador de recursos. Por ejemplo, si el espacio de direcciones de subred de red virtual de administrador de recursos es 10.2.0.0/24, escriba 10.2.0.0/24 cuando herramienta Hola le pide Hola Id. de red. 

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
     * **Versión**: Hadoop 2.7.3 (HDI 3.5). HDInsight unido a un dominio solo se admite en clústeres de HDInsight versión 3.5.
     * **Tipo de clúster**: PREMIUM
       
       Haga clic en **seleccione** cambios de hello toosave.
   * **Credenciales**: configurar las credenciales de hello para el usuario del clúster de Hola y usuario SSH Hola.
   * **Origen de datos**: crear una nueva cuenta de almacenamiento o usar una cuenta de almacenamiento existente como Hola cuenta de almacenamiento predeterminada para el clúster de HDInsight Hola. ubicación de Hello debe ser Hola igual que Hola dos redes virtuales.  Hola ubicación es también Hola Hola del clúster de HDInsight.
   * **Precios**: seleccione Hola número de nodos de trabajador del clúster.
   * **Configuraciones avanzadas**: 
     
     * **Unión a un dominio y red virtual o subred**: 
       
       * **Configuración de dominio**: 
         
         * **Nombre de dominio**: contoso.onmicrosoft.com
         * **Nombre de usuario de dominio**: Escriba un nombre de usuario de dominio. Este dominio debe tener Hola siguientes privilegios: unirse a dominio de toohello máquinas y colocarlos en la unidad organizativa de Hola que configuró anteriormente; Crear a entidades de servicio dentro de la unidad organizativa de Hola que configuró anteriormente; Crear entradas DNS inversas. Este usuario de dominio se convertirá en Administrador de Hola de este clúster de HDInsight Unidos a un dominio.
         * **Contraseña de dominio**: escriba la contraseña de usuario de dominio de Hola.
         * **La unidad organizativa**: escriba Hola nombre distintivo de hello unidad organizativa que configuró anteriormente. Por ejemplo: OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com
         * **Dirección URL de LDAPS**: ldaps://contoso.onmicrosoft.com:636
         * **Grupo de usuarios de acceso**: Especificar grupo de seguridad de hello cuyos usuarios wan toosync toohello clúster. Por ejemplo, HiveUsers.
           
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
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure-use-powershell/deploy-to-azure.png" alt="Deploy tooAzure"></a>
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
   * **DN de grupo de usuarios de clúster**: "\"CN=HiveUsers,OU=AADDC Users,DC=<DomainName>,DC=onmicrosoft,DC=com\""
   * **LDAPUrls**: ["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: (nombre de usuario de administrador de entrar Hola dominio)
   * **DomainAdminPassword**: (escriba la contraseña de usuario de administrador de dominio de hello)
   * **Muestro mi conformidad toohello términos y condiciones indicadas anteriormente**: (comprobar)
   * **PIN toodashboard**: (comprobar)
3. Haga clic en **Comprar**. Verá un icono nuevo llamado **Implementación para la implementación de plantilla**. Se tarda aproximadamente toocreate de aproximadamente 20 minutos de un clúster. Una vez creado el clúster de hello, haga clic en hoja de clúster de hello en tooopen portal Hola se.

Después de completar el tutorial de hello, conviene clúster de hello toodelete. Con HDInsight, los datos se almacenan en Almacenamiento de Azure, por lo que puede eliminar un clúster de forma segura cuando no está en uso. También se le cargará por un clúster de HDInsight aunque no esté en uso. Puesto que los cargos de Hola de clúster de hello son muchas veces más que los cargos de hello para el almacenamiento, conviene económico toodelete clústeres cuando no están en uso. Para obtener instrucciones de hello de la eliminación de un clúster, consulte [Hadoop administrar clústeres de HDInsight mediante el uso de Hola portal de Azure](hdinsight-administer-use-management-portal.md#delete-clusters).

## <a name="next-steps"></a>Pasos siguientes

* Para configurar directivas de Hive y ejecución de consultas de Hive, consulte [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Configuración de directivas de los clústeres de HDInsight unidos a dominio).
* Para usar clústeres de HDInsight unido tooDomain SSH tooconnect, consulte [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).

