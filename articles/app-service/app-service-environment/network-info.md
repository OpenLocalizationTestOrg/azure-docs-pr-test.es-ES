---
title: Consideraciones de aaaNetworking con un entorno de servicio de aplicaciones de Azure
description: "Explica el tráfico de red Hola ASE y cómo tooset NSG y UDRs con su ASE"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 955a4d84-94ca-418d-aa79-b57a5eb8cb85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ccompy
ms.openlocfilehash: d4d3000f4d4d75814b1e6d47079d967334eb1a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-an-app-service-environment"></a>Consideraciones de red para una instancia de App Service Environment #

## <a name="overview"></a>Información general ##

 [Azure App Service Environment][Intro] es una implementación de Azure App Service en una subred de Azure Virtual Network (VNet). Hay dos tipos de implementación de una instancia de App Service Environment (ASE):

- **ASE externo**: expone Hola aplicaciones ASE hospedado en una dirección IP accesible desde internet. Para más información, consulte [Creación de una instancia externa de App Service Environment][MakeExternalASE].
- **ILB ASE**: expone Hola aplicaciones ASE hospedado en una dirección IP dentro de la red virtual. extremo interno de Hello es un equilibrador de carga interno (ILB), que es la razón por la que se denomina una ASE de ILB. Para más información, consulte [Creación y uso de un ASE de ILB][MakeILBASE].

Ahora hay dos versiones de App Service Environment: ASEv1 y ASEv2. Para obtener información sobre ASEv1, consulte [Introducción tooApp v1 de entorno del servicio][ASEv1Intro]. Una instancia de ASEv1 se puede implementar en una red virtual clásica o en una de Resource Manager. En el caso de ASEv2, la implementación solo se puede realizar en una red virtual de Resource Manager.

Todas las llamadas desde una ASE que vaya toohello internet deje Hola red virtual a través de una VIP asignada para hello ASE. Hola IP pública de esta dirección VIP es, a continuación, IP de origen de Hola para todas las llamadas de hello ASE que vaya toohello internet. Si Hola aplicaciones en su ASE realiza llamadas tooresources en la red virtual o a través de una VPN, IP de origen de hello es uno de Hola direcciones IP de subred Hola utilizado por su ASE. Porque hello ASE es dentro de la red virtual de hello, también puede tener acceso a los recursos dentro de hello red virtual sin ninguna configuración adicional. Si hello red virtual es la red local de tooyour conectado, aplicaciones en su ASE también tienen acceso tooresources no existe. No es necesario tooconfigure Hola ASE o la aplicación cualquier aún más.

![ASE externo][1] 

Si tienes un ASE externo, VIP pública hello también es que las aplicaciones de ASE resuelvan toofor de punto de conexión de hello:

* HTTP/S. 
* FTP/S. 
* Implementación web.
* Depuración remota.

![ASE de ILB][2]

Si tiene una ASE de ILB, dirección IP de Hola de hello ILB es el punto de conexión de Hola para HTTP/S, FTP/S, implementación web y depuración remota.

puertos de acceso de aplicación normal de Hello son:

| Uso | De | demasiado|
|----------|---------|-------------|
|  HTTP/HTTPS  | Configurable por el usuario |  80, 443 |
|  FTP/FTPS    | Configurable por el usuario |  21, 990, 10001-10020 |
|  Depuración remota en Visual Studio  |  Configurable por el usuario |  4016, 4018, 4020, 4022 |

