---
title: aaaActive Directory Federation Services en Azure | Documentos de Microsoft
description: "En este documento, aprenderá cómo toodeploy AD FS en Azure para alta disponibilidad."
keywords: "implementar AD FS en azure, implementar azure adfs, adfs de azure, azure ad fs, implementar AD FS, implementar ad fs, AD FS en azure, implementar AD FS en azure, implementar AD FS en azure, azure AD FS, introducción tooAD FS, Azure, AD FS en Azure, iaas, AD FS, mover tooazure de adfs"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 692a188c-badc-44aa-ba86-71c0e8074510
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2c39271f7569b9ce395dce2f53f5ba5a4897b132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>Implementación de Active Directory Federation Services en Azure
AD FS proporciona funcionalidades de una federación de identidades simplificada y protegida, así como de inicio de sesión único (SSO) web. Federación con Azure AD u Office 365 permite a los usuarios tooauthenticate con localmente las credenciales y tener acceso a todos los recursos de nube. Como resultado, resulta importante toohave una alta disponibilidad ADFS infraestructura tooensure el acceso tooresources tanto de forma local y en la nube de Hola. Implementación de AD FS en Azure puede ayudar a lograr una alta disponibilidad de hello necesario con esfuerzos mínima.
La implementación de AD FS en Azure tiene varias ventajas; a continuación se enumeran algunas:

* **Alta disponibilidad** -la potencia de Hola de conjuntos de disponibilidad de Azure, asegúrese de una infraestructura de alta disponibilidad.
* **¿TooScale fácil** – necesitan un rendimiento más? Migrar fácilmente máquinas eficaz toomore por unos pocos clics en Azure
* **Redundancia geográfica entre** – con Azure Georredundancia puede estar seguro de que la infraestructura está altamente disponible en todo el mundo de Hola
* **TooManage fácil** – con opciones de administración muy simplificado en el portal de Azure, administrar su infraestructura es muy sencilla y sin complicaciones 

## <a name="design-principles"></a>Principios de diseño
![Diseño de la implementación](./media/active-directory-aadconnect-azure-adfs/deployment.png)

diagrama de Hello anterior muestra hello recomienda toostart topología básica implementar la infraestructura de AD FS en Azure. principios Hola Hola diversos componentes de la topología de Hola se enumeran a continuación:

* **Servidores de ADFS/controlador de dominio**: si tiene menos de 1000 usuarios, simplemente puede instalar el rol de AD FS en los controladores de dominio. Si no desea ningún impacto en el rendimiento en los controladores de dominio de Hola o si tiene más de 1.000 usuarios, a continuación, implementar AD FS en servidores independientes.
* **Servidor WAP** : es necesario toodeploy servidores de Proxy de aplicación Web, para que los usuarios pueden alcanzar Hola AD FS cuando no se encuentran en la red de empresa de hello también.
* **Red Perimetral**: servidores de Proxy de aplicación Web de Hola se colocarán en hello red Perimetral y se permite el acceso de solo TCP/443 entre Hola DMZ y subred interna Hola.
* **Equilibradores de carga**: tooensure alta disponibilidad de servidores de AD FS y Proxy de aplicación Web, se recomienda usar un equilibrador de carga interno para servidores de AD FS y el equilibrador de carga de Azure para los servidores Proxy de aplicación Web.
* **Conjuntos de disponibilidad**: implementación de tooprovide redundancia tooyour AD FS, se recomienda agrupar dos o más máquinas virtuales en un conjunto de disponibilidad para cargas de trabajo similares. Esta configuración garantiza que durante un evento de mantenimiento planeado o no planeado, al menos una máquina virtual estará disponible.
* **Las cuentas de almacenamiento**: se recomienda toohave dos cuentas de almacenamiento. Tener una única cuenta de almacenamiento puede provocar toocreation de un único punto de error y puede provocar Hola implementación toobecome no está disponible en un escenario poco probable que la cuenta de almacenamiento de hello deja de funcionar. Dos cuentas de almacenamiento ayudarán a asociar una cuenta de almacenamiento para cada línea con errores.
* **Segregación de la red**: los servidores proxy de aplicación web se deben implementar en una red perimetral independiente. Puede dividir una red virtual en dos subredes y, a continuación, implementar servidores de Proxy de aplicación Web de hello en una subred aislada. Simplemente puede configurar hello las opciones del grupo de seguridad de red para cada subred y permitir que solo requiere comunicación entre dos subredes de Hola. A continuación se proporcionan más detalles para cada escenario de implementación

