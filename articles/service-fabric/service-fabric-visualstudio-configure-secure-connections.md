---
title: "aaaConfigure conexiones seguras de Azure Service Fabric clúster | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Visual Studio tooconfigure proteger las conexiones que son compatibles con clústeres de hello Azure Service Fabric."
services: service-fabric
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: tglee
ms.assetid: 80501867-dd7a-4648-8bd6-d4f26b68402d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/04/2017
ms.author: cawa
ms.openlocfilehash: ed3e5043264cf026f74e24ca09b40ccc70086cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-connections-tooa-service-fabric-cluster-from-visual-studio"></a>Configurar el clúster de Service Fabric tooa de conexiones seguras de Visual Studio
Obtenga información acerca de cómo toouse Visual Studio toosecurely tener acceso a un clúster de Azure Service Fabric con las directivas de control de acceso configuradas.

## <a name="cluster-connection-types"></a>Tipos de conexión del clúster
Se admiten dos tipos de conexiones por clúster de hello Azure Service Fabric: **no seguras** conexiones y **x509 basada en certificados** conexiones seguras. (En los clústeres de Service Fabric hospedados localmente también se admiten las autenticaciones de **Windows** y **dSTS**). Tener tipo de conexión de tooconfigure Hola clúster cuando se va a crear el clúster de Hola. Una vez creado, no se puede cambiar el tipo de conexión de Hola.

herramientas de Visual Studio Service Fabric Hola admiten todos los tipos de autenticación para conexión de tooa de clúster para la publicación. Vea [configuración de un clúster de Service Fabric de hello Azure portal](service-fabric-cluster-creation-via-portal.md) para obtener instrucciones sobre cómo tooset un clúster de Service Fabric segura.

## <a name="configure-cluster-connections-in-publish-profiles"></a>Configuración de las conexiones del clúster en perfiles de publicación
Si se publica un proyecto de Service Fabric desde Visual Studio, use hello **publicar aplicación de servicio de Fabric** toochoose del cuadro de diálogo un clúster de Azure Service Fabric. En **Punto de conexión**, seleccione un clúster actual en su suscripción.

![Hola ** el cuadro de diálogo Publicar servicio Fabric aplicación ** es tooconfigure usa una conexión de Service Fabric.][publishdialog]

Hola **publicar aplicación de servicio de Fabric** cuadro de diálogo valida automáticamente la conexión de clúster de Hola. Si se le solicita, inicie sesión en tooyour cuenta de Azure. Si la validación es correcta, significa que el sistema tiene Hola correcto certificados instalados tooconnect toohello clúster de forma segura o el clúster es no seguras. Errores de validación pueden deberse a problemas de red o no hacer que el clúster seguros de tooa de tooconnect sistema configurado correctamente.

![Hola ** publicar servicio Fabric aplicación ** cuadro de diálogo valida una existente, correctamente configurado conexión de clúster de Service Fabric.][selectsfcluster]

### <a name="tooconnect-tooa-secure-cluster"></a>clúster de tooconnect tooa segura
1. Asegúrese de que puede tener acceso a uno de los certificados de cliente de Hola que Hola confianzas de clúster de destino. certificado de Hola se comparte normalmente como un archivo de intercambio de información Personal (.pfx). Vea [configuración de un clúster de Service Fabric de hello portal de Azure](service-fabric-cluster-creation-via-portal.md) sobre cómo tooconfigure Hola server toogrant tener acceso a tooa cliente.
2. Instale el certificado de confianza de Hola. toodo, haga doble clic en el archivo .pfx de Hola o usar Hola PowerShell script Import-PfxCertificate tooimport Hola certificados. Instalar certificado de hello demasiado**Cert: \LocalMachine\My**. Es tooaccept Aceptar todos los valores predeterminados durante la importación de certificados de Hola.
3. Elija hello **publicar...**  comando menú contextual de Hola Hola de hello proyecto tooopen **publicar aplicación de Azure** cuadro de diálogo y el clúster de destino, a continuación, seleccione Hola. herramienta de Hello resuelve conexión hello y guarda la conexión segura Hola parámetros Hola publicación perfil automáticamente.
4. Opcional: Puede editar Hola publicar perfil toospecify una conexión de clúster segura.
   
   Puesto que puede editar manualmente la información del certificado Hola XML del perfil de publicación archivo toospecify Hola, estar seguro de nombre de almacén de certificados de hello toonote, almacenar la ubicación y la huella digital del certificado. Necesitará tooprovide estos valores para el almacén de certificados de hello nombre y ubicación del almacén. Vea [Cómo: recuperar Hola huella digital de un certificado](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) para obtener más información.
   
   Puede usar hello *ClusterConnectionParameters* parámetros toospecify Hola PowerShell parámetros toouse cuando se conecta el clúster de Service Fabric toohello. Los parámetros válidos son los que se aceptan mediante el cmdlet Connect-ServiceFabricCluster Hola. Consulte [Conexión de ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) para obtener una lista de parámetros disponibles.
   
   Si va a publicar tooa de clúster remoto, necesita parámetros adecuados de toospecify Hola para ese clúster concreto. Hola te mostramos un ejemplo de clúster no seguras de conexión tooa:
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   Este es un ejemplo de tooan x509 conexión basada en certificados clúster segura:
   
   ```xml
   <ClusterConnectionParameters
   ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000"
   X509Credential="true"
   ServerCertThumbprint="0123456789012345678901234567890123456789"
   FindType="FindByThumbprint"
   FindValue="9876543210987654321098765432109876543210"
   StoreLocation="CurrentUser"
   StoreName="My" />
   ```
5. Modificar otras configuraciones necesarias, como parámetros de actualización y la ubicación del archivo de parámetro de la aplicación y, a continuación, publicar la aplicación de hello **publicar aplicación de servicio de Fabric** cuadro de diálogo de Visual Studio.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre el acceso a los clústeres de Service Fabric, consulte [Visualización del clúster mediante el Explorador de Service Fabric](service-fabric-visualizing-your-cluster.md).

<!--Image references-->
[publishdialog]:./media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:./media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png