Es así tanto si está en un ASE externo como en un ASE de ILB. Si se encuentra en un ASE externo, se alcanza los puertos de VIP pública Hola. Si se encuentra en un ASE ILB, alcanza los puertos de hello ILB. Si bloquea el puerto 443, puede haber un efecto sobre algunas características que se exponen en el portal de Hola. Para más información, consulte [Dependencias del portal](#portaldep).

## <a name="ase-dependencies"></a>Dependencias de ASE ##

Un dependencia de acceso de entrada de ASE es:

| Uso | De | demasiado|
|-----|------|----|
| Administración | Direcciones de administración de App Service | Subred de ASE: 454, 455 |
|  Comunicación interna ASE | Subred de ASE: todos los puertos | Subred de ASE: todos los puertos
|  Permitir entrada de Azure Load Balancer | Azure Load Balancer | Subred de ASE: todos los puertos
|  Direcciones IP asignadas a las aplicaciones | Direcciones asignadas a las aplicaciones | Subred de ASE: todos los puertos

Hello tráfico entrante proporciona comando y control de ASE de hello en la supervisión de toosystem de adición. direcciones IP de origen de Hola para este tráfico se enumeran en hello [ASE administración direcciones] [ ASEManagement] documento. configuración de seguridad de red de Hello necesita acceso de tooallow de todas las direcciones IP en los puertos 454 y 455.

Dentro de la subred de hello ASE hay muchos puertos utilizan para la comunicación de componente interno y puede cambiar.  Para ello, todos los puertos de hello en hello ASE subred toobe accesible desde la subred de ASE Hola. 

Para la comunicación de hello entre equilibrador de carga de Azure de Hola y puertos mínimos de hello ASE subred Hola ese toobe necesidad de abrir son 454 y 455, 16001. puerto 16001 Hola se utiliza para mantener activa tráfico entre equilibrador de carga de Hola y Hola ASE. Si utilizas una ASE de ILB, a continuación, se puede bloquear el tráfico hacia abajo toojust Hola 454, 455, 16001 puertos.  Si usas un ASE externo debe tootake en puertos de acceso de cuenta Hola aplicación normal.  Si se utilizan direcciones de la aplicación asignada necesita tooopen se tooall puertos.  Cuando se asigna una dirección tooa de aplicación específica, equilibrador de carga de hello usará los puertos que no se conocen de antemano toosend HTTP y HTTPS tráfico toohello ASE.

Si se utilizan direcciones IP de aplicación asignada debe tooallow tráfico de direcciones IP asignan subred de tooyour aplicaciones toohello ASE de Hola.

Para el acceso de salida, un ASE depende de varios sistemas externos. Esas dependencias del sistema se definen con nombres DNS y no asignan tooa un conjunto fijo de direcciones IP. Por lo tanto, Hola ASE necesita acceso de salida de hello ASE subred tooall direcciones IP externas en una variedad de puertos. Un ASE tiene Hola siguiendo las dependencias salientes:

| Uso | De | demasiado|
|-----|------|----|
| Azure Storage | Subred de ASE | table.core.windows.net, blob.core.windows.net, queue.core.windows.net, file.core.windows.net: 80, 443, 445 (445 se necesita solo para ASEv1). |
| Azure SQL Database | Subred de ASE | database.windows.net: 1433, 11000-11999, 14000-14999 (Para más información, consulte [Uso de los puertos de SQL Database V12](../../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md)).|
| Administración de Azure | Subred de ASE | management.core.windows.net, management.azure.com: 443 
| Comprobación de certificado SSL |  Subred de ASE            |  ocsp.msocsp.com, mscrl.microsoft.com, crl.microsoft.com: 443
| Azure Active Directory        | Subred de ASE            |  Internet: 443
| Administración de App Service        | Subred de ASE            |  Internet: 443
| DNS de Azure                     | Subred de ASE            |  Internet: 53
| Comunicación interna ASE    | Subred de ASE: todos los puertos |  Subred de ASE: todos los puertos

Si Hola ASE pierde el acceso a las dependencias de toothese, deja de funcionar. Cuando esto ocurre tiempo suficiente, Hola ASE se suspende.

### <a name="customer-dns"></a>DNS del cliente ###

Si hello red virtual esté configurada con un servidor DNS definido por el cliente, las cargas de trabajo de inquilino de hello utilizan. Hola ASE sigue necesitando toocommunicate con DNS de Azure para fines de administración. 

Si hello red virtual está configurado con un cliente DNS en Hola otro lado de una VPN, servidor DNS de hello debe ser accesible desde la subred de Hola que contiene ASE Hola.

<a name="portaldep"></a>

## <a name="portal-dependencies"></a>Dependencias del portal ##

En dependencias funcionales toohello ASE de adición, hay algunos elementos adicionales relacionados toohello portal experiencia. Algunas de las capacidades de Hola Hola portal de Azure dependen de acceso directo too_SCM site_. Para cada aplicación en Azure App Service, hay dos direcciones URL. la primera dirección URL de Hello es tooaccess la aplicación. dirección URL del segundo Hello es sitio SCM hello tooaccess, que también se denomina hello _consola Kudu_. Características que usan el sitio SCM Hola incluyen:

-   Trabajos web
-   Functions
-   Secuencias de registro
-   Kudu
-   Extensiones
-   Explorador de procesos
-   Consola

Cuando se usa una ASE de ILB, sitio SCM de hello no es accesible desde fuera de hello red virtual de internet. Cuando la aplicación se hospeda en un ASE ILB, algunas funciones no funcionará desde el portal de Hola.  

Muchas de estas capacidades que dependen de sitio SCM hello también están disponibles directamente en la consola de Kudu Hola. Puede conectarse tooit directamente en lugar de usar el portal de Hola. Si la aplicación se hospeda en un ASE ILB, use la publicación toosign de credenciales en. Hola URL tooaccess Hola SCM sitio de una aplicación hospedada en un ASE ILB tiene Hola siguiendo el formato: 

```
<appname>.scm.<domain name hello ILB ASE was created with> 
```

Si su ASE ILB es el nombre de dominio de hello *contoso.net* y el nombre de la aplicación es *testapp*, aplicación hello se alcanza a *testapp.contoso.net*. sitio SCM Hola que lo acompaña se alcanza a *testapp.scm.contoso.net*.

### <a name="functions-and-web-jobs"></a>Trabajos web y de funciones ###

Funciones y Web trabajos dependen de sitio SCM Hola pero se admiten para su uso en el portal de hello, incluso si las aplicaciones en un ASE ILB, siempre y cuando el explorador puede llegar a sitio de hello SCM.  Si está utilizando un certificado autofirmado con su ASE ILB, será necesario tooenable su tootrust de explorador de certificados.  Para Internet Explorer y borde que significa que el certificado de hello tiene toobe de confianza del equipo de hello almacenar.  Si usas Chrome, a continuación, significa que acepta certificados de hello en el Explorador de hello anteriormente pulsando supuestamente sitio scm de hello directamente.  Hola mejor solución es toouse un certificado comercial que se encuentra en la cadena del explorador de Hola de confianza.  

## <a name="ase-ip-addresses"></a>Direcciones IP de ASE ##

Un ASE tiene unos toobe de direcciones IP que tenga en cuenta. Son las siguientes:

- **Dirección IP pública de entrada**: se usa para el tráfico de la aplicación en un ASE externo y para el tráfico de administración tanto en un ASE externo como en un ASE de ILB.
- **IP pública saliente**: usar como Hola "de" IP para las conexiones salientes de hello ASE ese Hola deje de red virtual, que no se enruta hacia abajo una VPN.
- **Dirección IP del ILB:**: si usa una ASE de ILB.
- **Direcciones SSL basadas en IP asignadas a la aplicación**: solo son posibles con un ASE externo y cuando hay configurada una SSL basada en IP.

Todas estas direcciones IP son fácilmente visibles en un ASEv2 Hola portal de Azure de hello ASE interfaz de usuario. Si tiene una ASE de ILB, se muestra hello IP para hello ILB.

![Direcciones IP][3]

### <a name="app-assigned-ip-addresses"></a>Direcciones IP asignadas a la aplicación ###

Con un ASE externo, puede asignar direcciones IP tooindividual aplicaciones. No puede hacer eso con un ASE de ILB. Para obtener más información acerca de cómo tooconfigure su aplicación toohave su propia dirección IP, consulte [enlazar una existente personalizado SSL certificado tooAzure aplicaciones web](../../app-service-web/app-service-web-tutorial-custom-ssl.md).

Cuando una aplicación tiene su propia dirección SSL basado en IP, Hola ASE reserva de dirección IP toothat de dos puertos toomap. Un puerto es para el tráfico HTTP y hello otro puerto es para HTTPS. Estos puertos se enumeran en hello ASE interfaz de usuario en la sección de direcciones IP de Hola. Tráfico debe ser capaz de tooreach esos puertos de VIP de Hola o aplicaciones de hello son inaccesibles. Este requisito es importante tooremember al configurar grupos de seguridad de red (NSG).

## <a name="network-security-groups"></a>Grupos de seguridad de red ##

[Grupos de seguridad de red] [ NSGs] proporcionan acceso de red de hello capacidad toocontrol dentro de una red virtual. Si se usa el portal de hello, hay un modo implícito deny de regla en hello menor prioridad toodeny todo. Lo que crea son las reglas de permiso.

En un ASE, no tienes acceso toohello máquinas virtuales que usan toohost Hola ASE propio. Están en una suscripción administrada por Microsoft. Si desea que toorestrict acceso toohello aplicaciones en hello ASE, establezca los NSG de subred de ASE Hola. Si lo hace, preste atención cuidado las dependencias de ASE toohello. Si se bloquea todas las dependencias, Hola ASE deja de funcionar.

Los NSG pueden configurarse a través del portal de Azure de Hola o a través de PowerShell. información de Hello aquí muestra hello portal de Azure. Puede crear y administrar los NSG en el portal de Hola como un recurso de nivel superior bajo **red**.

Cuando hello se tienen requisitos de entrada y salidos en la cuenta, hello NSG debe tener un aspecto similar NSG toohello se muestra en este ejemplo. es el intervalo de direcciones de red virtual de Hello _192.168.250.0/16_, y es Hola subred ASE hello en _192.168.251.128/25_.

se muestran los requisitos de entrada primero dos de Hola para hello ASE toofunction princip Hola de lista de hello en este ejemplo. Permiten la administración ASE y permitir Hola ASE toocommunicate consigo misma. Hello las demás entradas son todos los inquilinos configurable y pueden administrar aplicaciones de toohello hospedadas en ASE de acceso de red. 

![Reglas de seguridad de entrada][4]

Una regla predeterminada permite Hola direcciones IP de subred de hello red virtual tootalk toohello ASE. Otra regla predeterminada permite equilibrador de carga de hello, también conocido como VIP pública hello, toocommunicate con hello ASE. Seleccione las reglas predeterminadas de Hola de toosee, **reglas predeterminadas** toohello siguiente **agregar** icono. Si coloca una instrucción deny de todo lo demás regla después de hello NSG reglas se muestra, se evita que el tráfico entre la VIP de Hola y Hola ASE. tooprevent el tráfico que llegue desde dentro de Hola de red virtual, agregue su propios tooallow regla entrante. Usar un tooAzureLoadBalancer igual de origen con un destino de **cualquier** y un intervalo de puertos de  **\*** . Como regla NSG hello es toohello aplicado ASE subred, no es necesario toobe específica en el destino de Hola.

Si asigna una aplicación de tooyour de dirección IP, asegúrese de que mantener Hola puertos abiertos. seleccionar puertos de hello toosee, **entono** > **direcciones IP**.  

Se necesitan todos los elementos de Hola se muestra en hello siguiendo las reglas de salida, excepto el último elemento de saludo. Le permiten dependencias ASE de toohello de acceso de red que se indicaron anteriormente en este artículo. Si bloquea alguna de ellas, el ASE deja de funcionar. último elemento de lista de Hola de Hello permite su toocommunicate ASE con otros recursos de la red virtual.

![Reglas de seguridad de entrada][5]

Una vez definidos sus NSG, asignarlos subred toohello que su ASE está activado. Si no recuerdas Hola ASE VNet o subred, puede ver desde el portal de administración de hello ASE. tooassign Hola subred tooyour NSG, vaya toohello subred interfaz de usuario y seleccione hello NSG.

## <a name="routes"></a>Rutas ##

Las rutas presentan problemas sobre todo cuando la red virtual se configura con Azure ExpressRoute. Hay tres tipos de rutas en una red virtual:

-   Rutas del sistema
-   Rutas BGP
-   Rutas definidas por el usuario (UDR)

Las rutas BGP reemplazan a las rutas del sistema. Las UDR reemplazan a las rutas BGP. Para más información acerca de las rutas en las redes virtuales de Azure, consulte la [Introducción a las rutas definidas por el usuario][UDRs].

base de datos de SQL Azure de Hola Hola ASE utilizado por sistema de hello toomanage tiene un firewall. Requiere comunicación toooriginate de hello VIP pública ASE. Si se envían hacia abajo Hola conexión ExpressRoute y otra dirección IP, se denegarán las conexiones toohello base de datos SQL ASE Hola.

Si se envían las solicitudes de administración de respuestas tooincoming hacia abajo hello ExpressRoute, dirección de respuesta de hello es diferente de destino original Hola. Esta falta de coincidencia interrumpe la comunicación TCP Hola.

Para su toowork ASE mientras la red virtual se configura con una ExpressRoute toodo lo más fácil de hello es:

-   Configurar ExpressRoute tooadvertise _0.0.0.0/0_. De forma predeterminada, obliga a dirigir todo el tráfico saliente tráfico local.
-   Crear un UDR. Aplicar toohello subred que contiene Hola ASE con un prefijo de dirección de _0.0.0.0/0_ y tipo de un próximo salto _Internet_.

Si realiza estos dos cambios, tráfico destinado de internet que se origina en la subred de ASE hello no forzado inactivo ExpressRoute de Hola y Hola ASE funciona. 

> [!IMPORTANT]
> rutas de Hello definidas en un UDR deben ser lo suficientemente específica como tootake prioridad sobre las rutas anunciadas por la configuración de ExpressRoute de Hola. Hello en el ejemplo anterior se usa el intervalo de direcciones de hello amplia 0.0.0.0/0. Puede reemplazarse accidentalmente por los anuncios de ruta con intervalos de direcciones más específicos.
>
> ASEs no son compatibles con las configuraciones de ExpressRoute que entre-anuncian rutas de hello emparejamiento público toohello emparejamiento privado ruta de acceso. Las configuraciones de ExpressRoute con el emparejamiento público configurado reciben anuncios de ruta de Microsoft. los anuncios de Hola contienen un gran conjunto de intervalos de direcciones IP de Microsoft Azure. Si los intervalos de direcciones de hello entre anunciados en ruta de acceso privada emparejamiento hello, todos los paquetes de red saliente de la subred de Hola de ASE son infraestructura de red local del cliente de túnel tooa force. Actualmente, este flujo de red no es compatible con las instancias de ASE. Un problema de toothis de solución es rutas de toostop entre anuncios de Hola emparejamiento público toohello emparejamiento privado ruta de acceso.

toocreate un UDR, siga estos pasos:

1. Vaya toohello portal de Azure. Seleccione **Redes** > **Tablas de rutas**.

2. Crear una nueva tabla de rutas en hello misma región que la red virtual.

3. En la interfaz de usuario de la tabla de rutas, seleccione **Rutas** > **Agregar**.

4. Conjunto hello **tipo de salto siguiente** demasiado**Internet** hello y **prefijo de dirección** demasiado**0.0.0.0/0**. Seleccione **Guardar**.

    A continuación, verá algo parecido a Hola siguiente:

    ![Rutas funcionales][6]

5. Después de crear la nueva tabla de rutas hello, vaya toohello subred que contiene su ASE. Seleccione la tabla de rutas de lista de hello en el portal de Hola. Después de guardar los cambios de hello, a continuación, debería ver Hola NSG y rutas que se anotan con la subred.

    ![NSG y rutas][7]

### <a name="deploy-into-existing-azure-virtual-networks-that-are-integrated-with-expressroute"></a>Implementación en redes virtuales de Azure existentes que están integradas con ExpressRoute ###

toodeploy su ASE en una red virtual que se integra con ExpressRoute, preconfigurar subred Hola donde desea ASE Hola implementado. A continuación, utilice un toodeploy de plantilla de administrador de recursos se. toocreate un ASE en una red virtual que ya tiene configurado de ExpressRoute:

- Crear un Hola de toohost ASE de subred.

    > [!NOTE]
    > Nada más puede estar en la subred Hola pero ASE Hola. Ser toochoose seguro de un espacio de direcciones que permite el crecimiento futuro. No puede cambiar esta configuración posteriormente. Se recomienda un tamaño de `/25` con ciento veintiocho direcciones.

- Cree UDRs (por ejemplo, tablas de rutas) como se describió anteriormente y establezca en la subred de Hola.
- Crear Hola ASE mediante una plantilla de administrador de recursos, como se describe en [crear un ASE mediante una plantilla de administrador de recursos][MakeASEfromTemplate].

<!--Image references-->
[1]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow.png
[2]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow2.png
[3]: ./media/network_considerations_with_an_app_service_environment/networkase-ipaddresses.png
[4]: ./media/network_considerations_with_an_app_service_environment/networkase-inboundnsg.png
[5]: ./media/network_considerations_with_an_app_service_environment/networkase-outboundnsg.png
[6]: ./media/network_considerations_with_an_app_service_environment/networkase-udr.png
[7]: ./media/network_considerations_with_an_app_service_environment/networkase-subnet.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ASEManagement]: ./management-addresses.md