## <a name="steps-toodeploy-ad-fs-in-azure"></a>Pasos toodeploy AD FS en Azure
pasos de Hello mencionados en esta sección esquema Hola guía toodeploy Hola siguiente muestran la infraestructura de AD FS en Azure.

### <a name="1-deploying-hello-network"></a>1. La implementación de red de Hola
Como se describió anteriormente, puede crear dos subredes en una única red virtual, o bien crear dos redes virtuales completamente diferentes. Este artículo se centrará en la implementación de una única red virtual y la dividirá en dos subredes. Actualmente, esta es un enfoque más sencillo como dos redes virtuales independientes podría necesitar una puerta de enlace de red virtual tooVNet para las comunicaciones.

**1.1 Creación de una red virtual**

![Creación de una red virtual](./media/active-directory-aadconnect-azure-adfs/deploynetwork1.png)

Hola portal de Azure, seleccione red virtual e implementar la red virtual de hello y una subred inmediatamente con un solo clic. Subred INT también se define y está ahora listo para toobe de las máquinas virtuales que se agrega.
paso siguiente Hello es tooadd otra red de toohello de subred, es decir, la subred de hello red Perimetral. toocreate Hola subred de red Perimetral, simplemente

* Seleccione la red Hola recién creado
* En Propiedades de hello seleccione subred
* Haga clic en el panel de una subred hello en hello Agregar botón
* Proporcione Hola subred nombre y la dirección espacio información toocreate Hola subred

![Subred](./media/active-directory-aadconnect-azure-adfs/deploynetwork2.png)

![Subred DMZ](./media/active-directory-aadconnect-azure-adfs/deploynetwork3.png)

**1.2. Crear grupos de seguridad de red de Hola**

Un grupo de seguridad de red (NSG) contiene una lista de reglas de lista de Control de acceso (ACL) que permiten o deniegan el tráfico de red tooyour instancias de máquina virtual en una red Virtual. Los NSG se pueden asociar con las subredes o las instancias individuales de máquina virtual dentro de esa subred. Cuando un NSG está asociado a una subred, las reglas de ACL de hello aplican tooall instancias de máquina virtual de hello en esa subred.
A fin de Hola de esta guía, crearemos dos NSG: uno para una red interna y una red Perimetral. Se denominarán NSG_INT y NSG_DMZ respectivamente.

![Creación de NSG](./media/active-directory-aadconnect-azure-adfs/creatensg1.png)

Después de hello que NSG se crea, habrá 0 reglas de entrada y 0 de salida. Una vez instalado y funciona roles hello en los servidores respectivos hello, a continuación, hello reglas entrantes y salientes pueden realizarse correspondiente de toohello deseado de nivel de seguridad.

![Inicialización de Git](./media/active-directory-aadconnect-azure-adfs/nsgint1.png)

Una vez creados los NSG Hola, asociar NSG_INT subred INT y NSG_DMZ con la subred de red Perimetral. A continuación se proporciona una captura de pantalla de ejemplo:

![Configuración de NSG](./media/active-directory-aadconnect-azure-adfs/nsgconfigure1.png)

* Haga clic en panel de subredes tooopen Hola para subredes
* Seleccione hello tooassociate de subred con hello NSG 

Después de la configuración, el panel de Hola para subredes debería ser similar a continuación:

![Subredes después GSN](./media/active-directory-aadconnect-azure-adfs/nsgconfigure2.png)

**1.3. Crear conexión tooon local**

Necesitamos una conexión tooon de manera local en orden toodeploy Hola controlador de dominio (DC) en azure. Azure ofrece diversas tooconnect de opciones de conectividad su tooyour de infraestructura local infraestructura de Azure.

* De punto a sitio
* De sitio a sitio de red virtual
* ExpressRoute

Se recomienda toouse ExpressRoute. ExpressRoute permite crear conexiones privadas entre los centros de datos de Azure y la infraestructura que está en su entorno local o en un entorno de colocalización. Las conexiones ExpressRoute no pasan por hello Internet pública. Ofrecen más confiabilidad, velocidades más rápidas, latencias más bajas y mayor seguridad que las típicas conexiones a través de Internet de Hola.
Aunque se recomienda toouse ExpressRoute, puede elegir cualquier método de conexión más adecuado para su organización. más información sobre ExpressRoute y hello toolearn distintas opciones de conectividad con ExpressRoute, leer [información general técnica de ExpressRoute](https://aka.ms/Azure/ExpressRoute).

### <a name="2-create-storage-accounts"></a>2. Creación de cuentas de almacenamiento
En la alta disponibilidad de orden toomaintain y evitar la dependencia de una única cuenta de almacenamiento, puede crear dos cuentas de almacenamiento. Dividir máquinas hello en cada conjunto de disponibilidad en dos grupos y, a continuación, asigne a cada grupo de una cuenta de almacenamiento independiente.

![Creación de cuentas de almacenamiento](./media/active-directory-aadconnect-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3. Creación de conjuntos de disponibilidad
Para cada rol (controlador de dominio/AD FS y WAP), crear conjuntos de disponibilidad que va a contener 2 máquinas en hello mínimo. Esto le ayudará a lograr una mayor disponibilidad para cada rol. Mientras conjuntos de creación de hello de disponibilidad, es esencial toodecide en siguientes hello:

* **Dominios de error**: Hola de máquinas virtuales en el mismo recurso compartido de dominio de error Hola misma fuente de alimentación y el conmutador de red físico. Se recomienda un mínimo de dos dominios de error. valor predeterminado de Hello es 3 y puede dejarla como está para el propósito de Hola de esta implementación
* **Actualizar dominios**: máquinas que pertenecen toohello al mismo dominio de actualización se reinician juntas durante una actualización. Desea toohave mínimo 2 dominios de actualización. valor predeterminado de Hello es 5 y puede dejarla como está para el propósito de Hola de esta implementación

![Conjuntos de disponibilidad](./media/active-directory-aadconnect-azure-adfs/availabilityset1.png)

Crear hello siguientes conjuntos de disponibilidad

| Conjunto de disponibilidad | Rol | Dominios de error | Dominios de actualización |
|:---:|:---:|:---:|:--- |
| contosodcset |DC/ADFS |3 |5 |
| contosowapset |WAP |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4. Implementación de máquinas virtuales
Hola siguiente paso es máquinas virtuales de toodeploy que va a hospedar roles diferentes de hello en su infraestructura. Se recomienda un mínimo de dos máquinas en cada conjunto de disponibilidad. Cree cuatro máquinas virtuales para la implementación básica de Hola.

| Máquina | Rol | Subred | Conjunto de disponibilidad | Cuenta de almacenamiento | Dirección IP |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |DC/ADFS |INT |contosodcset |contososac1 |Estática |
| contosodc2 |DC/ADFS |INT |contosodcset |contososac2 |Estática |
| contosowap1 |WAP |DMZ |contosowapset |contososac1 |Estática |
| contosowap2 |WAP |DMZ |contosowapset |contososac2 |Estática |

Como habrá observado, no se ha especificado ningún NSG. Esto es porque azure le permite usar NSG en el nivel de subred Hola. A continuación, puede controlar el tráfico de red de máquina mediante hello que NSG individual asociado ya sea subred Hola o bien objeto NIC de Hola. Para más información consulte [¿Qué es un grupo de seguridad de red?](https://aka.ms/Azure/NSG)
Se recomienda la dirección IP estática si está administrando Hola DNS. Puede usar DNS de Azure y en su lugar en los registros DNS hello para el dominio, vea toohello nuevas máquinas por sus nombres de dominio completos de Azure.
El panel de la máquina virtual debe ser similar a continuación una vez completada la implementación de hello:

![Máquinas virtuales implementadas](./media/active-directory-aadconnect-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-hello-domain-controller--ad-fs-servers"></a>5. Configurar controlador de dominio de Hola / servidores de AD FS
 En orden tooauthenticate cualquier solicitud entrante, AD FS tendrá controlador de dominio de toocontact Hola. toosave hello costosas de ida y vuelta desde el controlador de dominio de Azure tooon-local para la autenticación, se recomienda toodeploy una réplica de controlador de dominio de hello en Azure. En orden tooattain la alta disponibilidad, se recomienda toocreate un conjunto de disponibilidad como mínimo 2 de controladores de dominio.

| Controlador de dominio | Rol | Cuenta de almacenamiento |
|:---:|:---:|:---:|
| contosodc1 |Réplica |contososac1 |
| contosodc2 |Réplica |contososac2 |

* Promocionar a dos servidores de hello como controladores de dominio de réplica con DNS
* Configure los servidores de hello AD FS mediante la instalación de rol de hello AD FS con el Administrador de servidor de Hola.

### <a name="6-deploying-internal-load-balancer-ilb"></a>6. Implementación del Equilibrador de carga interno (ILB)
**6.1. Crear hello ILB**

toodeploy un ILB, seleccione equilibradores de carga en hello portal de Azure y haga clic en suma (+).

> [!NOTE]
> Si no ve **equilibradores de carga** en el menú, haga clic en **examinar** Hola inferior izquierda del portal de Hola y desplácese hasta que vea **equilibradores de carga**.  A continuación, haga clic en tooadd estrella amarilla Hola se tooyour menú. Ahora seleccione Hola nueva configuración equilibrador de carga icono tooopen Hola panel toobegin Hola de equilibrador de carga.
> 
> 

![Examinar el equilibrador de carga](./media/active-directory-aadconnect-azure-adfs/browseloadbalancer.png)

* **Nombre**: conceder a cualquier equilibrador de carga de toohello nombre adecuado
* **Esquema**: puesto que este equilibrador de carga se colocarán delante de los servidores de hello AD FS y está pensado para las conexiones de red interna, seleccione "Interno"
* **Red virtual**: elija la red virtual de Hola donde va a implementar AD FS
* **Subred**: elija Hola aquí en la subred interna
* **Asignación de dirección IP**: Estática

![Equilibrador de carga interno](./media/active-directory-aadconnect-azure-adfs/ilbdeployment1.png)

Tras hacer clic en crear y se implementa hello ILB, debería aparecer en lista de Hola de equilibradores de carga:

![Equilibradores de carga después del ILB](./media/active-directory-aadconnect-azure-adfs/ilbdeployment2.png)

Siguiente paso es tooconfigure grupo back-end de Hola y el sondeo de back-end de Hola.

**6.2. Configuración del grupo back-end del ILB**

Seleccione hello recién creado ILB en el panel de hello equilibradores de carga. Se abrirá el panel de configuración de Hola. 

1. Seleccione grupos back-end desde el panel de configuración de Hola
2. Hola, agregar el panel de grupo back-end, haga clic en Agregar una máquina virtual
3. Aparecerá un panel donde puede elegir el conjunto de disponibilidad.
4. Elija el conjunto de disponibilidad de hello AD FS

![Configuración del grupo back-end del ILB](./media/active-directory-aadconnect-azure-adfs/ilbdeployment3.png)

**6.3. Configuración del sondeo**

En el panel de configuración de ILB de hello, seleccione los sondeos.

1. Haga clic en Agregar.
2. Proporcione la información para el sondeo a. **Nombre**: nombre del sondeo b. **Protocolo**: TCP c. **Puerto**: 443 (HTTPS) d. **Intervalo**: 5 (valor predeterminado): se trata de intervalo de hello en el que ILB realizarán un sondeo máquinas hello en el grupo de back-end de hello e. **Límite del umbral incorrecto**: 2 (valor predeterminado ue val): se trata de hello umbral de errores de sondeo consecutivos después del cual ILB declarará una máquina en hello back-end grupo no responde y detención del envío tráfico tooit.

![Configuración del sondeo del ILB](./media/active-directory-aadconnect-azure-adfs/ilbdeployment4.png)

**6.4. Creación de reglas de equilibrio de carga**

En orden tooeffectively equilibrar Hola tráfico, hello ILB debe configurarse con las reglas de equilibrio de carga. En orden toocreate una regla de equilibrio de carga 

1. Seleccione la regla desde el panel de configuración de Hola de hello ILB equilibrio de carga
2. Haga clic en Agregar en hello panel de regla de equilibrio de carga
3. En hello Agregar panel de regla de equilibrio de carga una. **Nombre**: proporcione un nombre para la regla de hello b. **Protocolo**: seleccione TCP c. **Puerto**: 443 d. **Puerto back-end**: 443 e. **Grupo back-end**: seleccione grupo de Hola que creó para AD FS hello clúster f anterior. **Sondeo**: sondeo Hola seleccione creado anteriormente para servidores de AD FS

![Configuración de las reglas de equilibrio de carga](./media/active-directory-aadconnect-azure-adfs/ilbdeployment5.png)

**6.5. Actualización de DNS con el ILB**

Vaya tooyour servidor DNS y crear un CNAME para hello ILB. Hola CNAME debería ser para servicio de federación de Hola por dirección IP de Hola que señala la dirección IP de toohello de hello ILB. Por ejemplo, si Hola dirección DIP de ILB es 10.3.0.8 y el servicio de federación de hello instalado es fs.contoso.com, a continuación, crear un CNAME para fs.contoso.com que apunte too10.3.0.8.
Así se asegurará de que todas las comunicaciones con respecto a fs.contoso.com acabar en hello ILB y se enrutan correctamente.

### <a name="7-configuring-hello-web-application-proxy-server"></a>7. Configuración de servidor Proxy de aplicación Web de Hola
**7.1. Configurar servidores de hello Web Application Proxy servidores tooreach AD FS**

En orden tooensure que los servidores Proxy de aplicación Web son servidores de hello AD FS de tooreach pueda detrás de hello ILB, cree un registro de hello %systemroot%\system32\drivers\etc\hosts para hello ILB. Tenga en cuenta que Hola nombre distintivo (DN) debe ser el nombre de servicio de federación de hello, por ejemplo, fs.contoso.com. Y entrada de hello IP debe ser de dirección IP del ILB Hola (10.3.0.8 como en el ejemplo de Hola).

**7.2. Instalar el rol de Proxy de aplicación Web de Hola**

Después de asegurarse de que los servidores Proxy de aplicación Web son servidores de hello AD FS de tooreach pueda detrás de ILB, a continuación puede instalar a servidores de Proxy de aplicación Web de Hola. Servidores Proxy de aplicación Web no sean toohello Unidos a un dominio. Instalar roles de Proxy de aplicación Web de hello en dos servidores de Proxy de aplicación Web Hola seleccionando Hola rol de acceso remoto. el administrador del servidor Hello le ayudará a instalación de toocomplete Hola WAP.
Para obtener más información acerca de cómo leer toodeploy WAP, [instalar y configurar el servidor de Proxy de aplicación Web de hello](https://technet.microsoft.com/library/dn383662.aspx).

### <a name="8--deploying-hello-internet-facing-public-load-balancer"></a>8.  Implementar Hola Internet orientada hacia el (público) de equilibrador de carga
**8.1.  Creación del equilibrador de carga accesible desde Internet (público)**

Hola portal de Azure, seleccione equilibradores de carga y, a continuación, haga clic en Agregar. En el panel de equilibrador de carga de crear hello, escriba Hola siguiente información

1. **Nombre**: nombre para el equilibrador de carga de Hola
2. **Esquema**: público; esta opción indica a Azure que este equilibrador de carga necesitará una dirección pública.
3. **Dirección IP**: crea una dirección IP (dinámica).

![Equilibrador de carga accesible desde Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment1.png)

Después de la implementación, el equilibrador de carga de hello aparecerá en lista de equilibradores de carga de Hola.

![Lista de equilibradores de carga](./media/active-directory-aadconnect-azure-adfs/elbdeployment2.png)

**8.2. Asignar una dirección IP pública de toohello etiqueta DNS**

Haga clic en la entrada de equilibrador de carga de hello recién creado en hello carga equilibradores panel toobring panel hello para la configuración. Siga por debajo de la etiqueta de pasos tooconfigure Hola DNS para la dirección IP pública hello:

1. Haga clic en la dirección IP pública Hola. Se abrirá el panel de hello para la dirección IP pública hello y su configuración
2. Haga clic en Configuración.
3. Proporcione una etiqueta DNS. Esto se convertirá en la etiqueta DNS pública Hola que puede tener acceso desde cualquier lugar, por ejemplo contosofs.westus.cloudapp.azure.com. Puede agregar una entrada en hello (contosofs.westus.cloudapp.azure.com) de equilibrador de carga de DNS externo para servicio de federación de hello (por ejemplo, fs.contoso.com) que se resuelve toohello etiqueta DNS de hello externo.

![Configuración del equilibrador de carga accesible desde Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment3.png) 

![Configuración del equilibrador de carga accesible desde Internet (DNS)](./media/active-directory-aadconnect-azure-adfs/elbdeployment4.png)

**8.3. Configuración de un grupo back-end para el equilibrador de carga accesible desde Internet (público)** 

Hola seguimiento mismo pasos al igual que en la creación de equilibrador de carga interno de hello, grupo de back-end de hello tooconfigure para Internet con conexión a (público) equilibrador de carga como disponibilidad Hola establecido para los servidores WAP Hola. Por ejemplo, contosowapset.

![Configuración del grupo back-end del equilibrador de carga accesible desde Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment5.png)

**8.4. Configuración del sondeo**

Siga Hola mismo pasos como en configuración de sondeo del equilibrador tooconfigure Hola de Hola de carga interno para el grupo de back-end de Hola de los servidores WAP.

![Configuración del sondeo del equilibrador de carga accesible desde Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment6.png)

**8.5. Creación de reglas de equilibrio de carga**

Siga los mismos pasos de equilibrio de carga de ILB tooconfigure Hola de regla para TCP 443 de Hola.

![Configuración de reglas de equilibrio del equilibrador de carga accesible desde Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment7.png)

### <a name="9-securing-hello-network"></a>9. Protección de red de Hola
**9.1. Protección de subred interna Hola**

En general, deberá Hola siguiendo reglas tooefficiently proteger su subred interna (en orden de hello como se muestra a continuación)

| Regla | Descripción | Flujo |
|:--- |:--- |:---:|
| AllowHTTPSFromDMZ |Permitir la comunicación de HTTPS de Hola de red Perimetral |Entrada |
| DenyInternetOutbound |No hay toointernet de acceso |Salida |

![Reglas de acceso INT (entrantes)](./media/active-directory-aadconnect-azure-adfs/nsg_int.png)

[comentario]: <> (![reglas de acceso INT (entrantes)](./media/active-directory-aadconnect-azure-adfs/nsgintinbound.png)) [comentario]: <> (![reglas de acceso INT (salientes)](./media/active-directory-aadconnect-azure-adfs/nsgintoutbound.png))

**9.2. Protección de subred de la red Perimetral de Hola**

| Regla | Descripción | Flujo |
|:--- |:--- |:---:|
| AllowHTTPSFromInternet |Permitir HTTPS de internet toohello DMZ |Entrada |
| DenyInternetOutbound |Nada salvo toointernet HTTPS está bloqueado |Salida |

![Reglas de acceso EXT (entrantes)](./media/active-directory-aadconnect-azure-adfs/nsg_dmz.png)

[comentario]: <> (![reglas de acceso EXT (entrantes)](./media/active-directory-aadconnect-azure-adfs/nsgdmzinbound.png)) [comentario]: <> (![reglas de acceso EXT (salientes)](./media/active-directory-aadconnect-azure-adfs/nsgdmzoutbound.png))

> [!NOTE]
> Si se requiere la autenticación del certificado de usuario del cliente (autenticación de clientTLS mediante certificados de usuario X509), AD FS necesitará que el puerto TCP 49443 esté habilitado para el acceso de entrada.
> 
> 

### <a name="10-test-hello-ad-fs-sign-in"></a>10. Probar en el inicio de sesión de hello AD FS
Hello más sencillo es tootest que AD FS es mediante hello IdpInitiatedSignon.aspx página. En orden toobe capaz de toodo, que es necesario tooenable Hola IdpInitiatedSignOn en las propiedades de hello AD FS. Siga estos pasos hello tooverify el programa de instalación de AD FS

1. Ejecución Hola por debajo de cmdlet en el servidor de hello AD FS, con PowerShell, tooset, tooenabled.
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true 
2. Desde cualquier acceso de equipo externo https://adfs.thecloudadvocate.com/adfs/ls/IdpInitiatedSignon.aspx  
3. Debería ver la página de hello AD FS como las siguientes:

![Prueba de la página de inicio de sesión](./media/active-directory-aadconnect-azure-adfs/test1.png)

Cuando se inicia sesión correctamente, aparecerá un mensaje de confirmación similar al siguiente:

![Prueba correcta](./media/active-directory-aadconnect-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>Plantilla de implementación de AD FS en Azure
plantilla de Hello implementa una configuración del 6 equipo, 2 para controladores de dominio, AD FS y WAP.

[Plantilla de implementación de AD FS en Azure](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

Puede usar una red virtual existente o crear una nueva red virtual durante la implementación de esta plantilla. Hola varios parámetros disponibles para personalizar la implementación de Hola se enumeran a continuación con la descripción de Hola de uso del parámetro de Hola Hola proceso de implementación. 

| Parámetro | Descripción |
|:--- |:--- |
| Ubicación |recursos de Hello región toodeploy hello en, por ejemplo, este de EE.. |
| StorageAccountType |tipo de Hola de hello cuenta de almacenamiento creada |
| VirtualNetworkUsage |Indica si se creará una nueva red virtual o se va a utilizar una existente |
| VirtualNetworkName |nombre de Hola de tooCreate de red Virtual de hello, obligatorio en el uso de red virtual nueva o existente |
| VirtualNetworkResourceGroupName |Especifica el nombre de Hola Hola del grupo de recursos donde reside la red virtual existente de Hola. Cuando se usa una red virtual existente, se convierte en un parámetro obligatorio para que implementación de hello pueda encontrar el Id. de Hola de red virtual existente de Hola |
| VirtualNetworkAddressRange |Hola intervalo de direcciones de hello red virtual nueva, es obligatorio si se crea una nueva red virtual |
| InternalSubnetName |nombre de Hola de subred interna de hello, obligatoria en ambas opciones de uso de red virtual (nuevas o existentes) |
| InternalSubnetAddressRange |intervalo de direcciones de Hola de subred interna hello, que contiene Hola ADFS y controladores de dominio servidores, obligatorios si crea una nueva red virtual. |
| DMZSubnetAddressRange |intervalo de direcciones de Hola de subred de red perimetral de hello, que contiene Hola Windows servidores proxy de aplicación, obligatorios si crea una nueva red virtual. |
| DMZSubnetName |nombre de Hola de subred interna de hello, obligatoria en ambas opciones de uso de red virtual (nuevas o existentes). |
| ADDC01NICIPAddress |dirección IP interna de Hola de Hola primer controlador de dominio, esta dirección IP se asignarán estáticamente toohello controlador de dominio y debe ser una dirección ip válida dentro de la subred interna Hola |
| ADDC02NICIPAddress |dirección IP interna de Hola de Hola segundo controlador de dominio, esta dirección IP se asignarán estáticamente toohello controlador de dominio y debe ser una dirección ip válida dentro de la subred interna Hola |
| ADFS01NICIPAddress |dirección IP interna de Hello del primer servidor de ADFS hello, esta dirección IP se asignarán estáticamente toohello servidor de ADFS y debe ser una dirección ip válida dentro de la subred interna Hola |
| ADFS02NICIPAddress |dirección IP interna de Hello del segundo servidor ADFS hello, esta dirección IP se asignarán estáticamente toohello servidor de ADFS y debe ser una dirección ip válida dentro de la subred interna Hola |
| WAP01NICIPAddress |dirección IP interna de Hello del primer servidor de WAP hello, esta dirección IP se asignarán estáticamente servidor WAP de toohello y debe ser una dirección ip válida dentro de la subred de la red Perimetral de Hola |
| WAP02NICIPAddress |dirección IP interna de Hello del segundo servidor WAP hello, esta dirección IP se asignarán estáticamente servidor WAP de toohello y debe ser una dirección ip válida dentro de la subred de la red Perimetral de Hola |
| ADFSLoadBalancerPrivateIPAddress |equilibrador de carga de la dirección IP interna de Hola de hello ADFS, esta dirección IP se asignarán estáticamente toohello equilibrador de carga y debe ser una dirección ip válida dentro de la subred interna Hola |
| ADDCVMNamePrefix |Prefijo del nombre de máquina virtual para los controladores de dominio |
| ADFSVMNamePrefix |Prefijo del nombre de máquina virtual para los servidores ADFS |
| WAPVMNamePrefix |Prefijo del nombre de máquina virtual para los servidores WAP |
| ADDCVMSize |tamaño de máquina virtual de Hola de hello controladores de dominio |
| ADFSVMSize |tamaño de máquina virtual de Hola de servidores ADFS de Hola |
| WAPVMSize |tamaño de los servidores WAP Hola de Hello memoria virtual |
| AdminUserName |nombre de Hola de Hola administrador local de máquinas virtuales de Hola |
| AdminPassword |contraseña de Hello para la cuenta de administrador local de Hola de máquinas virtuales de Hola |

## <a name="additional-resources"></a>Recursos adicionales
* [Conjuntos de disponibilidad](https://aka.ms/Azure/Availability) 
* [Equilibrador de carga de Azure](https://aka.ms/Azure/ILB)
* [Equilibrador de carga interno](https://aka.ms/Azure/ILB/Internal)
* [Equilibrador de carga accesible desde Internet](https://aka.ms/Azure/ILB/Internet)
* [Cuentas de almacenamiento](https://aka.ms/Azure/Storage)
* [Redes virtuales de Azure](https://aka.ms/Azure/VNet)
* [AD FS y vínculos de proxy de aplicación web](http://aka.ms/ADFSLinks) 

## <a name="next-steps"></a>Pasos siguientes
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
* [Configuración y administración de AD FS con Azure AD Connect](active-directory-aadconnectfed-whatis.md)
* [Implementación de AD FS en Azure de alta disponibilidad entre regiones geográficas con Azure Traffic Manager](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)

