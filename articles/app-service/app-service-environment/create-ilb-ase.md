---
title: aaaCreate y use un equilibrador de carga interno con un entorno de servicio de aplicaciones de Azure
description: "Obtener detalles sobre cómo toocreate y usar un entorno de servicio de aplicaciones de Azure con aislamiento de internet"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: d019ca6f231c3acfdab4cd380db375a076802f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a>Creación y uso de un equilibrador de carga interno con una instancia de App Service Environment #

 Azure App Service Environment es una implementación de Azure App Service en una subred de Azure Virtual Network (VNet). Hay dos toodeploy de formas en un entorno de servicio de aplicaciones (ASE): 

- Con una dirección VIP en una dirección IP externa, a la que se suele hacer referencia como instancia externa de ASE.
- Con una VIP en una dirección IP interna, suele denominar una ASE de ILB porque el extremo interno de hello es un equilibrador de carga interno (ILB). 

Este artículo muestra cómo toocreate una ASE de ILB. Para obtener información general sobre Hola ASE, consulte [entornos del servicio de introducción tooApp][Intro]. toolearn toocreate un ASE externos, vea [crear un ASE externo][MakeExternalASE].

## <a name="overview"></a>Información general ##

Puede implementar un ASE con un punto de conexión accesible por Internet o con una dirección IP en la red virtual. tooset tooa dirección de red virtual, Hola ASE debe implementarse con un ILB de direcciones IP de Hola. Al implementar el ASE con un ILB, debe proporcionar:

-   Su propio dominio, el cual usa al crear sus aplicaciones.
-   certificado de Hello utilizado para HTTPS.
-   Administración de DNS para el dominio.

A cambio, podrá realizar todo esto:

-   Hospedar aplicaciones de intranet segura en la nube de hello, que puede tener acceso a través de un sitio a sitio o una VPN de ExpressRoute de Azure.
-   Aplicaciones de host en la nube de Hola que no aparezcan en los servidores DNS públicos.
-   Crear aplicaciones de back-end aisladas de Internet con las que pueden integrarse de forma segura sus aplicaciones de front-end.

### <a name="disabled-functionality"></a>Funcionalidad deshabilitada ###

Sin embargo, cuando utilice un ASE con un ILB, no podrá realizar algunas operaciones:

-   Use SSL basada en IP.
-   Asignar direcciones IP toospecific aplicaciones.
-   Comprar y usar un certificado con una aplicación a través de hello portal de Azure. Puede obtener certificados directamente en una entidad de certificación y usarlos con sus aplicaciones. No se puede obtenerlas a través de hello portal de Azure.

## <a name="create-an-ilb-ase"></a>Creación de un ASE con un ILB ##

toocreate una ASE de ILB:

1. Hola portal de Azure, seleccione **New** > **Web y móvil** > **entono**.

2. Seleccione su suscripción.

3. Seleccione o cree un grupo de recursos.

4. Cree una red virtual o seleccione una.

5. Si selecciona una red virtual existente, deberá toocreate un Hola de toohold ASE de subred. Asegúrese de que el tamaño de tooset una subred lo suficientemente grande como tooaccommodate crecimiento futuro de su ASE. Recomendamos un tamaño de `/25`, que tiene 128 direcciones y puede controlar los ASE de tamaño máximo. Puede seleccionar el tamaño mínimo Hello es un `/28`. Después de necesidades de infraestructura, este tamaño puede ser tooa escalado máximo de instancias de 11.

    * Vaya más allá del máximo de saludo predeterminado de 100 instancias en los planes de servicio de aplicaciones.

    * Escale cerca de 100, pero con un escalado de front-end más rápido.

6. Seleccione **Red virtual/Ubicación** > **Configuración de red virtual**. Conjunto hello **VIP tipo** demasiado**interno**.

7. Escriba un valor en nombre de dominio. Este dominio es hello uno utilizado para las aplicaciones creadas en esta ASE. Hay algunas restricciones. No puede ser:

    * net   

    * azurewebsites.net

    * p.azurewebsites.net

    * &lt;nombre_del_ASE&gt;.p.azurewebsites.net

   usa el nombre de dominio personalizado de Hola para las aplicaciones y nombre de dominio de hello utilizado por su ASE no se puede superponer. Para una ASE de ILB con el nombre de dominio de hello _contoso.com_, no puede utilizar nombres de dominio personalizados para las aplicaciones como:

    * www.contoso.com

    * abcd.def.contoso.com

    * abcd.contoso.com

   Si conoce los nombres de dominio personalizados de Hola para las aplicaciones, seleccione un dominio para hello ASE de ILB que no tienen un conflicto con los nombres de dominio personalizado. En este ejemplo, puede usar algo parecido a *contoso internal.com* para dominio Hola de su ASE dado que no estén en conflicto con nombres de dominio personalizado que terminan en *. contoso.com*.

