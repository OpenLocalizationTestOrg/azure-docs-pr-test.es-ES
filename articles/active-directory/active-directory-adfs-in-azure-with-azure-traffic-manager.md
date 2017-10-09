---
title: "implementación de aaaHigh disponibilidad geográfica de entre AD FS en Azure con Azure Traffic Manager | Documentos de Microsoft"
description: "En este documento, aprenderá cómo toodeploy AD FS en Azure para alta disponibilidad."
keywords: "AD fs con el Administrador de tráfico de Azure, adfs con Azure Traffic Manager, geográficos, centro de datos de múltiples, centros de datos geográficos, varios centros de datos geográficos, implementación AD FS en azure, implementación azure adfs, adfs de azure, azure ad fs, implementación AD FS, implementación ad fs, AD FS en azure, implementar AD FS en azure, implementar AD FS en azure, azure AD FS, introducción tooAD FS, Azure, AD FS en Azure, iaas, AD FS, mover tooazure de adfs"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: c5838d749cdc5c8aabbe62b255d568525da747ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>Implementación entre regiones geográficas de AD FS de alta disponibilidad en Azure con Azure Traffic Manager
[Implementación de AD FS en Azure](active-directory-aadconnect-azure-adfs.md) proporciona instrucciones paso a paso como toohow puede implementar una infraestructura de AD FS simple para su organización en Azure. Este artículo proporciona pasos de hello toocreate un entre geográfica de implementación de AD FS en Azure mediante [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md). Traffic Manager de Azure le ayuda a crear una infraestructura de AD FS de alto rendimiento para su organización y geográficamente spread alta disponibilidad mediante la realización de uso de intervalo de métodos de enrutamiento toosuit disponible diferentes necesidades de infraestructura de Hola.

Una infraestructura entre regiones geográficas de AD FS de alta disponibilidad permite:

* **Eliminación de un punto único de error:** con capacidades de conmutación por error de Azure Traffic Manager, puede lograr una alta disponibilidad infraestructura de AD FS incluso cuando uno de los centros de datos de hello en una parte del mundo Hola deja de funcionar
* **Rendimiento mejorado:** puede usar Hola sugiere implementación en este artículo tooprovide una infraestructura de AD FS de alto rendimiento que puede ayudar a los usuarios a autenticarse con mayor rapidez. 

