---
title: "aplicaciones de aaaPublishing en redes independientes y las ubicaciones con grupos de conectores de Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "Cubre cómo toocreate y administrar grupos de conectores en el Proxy de aplicación de Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: 8c9a84b365eab28eaaeb343d4d1e2e6990537fec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>Publicación de aplicaciones en redes independientes y ubicaciones mediante grupos de conectores
> [!div class="op_single_selector"]
> * [Portal de Azure](active-directory-application-proxy-connectors-azure-portal.md)
> * [Portal de Azure clásico](active-directory-application-proxy-connectors.md)
>

Los clientes usan el proxy de aplicación de Azure AD en cada vez más escenarios y aplicaciones. Por este motivo, hemos habilitado más topologías para que sea más flexible. Puede crear grupos de conectores de Proxy de aplicación para que pueda asignar conectores específicos tooserve determinadas aplicaciones. Esta funcionalidad le ofrece más toooptimize de control y formas de la implementación de Proxy de aplicación. 

Cada conector del Proxy de aplicación se asigna el grupo de conectores de tooa. Todos los Hola conectores que pertenecen toohello al mismo grupo de conectores actúan como una unidad independiente para alta disponibilidad y equilibrio de carga. Todos los conectores pertenecen tooa grupo de conectores. Si no crea grupos, todos sus conectores estarán en un grupo predeterminado. El administrador puede crear nuevos grupos y asignar toothem conectores Hola portal de Azure. 

Todas las aplicaciones se asignan a tooa grupo de conectores. Si no se crean grupos, todas las aplicaciones se asignan a tooa grupo de manera predeterminada. Pero si organizar sus conectores en grupos, puede establecer cada toowork de aplicación con un grupo de conectores específico. En este caso, solo conectores de hello en ese grupo de dar servicio a aplicación Hola tras la solicitud. Esta característica es útil si las aplicaciones se hospedan en diferentes ubicaciones. Puede crear grupos de conectores en función de la ubicación, para que las aplicaciones son siempre atendidas por los conectores que están físicamente cerrar toothem.

>[!TIP] 
>Si tiene una implementación de Proxy de aplicación de gran tamaño, no asigne a ningún grupo de conectores de aplicaciones toohello de forma predeterminada. De este modo, nuevos conectores no reciben todo el tráfico en vivo hasta que los asigne a grupo del conector de active tooan. Esta configuración también le permite tooput conectores en modo inactivo moviéndolos toohello atrás el grupo predeterminado, por lo que puede realizar el mantenimiento sin afectar a los usuarios.

## <a name="prerequisites"></a>Requisitos previos
toogroup sus conectores, tendrá que toomake seguro de [varios conectores instalados](active-directory-application-proxy-enable.md). Cuando se instala un nuevo conector, se une automáticamente hello **predeterminado** grupo de conectores.

## <a name="create-connector-groups"></a>Creación de grupos de conectores
Use estos pasos toocreate tantos grupos de conectores como desee. 

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
1. Seleccione **Azure Active Directory** > **Aplicaciones empresariales** > **Proxy de aplicación**.
2. Seleccione **Nuevo grupo de conectores**. aparece la hoja de nuevo grupo de conectores de Hola.

   ![Seleccione Nuevo grupo de conectores](./media/active-directory-application-proxy-connectors-azure-portal/new-group.png)

3. Asigne un nombre a su nuevo grupo de conectores, utilice tooselect de menú desplegable de Hola que conectores pertenecen a este grupo.
4. Seleccione **Guardar**.

## <a name="assign-applications-tooyour-connector-groups"></a>Asignar a grupos de conectores de tooyour de aplicaciones
Siga estos pasos para cada una de las aplicaciones que haya publicado con el proxy de aplicación. Puede asignar a un grupo de conectores de aplicaciones tooa al publicarlo primero, o puede utilizar la asignación de Hola de toochange para estos pasos siempre que lo desee.   