8. Seleccione **Aceptar** y después **Crear**.

    ![Creación de ASE][1]

En hello **red Virtual** hoja, hay un **configuración de red Virtual** opción. Puede usar tooselect una VIP externa o una VIP interno. valor predeterminado de Hello es **externo**. Si selecciona **Externa**, el ASE utilizará una dirección VIP accesible de Internet. Si selecciona **Interna**, el ASE se configurará con un ILB en una dirección IP de su red virtual.

Después de seleccionar **interno**, Hola capacidad tooadd más direcciones IP tooyour ASE se quita. En su lugar, debe tooprovide dominio de Hola de hello ASE. En un ASE con una VIP externa, nombre de Hola de hello que ase se usa en el dominio de Hola para las aplicaciones creadas en esa ASE.

Si establece **VIP tipo** demasiado**interno**, el nombre de ASE no se usa en el dominio de Hola para hello ASE. Especifique el dominio de hello explícitamente. Si su dominio es *contoso.corp.net* y crear una aplicación en ASE denominado *timereporting*, Hola dirección URL para que la aplicación es timereporting.contoso.corp.net.


## <a name="create-an-app-in-an-ilb-ase"></a>Creación de una aplicación en un ASE con un ILB ##

Crear una aplicación en un ASE ILB Hola igual que crear una aplicación en un ASE normalmente.

1. Hola portal de Azure, seleccione **New** > **Web y móvil** > **Web** o **Mobile** o  **Aplicación de API de**.

2. Escriba el nombre de Hola de aplicación hello.

3. Seleccione la suscripción de Hola.

4. Seleccione o cree un grupo de recursos.

5. Seleccione o cree un plan del Servicio de aplicaciones. Si desea que toocreate un nuevo plan de servicio de aplicaciones, seleccione su ASE como ubicación de Hola. Seleccione el grupo de trabajo de Hola donde desea que su toobe del plan de servicio de aplicaciones creado. Cuando creas Hola plan de servicio de aplicaciones, seleccione su ASE como ubicación de Hola y el grupo de trabajo de Hola. Cuando se especifica el nombre de Hola de aplicación hello, dominio hello en el nombre de la aplicación se reemplazó por dominio de Hola para su ASE.

6. Seleccione **Crear**. Si desea tooappear de aplicación hello en el panel, seleccione la **toodashboard Pin** casilla de verificación.

    ![Creación del plan de App Service][2]

    En **nombre de la aplicación**, nombre de dominio de hello es el dominio de hello tooreflect actualizada de su ASE.

## <a name="post-ilb-ase-creation-validation"></a>Validación posterior a la creación del ASE con un ILB ##

Una ASE de ILB es ligeramente diferente que hello no - ILB ASE. Como ya se indicó, deberá toomanage su propio DNS. También tiene tooprovide su propio certificado para las conexiones HTTPS.

Después de crear su ASE, nombre de dominio de hello muestra dominio Hola especificado. Aparece un nuevo elemento en el menú **Configuración** denominado **Certificado de ILB**. Hola ASE se crea con un certificado que no especifica el dominio de ILB ASE Hola. Si usas Hola ASE con ese certificado, el explorador le indica que no es válido. Este certificado resulta más fácil tootest HTTPS, pero debe tooupload su propio certificado de dominio de ILB ASE tooyour relacionados. Este paso es necesario independientemente de si el certificado es autofirmado o se adquiere de una entidad de certificación.

![Nombre de dominio del ASE con un ILB][3]

El ASE con un ILB necesita un certificado SSL válido. Use entidades de certificación internas, compre un certificado a un emisor externo o utilice un certificado autofirmado. Independientemente del origen de hello del certificado SSL de hello, hello siguientes atributos de certificado necesitan toobe configurado correctamente:

* **Asunto**: este atributo debe establecerse too*.your raíz dominio aquí.
* **Nombre alternativo del firmante**: este atributo debe incluir tanto **.your-root-domain-here* como **.scm.your-root-domain-here*. Toohello de las conexiones SSL sitio SCM/Kudu asociado a cada aplicación usa una dirección del formulario de hello *your-app-name.scm.your-root-domain-here*.

Certificado SSL de Hola de Convert/Guardar como un archivo. pfx. archivo .pfx de Hello debe incluir todos los intermedio y raíz certificados. Protéjalo con una contraseña.

Si desea toocreate un certificado autofirmado, puede usar comandos de PowerShell de hello aquí. Ser toouse seguro de su nombre de dominio de ILB ASE en lugar de *internal.contoso.com*: 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

exploradores marca certificado Hola que generan estos comandos de PowerShell porque no se creó el certificado de Hola por una entidad de certificación que se encuentra en las cadenas de confianza de su explorador. tooget un certificado que confíe en el explorador, adquirir, de una entidad de certificación comercial en las cadenas de confianza de su explorador. 

![Establecimiento de certificado de ILB][4]

tooupload sus propios certificados y probar el acceso:

1. Después de crea ASE hello, vaya toohello ASE interfaz de usuario. Seleccione **ASE** > **Configuración** > **Certificado de ILB**.

2. certificado ILB de tooset hello, seleccione el archivo .pfx del certificado hello y escribir contraseña de Hola. Este paso toma algunas tooprocess de tiempo. Aparece un mensaje que indica que una operación de carga está en curso.

3. Obtener la dirección ILB de Hola para su ASE. Seleccione **ASE** > **Propiedades** > **Dirección IP virtual**.

4. Crear una aplicación web en su ASE después de crea Hola ASE.

5. Cree una máquina virtual si no dispone de una en la red virtual.

    > [!NOTE] 
    > No intente toocreate esta máquina virtual en Hola misma subred como Hola ASE porque se producirá un error o causar problemas.
    >
    >

6. Establecer Hola DNS para el dominio de ASE. Puede usar un comodín con el dominio en el DNS. toodo algunas sencillas pruebas, edite el archivo de hosts de hello en la máquina virtual tooset hello web app nombre toohello dirección VIP IP:

    a. Si su ASE tiene el nombre de dominio de hello _. ilbase.com_ y crear una aplicación web de hello denominado _mytestapp_, se dirige a _mytestapp.ilbase.com_. A continuación, establezca _mytestapp.ilbase.com_ dirección de tooresolve toohello ILB. (En Windows, el archivo de hosts de hello es en _C:\Windows\System32\drivers\etc\_.)

    b. tootest web implementación publicación o acceso toohello avanzada de consola, cree un registro para _mytestapp.scm.ilbase.com_.

7. Utilice un explorador en esa máquina virtual y vaya a http://mytestapp.ilbase.com (O visite toowhatever que es el nombre de la aplicación web con el dominio.)

8. Utilice un explorador en esa máquina virtual y vaya a https://mytestapp.ilbase.com. Si usa un certificado autofirmado, Aceptar falta Hola de seguridad.

    dirección IP de Hello para el ILB aparece en **direcciones IP**. Esta lista también tiene direcciones IP de hello utilizadas por VIP externa hello y tráfico de administración de entrada.

    ![Dirección IP del ILB][5]

### <a name="web-jobs-functions-and-hello-ilb-ase"></a>Web trabajos, funciones y Hola ASE de ILB

Las funciones y los trabajos web se admiten en un ASE ILB pero para hello toowork portal con ellos, debe tener el sitio de red acceso toohello SCM.  Esto significa que el explorador debe estar en un host que está en o red virtual toohello conectada.  

Cuando se utilizan funciones de Azure en un ASE de ILB, podría obtener un mensaje de error que dice "no somos tooretrieve capaz de sus funciones en este momento. Inténtelo de nuevo más tarde." Este error se produce porque Hola interfaz de usuario de funciones aprovecha sitio SCM de Hola a través de HTTPS y certificado de raíz de hello no está en la cadena del explorador de Hola de confianza. Los trabajos web tienen un problema similar. tooavoid este problema puede realizar una de las siguientes de hello:

- Agregue el almacén de certificados de confianza de hello certificados tooyour. Esto desbloquea Edge e Internet Explorer.
- Usar Chrome y vaya sitio SCM toohello en primer lugar, acepte el certificado de confianza de hello y, a continuación, seguir toohello portal.
- Use un certificado comercial que se encuentre en la cadena de confianza del explorador.  Esto es mejor opción de Hola.  