## <a name="design-principles"></a>Principios de diseño
![Diseño general](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

principios de diseño básico de Hello será mismos como se muestra en los principios de diseño en el artículo de hello implementación de AD FS en Azure. diagrama de Hello anterior muestra una extensión simple de la región geográfica de tooanother de implementación básica de Hola. A continuación se muestran algunos puntos tooconsider al extender la región geográfica de toonew de implementación

* **Red virtual:** debe crear una nueva red virtual en la región geográfica de hello desea infraestructura de toodeploy adicional AD FS. En el diagrama de hello anterior verá Geo1 virtuales y red virtual Geo2 como Hola dos redes virtuales en cada región geográfica.
* **Controladores de dominio y servidores de AD FS en la nueva red virtual geográfica:** se recomienda toodeploy controladores de dominio en la nueva región geográfica de Hola para que AD FS Hola servidores en la nueva región de hello no tengan toocontact un controlador de dominio en otro momento toocomplete una autenticación de ubicación de red y, por tanto, mejorar rendimiento de Hola.
* **Cuentas de almacenamiento:** las cuentas de almacenamiento están asociadas a una región. Puesto que va a implementar las máquinas en una nueva región geográfica, tendrá nuevas cuentas de almacenamiento toocreate toobe utilizada en la región de Hola.  
* **Grupos de seguridad de red:** al igual que las cuentas de almacenamiento, los grupos de seguridad de red creados en una región no se pueden usar en otra región geográfica. Por lo tanto, necesitará toocreate nueva red seguridad grupos similares toothose pertenecen a la primera región geográfica de Hola para INT y DMZ subred en la nueva región geográfica de Hola.
* **Las etiquetas de DNS para las direcciones IP públicas:** Azure Traffic Manager puede hacer referencia a tooendpoints sólo a través de las etiquetas DNS. Por lo tanto, son necesarios toocreate DNS etiquetas para las direcciones IP públicas de Hola externo equilibradores de carga.
* **Azure Traffic Manager:** Microsoft Azure Traffic Manager le permite la distribución de hello toocontrol de extremos de servicio como usuario tráfico tooyour que se ejecutan en distintos centros de datos alrededor de Hola a todos. Azure Traffic Manager funciona en hello nivel de DNS. Usa DNS respuestas toodirect por el usuario final tráfico distribuidas tooglobally puntos de conexión. Los clientes, a continuación, conectarse directamente toothose extremos. Con diferentes opciones de enrutamientos de prioridad, Weighted y rendimiento, puede elegir fácilmente opción de enrutamiento de hello es adecuada para las necesidades de su organización. 
* **Conectividad de red tooV de V-net entre dos regiones:** no es necesario toohave conectividad entre redes virtuales de hello en la propia. Puesto que cada red virtual tiene acceso toodomain controladores y servidor de AD FS y WAP en sí mismo, puede trabajar sin cualquier tipo de conectividad entre redes virtuales de hello en regiones diferentes. 

## <a name="steps-toointegrate-azure-traffic-manager"></a>Pasos toointegrate Azure Traffic Manager
### <a name="deploy-ad-fs-in-hello-new-geographical-region"></a>Implementar AD FS en la nueva región geográfica de Hola
Siga los pasos de Hola y directrices en [implementación de AD FS en Azure](active-directory-aadconnect-azure-adfs.md) toodeploy Hola misma topología en la nueva región geográfica de Hola.

### <a name="dns-labels-for-public-ip-addresses-of-hello-internet-facing-public-load-balancers"></a>Etiquetas DNS para las direcciones IP públicas de hello con conexión a Internet (pública) equilibradores de carga
Tal y como se mencionó anteriormente, hello Azure Traffic Manager solo puede hacer referencia a las etiquetas de tooDNS los puntos de conexión y, por tanto, es importante toocreate etiquetas DNS para las direcciones IP públicas de Hola externo equilibradores de carga. Siguiente captura de pantalla muestra cómo puede configurar la etiqueta DNS para la dirección IP pública Hola. 

![Etiqueta DNS](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Implementación de Azure Traffic Manager
Siga estos pasos hello toocreate un perfil de administrador de tráfico. Para obtener más información, también puede hacer referencia demasiado[administrar un perfil de Traffic Manager de Azure](../traffic-manager/traffic-manager-manage-profiles.md).

1. **Creación de un perfil de Traffic Manager:** asigne un nombre único a su perfil del administrador de tráfico. Este nombre de perfil de hello forma parte del nombre DNS de Hola y actúa como un prefijo de etiqueta de nombre de dominio de Traffic Manager de Hola. nombre de Hola / too.trafficmanager.net toocreate una etiqueta DNS se añade el prefijo para el Administrador de tráfico. Hola de captura de pantalla siguiente muestra al administrador de tráfico Hola prefijo DNS que se va a establecer como mysts y etiqueta DNS resultante será mysts.trafficmanager.net. 
   
    ![Creación del perfil de Traffic Manager](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **Método de enrutamiento de tráfico:** existen tres opciones de enrutamiento disponibles en el administrador de tráfico:
   
   * Prioridad 
   * Rendimiento
   * Ponderado
     
     **Rendimiento** recomienda Hola infraestructura de opción tooachieve alta capacidad de respuesta AD FS. Sin embargo, puede elegir el método de enrutamiento que mejor se adapte a sus necesidades de implementación. funcionalidad de Hello AD FS no se ve afectada por la opción de enrutamiento de hello seleccionada. Consulte [Métodos de enrutamiento de tráfico de Traffic Manager](../traffic-manager/traffic-manager-routing-methods.md) para más información. Hola captura de pantalla de ejemplo anterior puede ver hello **rendimiento** método seleccionado.
3. **Configurar los puntos de conexión:** en la página del Administrador de tráfico de hello, haga clic en los puntos de conexión y seleccione Agregar. Se abrirá un Agregar extremo página similar toohello siguiente captura de pantalla
   
   ![Configuración de extremos](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   Para las entradas diferentes hello, sigue la norma de Hola a continuación:
   
   **Tipo:** seleccione extremo de Azure, tal y como se apuntar tooan Azure dirección IP pública.
   
   **Nombre:** crear un nombre que desee tooassociate con el punto de conexión de Hola. Esto no es el nombre DNS de hello y no repercute sobre los registros DNS.
   
   **Tipo de recurso de destino:** seleccionar pública dirección IP como propiedad de hello value toothis. 
   
   **Recurso de destino:** Esto le proporcionará una opción toochoose de etiquetas DNS diferentes de Hola que tiene disponible en su suscripción. Elija Hola que DNS etiqueta de punto de conexión toohello correspondiente que se va a configurar.
   
   Agregar punto de conexión para cada región geográfica que desee hello Azure Traffic Manager tooroute tráfico.
   Para obtener más información y pasos detallados sobre cómo tooadd / configurar puntos de conexión en el Administrador de tráfico, consulte demasiado[agregar, deshabilitar, habilitar o eliminar puntos de conexión](../traffic-manager/traffic-manager-endpoints.md)
4. **Configurar el sondeo:** en la página del Administrador de tráfico de hello, haga clic en configuración. En la página de configuración de hello, necesita tooprobe de configuración de monitor toochange hello en el puerto HTTP 80 y /adfs/probe de ruta de acceso relativa
   
    ![Configuración del sondeo](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **Asegúrese de que el estado de Hola de extremos de Hola es en línea una vez completada la configuración de Hola**. Si todos los extremos están en estado 'Degradado', Azure Traffic Manager hará un mejor intento tooroute Hola el tráfico suponiendo que diagnósticos de hello es correcta y que todos los extremos son accesibles.
   > 
   > 
5. **Modificar los registros DNS para el Administrador de tráfico de Azure:** el servicio de federación debe ser un nombre de DNS de Traffic Manager de Azure CNAME toohello. Crear un CNAME en hello registros DNS públicos para que la persona que está tratando de servicio de federación de hello tooreach no llegue al hello Azure Traffic Manager.
   
    Por ejemplo, toohello de fs.fabidentity.com Traffic Manager, para el servicio de federación de hello toopoint necesitaría tooupdate su Hola de toobe registros de recursos DNS siguientes:
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-hello-routing-and-ad-fs-sign-in"></a>Probar el enrutamiento de Hola y en el inicio de sesión de AD FS
### <a name="routing-test"></a>Prueba de enrutamiento
Una prueba muy básica para el enrutamiento de hello sería tootry ping Hola federación nombre DNS del servicio desde un equipo en cada región geográfica. Función elegido el método de enrutamiento de Hola, endpoint Hola que hace ping en realidad se verán reflejado en pantalla de ping de Hola. Por ejemplo, si ha seleccionado el rendimiento de hello enrutamiento, a continuación, extremo de hello más próximo toohello región del cliente de Hola se alcanzará. A continuación se muestra instantánea Hola de dos pings desde dos máquinas de cliente de región diferentes, uno en la región de Asia oriental y otro zona horaria del Pacífico occidental. 

![Prueba de enrutamiento](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>Prueba de inicio de sesión de AD FS
tootest de manera más fácil de Hello AD FS es mediante hello IdpInitiatedSignon.aspx página. En orden toobe capaz de toodo, que es necesario tooenable Hola IdpInitiatedSignOn en las propiedades de hello AD FS. Siga estos pasos hello tooverify el programa de instalación de AD FS

1. Ejecución Hola por debajo de cmdlet en el servidor de hello AD FS, con PowerShell, tooset, tooenabled. 
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
2. Desde cualquier acceso de equipo externo https://<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx
3. Debería ver la página de hello AD FS como las siguientes:
   
    ![Prueba de ADFS - desafío de autenticación](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    y cuando se inicia sesión correctamente, aparecerá un mensaje de confirmación similar al siguiente:
   
    ![Prueba de ADFS - autenticación correcta](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>Vínculos relacionados
* [Implementación básica de AD FS en Azure](active-directory-aadconnect-azure-adfs.md)
* [Microsoft Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md)
* [Métodos de enrutamiento del tráfico del Administrador de tráfico](../traffic-manager/traffic-manager-routing-methods.md)

## <a name="next-steps"></a>Pasos siguientes
* [Administrar un perfil del Administrador de tráfico de Azure](../traffic-manager/traffic-manager-manage-profiles.md)
* [Adición, deshabilitación, habilitación o eliminación de extremos](../traffic-manager/traffic-manager-endpoints.md) 