1. En el panel de administración de hello para el directorio, seleccione **aplicaciones empresariales** > **todas las aplicaciones** > Hola aplicación desea que el grupo de conectores de tooassign tooa >  **Proxy de aplicación**.
2. Hola de uso **grupo de conectores** grupo de hello desplegable menú tooselect desea Hola toouse de aplicación.
3. Seleccione **guardar** cambio de hello tooapply.

## <a name="use-cases-for-connector-groups"></a>Casos de uso de grupos de conectores 

Los grupos de conectores son útiles para diversos escenarios, por ejemplo:

### <a name="sites-with-multiple-interconnected-datacenters"></a>Sitios con varios centros de datos interconectados.

Muchas organizaciones tienen muchos centros de datos interconectados. En este caso, desea tookeep como cantidad de tráfico en el centro de datos de hello como sea posible porque los vínculos entre centros de datos son costosos y lentos. Puede implementar los conectores en cada centro de datos tooserve solo hello las aplicaciones que residen en el centro de datos de Hola. Este enfoque minimiza los vínculos entre centros de datos y proporciona una experiencia totalmente transparente tooyour a los usuarios.

### <a name="applications-installed-on-isolated-networks"></a>Aplicaciones instaladas en redes aisladas

Las aplicaciones se pueden hospedar en redes que no forman parte de la red corporativa principal de Hola. Puede utilizar conectores de tooinstall dedicado de grupos de conector de red de toohello de redes aisladas tooalso aislar las aplicaciones. Esto suele suceder cuando un proveedor de terceros mantiene una aplicación concreta para su organización. 

Grupos de conectores permiten tooinstall dedicado conectores para las redes a las que publican determinadas aplicaciones, lo que facilita y más seguro a la administración de aplicaciones toooutsource toothird fabricantes.

### <a name="applications-installed-on-iaas"></a>Aplicaciones instaladas en IaaS 

Para las aplicaciones instaladas en IaaS para el acceso a la nube, los grupos de conectores proporcionan una comunes del servicio toosecure Hola acceso tooall Hola de aplicaciones. Grupos de conectores no crear dependencia adicional en la red corporativa o fragmentar la experiencia de aplicación Hola. Los conectores se pueden instalar en todos los centros de datos en la nube y servir solo a las aplicaciones que residen en esa red. Puede instalar varios disponibilidad alta tooachieve de conectores.

Tomemos como ejemplo una organización que tiene varias máquinas virtuales conectadas tootheir propia red virtual IaaS hospedados. tooallow empleados toouse estas aplicaciones, estas redes privadas son toohello conectado red corporativa mediante VPN de sitio a sitio. De este modo, los empleados que trabajan en un entorno local podrán usarlas sin ningún problema. Pero no es ideal para los empleados remotos, ya que requiere acceso de tooroute de infraestructura locales adicionales, como puede ver en diagrama de hello siguiente:

![Red Iaas de Azure AD](./media/application-proxy-publish-apps-separate-networks/application-proxy-iaas-network.png)
  
Con grupos de conectores de Proxy de aplicación de Azure AD, puede habilitar un tooall aplicaciones comunes de servicio toosecure Hola acceso sin crear dependencia adicional en la red corporativa:

![Varios proveedores de nube (IaaS de Azure AD)](./media/application-proxy-publish-apps-separate-networks/application-proxy-multiple-cloud-vendors.png)

### <a name="multi-forest--different-connector-groups-for-each-forest"></a>Varios bosques: grupos de conectores diferentes para cada bosque

La mayoría de los clientes que han implementado el proxy de aplicación usan sus funcionalidades de inicio de sesión único (SSO) mediante la delegación restringida de kerberos (KCD). tooachieve esto, máquinas necesidad toobe tooa Unidos a un dominio del conector de hello que puede delegar a los usuarios de hello hacia la aplicación hello. KCD es compatible con las funcionalidades de varios bosques. No obstante, en el caso de las empresas que tienen distintos entornos de varios bosques sin ninguna relación de confianza entre ellos, no se puede usar un solo conector para todos los bosques. 