## <a name="dns-configuration"></a>Configuración de DNS ##

Cuando se utiliza una VIP externa, Hola DNS está administrado por Azure. Cualquier aplicación creada en su ASE se agrega automáticamente tooAzure DNS, que es un DNS público. En un ASE con un ILB tiene que administrar su propio DNS. Para un dominio determinado como _contoso.net_, necesita toocreate DNS A registros en su DNS esa dirección de punto tooyour ILB para:

- *.contoso.net
- *.scm.contoso.net

Si su dominio ASE de ILB se usa para varias cosas fuera de este ASE, tendrá que toomanage DNS según el nombre de aplicación. Este método resulta difícil porque necesita tooadd cada nuevo nombre de aplicación en el DNS al crearlo. Por ello, recomendamos que use un dominio dedicado.

## <a name="publish-with-an-ilb-ase"></a>Publicación con un ASE con un ILB ##

Para cada aplicación que se cree, hay dos puntos de conexión. En un ASE con un ILB, existen *&lt;app name>.&lt;ILB ASE Domain>* y *&lt;app name>.scm.&lt;ILB ASE Domain>*. 

nombre del sitio de Hello SCM toma consola de Kudu toohello, llamado hello **portal avanzada**, dentro Hola portal de Azure. Hola Kudu consola le permite ver las variables de entorno, explorar disco hello, utilice una consola y mucho más. Para más información, consulte [Consola de Kudu para Azure App Service][Kudu]. 

En multiempresa Hola servicio de aplicaciones y en un ASE externos, hay un inicio de sesión único entre Hola portal de Azure y la consola de Kudu Hola. Para hello ASE de ILB, sin embargo, debe toouse su publicación toosign de credenciales en la consola de Kudu Hola.

Sistemas de CI basados en Internet, como GitHub y Visual Studio Team Services, no funcionan con un ASE ILB porque el extremo de publicación de hello no accesible de internet. En su lugar, deberá toouse un sistema de elementos de configuración que utiliza un modelo de extracción, por ejemplo, Dropbox.

publicación de extremos de Hola para las aplicaciones en un ASE ILB usa dominio Hola ese Hola con que ase de ILB se creó. Este dominio aparece en el perfil de publicación de la aplicación hello y en la hoja de portal de la aplicación hello (**Introducción** > **Essentials** y también **propiedades**). Si tienes una ASE de ILB con subdominio hello *contoso.net* y una aplicación denominada *MiPrueba*, use *mytest.contoso.net* para FTP y *mytest.scm.contoso.net*  para la implementación web.

## <a name="couple-an-ilb-ase-with-a-waf-device"></a>Acoplamiento de un ASE con un ILB con un dispositivo WAF ##

Servicio de aplicaciones de Azure proporciona muchas medidas de seguridad que protegen el sistema Hola. También ayudan a toodetermine si se vulnerables en caso de una aplicación. mejor protección Hola para una aplicación web es una plataforma de hospedaje, como el servicio de aplicación de Azure, con un servidor de aplicaciones web (WAFS) toocouple. Como Hola ASE de ILB tiene un extremo de la aplicación de aislamiento de red, es adecuado para un uso de este tipo.

más información acerca de cómo tooconfigure su ASE ILB con un dispositivo WAFS, consulte toolearn [configurar un servidor de seguridad de la aplicación web con su entorno de servicio de aplicaciones][ASEWAF]. Este artículo se muestra cómo toouse un dispositivo virtual Barracuda con su ASE. Otra opción es toouse puerta de enlace de aplicaciones de Azure. Puerta de enlace de aplicaciones utiliza Hola OWASP core reglas toosecure todas las aplicaciones se colocan detrás de él. Para obtener más información acerca de la puerta de enlace de aplicaciones, consulte [firewall de aplicación web de Azure de introducción toohello][AppGW].

## <a name="get-started"></a>Primeros pasos ##

Todos los artículos y cómo tooinstructions para ASEs están disponibles en la [archivo Léame para los entornos del servicio de aplicación][ASEReadme].

* tooget partió ASEs, consulte [entornos del servicio de introducción tooApp][Intro].
* Para obtener más información acerca de la plataforma de servicio de aplicaciones de Azure de hello, consulte [servicio de aplicaciones de Azure](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

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