En este caso, conectores específicos se pueden implementar por bosque y conjunto tooserve aplicaciones que fueron publicado tooserve Hola solo los usuarios de ese bosque específico. Cada grupo de conectores representa un bosque diferente. Mientras el inquilino de Hola y la mayoría de experiencia de hello unificada para todos los bosques, los usuarios pueden asignar aplicaciones de bosque tootheir con grupos de Azure AD.
 
### <a name="disaster-recovery-sites"></a>Sitios de recuperación ante desastres

Hay dos enfoques diferentes que puede adoptar con un sitio de recuperación ante desastres, dependiendo de cómo estén implementados sus sitios:

* Si el sitio de recuperación ante desastres se compila en el modo activo / activo que es exactamente igual que el sitio principal de Hola y tiene Hola mismo las redes y la configuración de AD, puede crear conectores de hello en el sitio de recuperación ante desastres de Hola Hola mismo grupo de conectores como sitio principal de Hola. Así, las conmutaciones por error de Azure AD toodetect para usted.
* Si el sitio de recuperación ante desastres es independiente del sitio principal de hello, puede crear un grupo de otro conector en el sitio de recuperación ante desastres de Hola y 1) tiene las aplicaciones de copia de seguridad ni desviar 2) manualmente el grupo de conectores de aplicaciones existentes de hello toohello DR según sea necesario.
 
### <a name="serve-multiple-companies-from-a-single-tenant"></a>Servicio a varias empresas desde un solo inquilino

Hay muchas maneras diferentes tooimplement un modelo en el que implementa un proveedor de servicio único y mantiene Azure AD relacionadas con servicios de varias compañías. Grupos de conectores ayudan Hola, administrador separar los conectores de Hola y aplicaciones en grupos distintos. Un método, que es adecuado para las pequeñas empresas, es toohave un único inquilino de Azure AD mientras compañías diferentes de hello tienen su propio nombre de dominio y redes. También es válido para los escenarios de fusión y adquisición, donde una sola división de TI presta servicios a varias empresas por motivos normativos o empresariales. 

## <a name="sample-configurations"></a>Configuraciones de ejemplo

Algunos ejemplos que se pueden implementar, incluyen hello siguientes grupos de conectores.
 
### <a name="default-configuration--no-use-for-connector-groups"></a>Configuración predeterminada: ningún uso para los grupos de conectores

Si no usa grupos de conectores, la configuración tendría un aspecto similar al siguiente:

![Sin grupos de conectores de Azure AD](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-1.png)
 
Esta configuración es suficiente para pruebas e implementaciones de menor envergadura. También funcionará bien si su organización tiene una topología de red plana.
 
### <a name="default-configuration-and-an-isolated-network"></a>Configuración predeterminada y red aislada

Esta configuración es una evolución de hello predeterminado, en el que hay una aplicación específica que se ejecuta en una red aislada, como la red virtual de IaaS: 

![Sin grupos de conectores de Azure AD](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-2.png)
 
### <a name="recommended-configuration--several-specific-groups-and-a-default-group-for-idle"></a>Configuración recomendada: varios grupos específicos y un grupo predeterminado para conectores inactivos

configuración recomendada para organizaciones grandes y complejas de Hello es grupo de conectores de toohave Hola predeterminado como un grupo que no sirva a cualquier aplicación y se utiliza para los conectores de inactividad o recién instalados. Las aplicaciones se atienden con grupos de conectores personalizados. Esto permite que toda la complejidad de Hola de escenarios de Hola que se ha descrito anteriormente.

En el siguiente ejemplo de Hola, empresa hello tiene dos centros de datos, A y B, con dos conectores que sirven de cada sitio. Cada uno de los sitios tienen distintas aplicaciones que se ejecutan en él. 

![Sin grupos de conectores de Azure AD](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-3.png)
 
## <a name="next-steps"></a>Pasos siguientes

* [Descripción de los conectores del Proxy de aplicación de Azure AD](application-proxy-understand-connectors.md)
* [Habilitar el inicio de sesión único](application-proxy-sso-overview.md)


