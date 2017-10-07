---
title: "aaaDeploy un equilibrador de carga a través de Internet con IPv6 - plantilla de Azure | Documentos de Microsoft"
description: "Cómo toodeploy IPv6 son compatibles con el equilibrador de carga de Azure y equilibrio de carga, las máquinas virtuales."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
keywords: "IPv6, Azure Load Balancer, pila doble, dirección ip pública, ipv6 nativo, móvil, iot"
ms.assetid: 2998e943-13fc-4ea9-a68c-875e53a08db3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2016
ms.author: kumud
ms.openlocfilehash: 68b9ba874a50161243577b64c4a6d9c76b39156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-internet-facing-load-balancer-solution-with-ipv6-using-a-template"></a>Implementación de una solución de equilibrador de carga orientado a Internet con IPv6 mediante el uso de una plantilla

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [CLI de Azure](load-balancer-ipv6-internet-cli.md)
> * [Plantilla](load-balancer-ipv6-internet-template.md)

Azure Load Balancer es un equilibrador de carga de nivel 4 (TCP y UDP) equilibrador de carga de Hello proporciona alta disponibilidad mediante la distribución de tráfico entrante entre instancias de servicio de estado de servicios en la nube o máquinas virtuales en un conjunto de equilibrador de carga. Azure Load Balancer también pueden presentar prestar servicios en varios puertos, varias direcciones IP o ambos.

## <a name="example-deployment-scenario"></a>Escenario de implementación de ejemplo

Hello siguiente diagrama ilustra Hola solución equilibrio de carga que se implementarán mediante la plantilla de ejemplo de Hola se describe en este artículo.

![Escenario del equilibrador de carga](./media/load-balancer-ipv6-internet-template/lb-ipv6-scenario.png)

En este escenario, creará hello Azure recursos siguientes:

* una interfaz de red virtual para cada máquina virtual con las direcciones IPv4 e IPv6 asignadas
* un equilibrador de carga orientado a Internet con una dirección IP pública IPv4 e IPv6
* dos equilibrio reglas toomap Hola VIP toohello privados extremos públicos de carga
* un conjunto de disponibilidad que contiene máquinas virtuales de hello dos
* dos máquinas virtuales (VM)

## <a name="deploying-hello-template-using-hello-azure-portal"></a>Implementación de plantilla hello mediante Hola portal de Azure

Este artículo hace referencia a una plantilla que se publica en hello [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/201-load-balancer-ipv6-create/) Galería. Puede descargar plantilla de Hola de galería de Hola o iniciar la implementación de hello en Azure directamente desde la Galería de Hola. En este artículo se da por supuesto que ha descargado el equipo local de hello plantilla tooyour.

1. Abra Hola portal de Azure e inicie sesión con una cuenta que tenga permisos toocreate máquinas virtuales y recursos de red dentro de una suscripción de Azure. Además, a menos que esté usando los recursos existentes, cuenta de hello necesita permiso toocreate un grupo de recursos y una cuenta de almacenamiento.
2. Haga clic en "+ nuevo" desde el menú de hello, después, escriba "plantilla" en el cuadro de búsqueda de Hola. Seleccione "Implementación de plantilla" en los resultados de búsqueda de Hola.

    ![lb-ipv6-portal-step2](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step2.png)

3. En Hola a todos los elementos hoja, haga clic en "Implementación de plantilla".

    ![lb-ipv6-portal-step3](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step3.png)

4. Haga clic en "Crear".

    ![lb-ipv6-portal-step4](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step4.png)

5. Haga clic en "Editar plantilla". Elimine el contenido existente de Hola y copiar y pegar en el contenido completo de Hola Hola del archivo de plantilla (tooinclude Hola inicio y finalización {}), a continuación, haga clic en "Guardar".

    > [!NOTE]
    > Si está utilizando Microsoft Internet Explorer, cuando se pega, aparece un cuadro de diálogo que le pide que Portapapeles de Windows en toohello tooallow acceso. Haga clic en "Permitir acceso".

    ![lb-ipv6-portal-step5](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step5.png)

6. Haga clic en "Editar parámetros". En la hoja de parámetros de hello, especificar valores de hello siguiendo las instrucciones de Hola Hola sección de parámetros de plantilla, a continuación, haga clic en "Guardar" tooclose Hola parámetros hoja. En la hoja de implementación personalizada de hello, seleccione su suscripción, un grupo de recursos existente o cree uno. Si va a crear un grupo de recursos, a continuación, seleccione una ubicación para el grupo de recursos de Hola. A continuación, haga clic en **condiciones legales**, a continuación, haga clic en **compra** para condiciones legales Hola. Azure comienza implementar recursos Hola. Toma todos los recursos de hello toodeploy de varios minutos.

    ![lb-ipv6-portal-step6](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step6.png)

    Para obtener más información acerca de estos parámetros, vea hello [variables y parámetros de plantilla](#template-parameters-and-variables) sección más adelante en este artículo.

7. recursos de Hola toosee creados por la plantilla de hello, haga clic en Examinar, desplácese hacia abajo de la lista de Hola hasta que vea "Grupos de recursos", a continuación, haga clic en él.

    ![lb-ipv6-portal-step7](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step7.png)

8. En la hoja de grupos de recursos de hello, haga clic en nombre de Hola Hola del grupo de recursos especificado en el paso 6. Ver una lista de todos los recursos de Hola que se implementaron. Si todo ha ido bien, debe poner "Correcto" en "Última implementación". De lo contrario, asegúrese de que la cuenta de hello que está usando tiene recursos necesarios de permisos toocreate Hola.

    ![lb-ipv6-portal-step8](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step8.png)

    > [!NOTE]
    > Si examina los grupos de recursos inmediatamente después de completar el paso 6, "Última implementación" muestra el estado de Hola de "Implementación" mientras se están implementando recursos Hola.

9. Haga clic en "myIPv6PublicIP" en la lista de Hola de recursos. Verá que tiene una dirección IPv6 en direcciones IP, y que su nombre DNS es valor de Hola que especificó para el parámetro de dnsNameforIPv6LbIP hello en el paso 6. Este recurso es Hola público IPv6 dirección y nombre de host que sea accesibles tooInternet-los clientes.

    ![lb-ipv6-portal-step9](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step9.png)

## <a name="validate-connectivity"></a>Validar conectividad

Cuando se implementa correctamente la plantilla de hello, pueda validar la conectividad siguiendo Hola siguientes tareas:

1. Inicie sesión toohello portal de Azure y conectar tooeach de hello VM creadas por la implementación de la plantilla de Hola. Si implementó una máquina virtual de Windows Server, ejecute ipconfig /all desde un símbolo del sistema. Verá que hello las máquinas virtuales tienen direcciones IPv4 e IPv6. Si ha implementado máquinas virtuales de Linux, deberá tooconfigure Hola sistema operativo Linux tooreceive dinámica las direcciones IPv6 con instrucciones de hello proporcionadas para la distribución de Linux.
2. Desde un cliente conectado a Internet de IPv6, iniciar una dirección de IPv6 pública de conexión toohello Hola de equilibrador de carga. tooconfirm que Hola equilibrador de carga es el equilibrio entre las máquinas virtuales de hello dos, se podía instalar un servidor web como Microsoft Internet Information Services (IIS) en cada una de las máquinas virtuales de Hola. página de web predeterminada de Hello en cada servidor podría contener texto hello "Server0" o "Server1" toouniquely identificarlo. A continuación, abra un explorador de Internet en un cliente conectado a la red Internet IPv6 y examinar toohello nombre de host especificado para el parámetro de dnsNameforIPv6LbIP Hola de IPv6 conectividad tooeach VM de hello carga equilibrador tooconfirm-to-end. Si solo ve hello web página de un solo servidor, deberá tooclear la memoria caché del explorador. Abra varias sesiones de exploración privadas. Debería obtener una respuesta de cada servidor.
3. Desde un cliente conectado a Internet IPv4, iniciar una dirección de IPv4 pública de conexión toohello Hola de equilibrador de carga. tooconfirm que Hola equilibrador de carga es el equilibrio de carga Hola dos máquinas virtuales, puede probar con IIS, tal como se detalla en el paso 2.
4. En cada máquina virtual, inicia una conexión saliente tooan IPv6 o un dispositivo de Internet IPv4 conectados. En ambos casos, IP de origen de hello visto por dispositivo de destino de hello es los dirección pública de IPv4 o IPv6 de Hola Hola de equilibrador de carga.

> [!NOTE]
> ICMP para IPv4 e IPv6 está bloqueado en hello red de Azure. Como resultado, las herramientas ICMP tales como ping siempre producen algún error. conectividad de tootest, utilice una alternativa TCP como TCPing u Hola cmdlet de PowerShell Test-NetConnection. Tenga en cuenta que se muestra en el diagrama de hello las direcciones IP Hola son ejemplos de valores que puede ver. Puesto que se asignan dinámicamente direcciones de hello IPv6, direcciones Hola que recibirá serán diferentes y pueden variar según la región. Además, es común para la dirección de IPv6 pública hello en hello toostart de equilibrador de carga con un prefijo diferente de Hola direcciones privadas de IPv6 en el grupo de back-end de Hola.

## <a name="template-parameters-and-variables"></a>Template parameters and variables

Una plantilla de Azure Resource Manager contiene varias variables y parámetros que se pueden personalizar tooyour necesidades. Las variables se usan para los valores fijos que no desea que un usuario toochange. Parámetros se usan para los valores que desea que un usuario tooprovide al implementar la plantilla de Hola. plantilla de ejemplo de Hola está configurado para el escenario de hello descrito en este artículo. Puede personalizar este tooneeds de su entorno.

ejemplo de Hola plantilla utilizada en este artículo incluye siguiente de hello variables y parámetros:

| Parámetro / Variable | Notas |
| --- | --- |
| adminUsername |Especificar nombre de Hola de cuenta de administrador de hello usa toosign en máquinas virtuales de toohello con. |
| adminPassword |Especificar la contraseña de hello para la cuenta de administrador de hello usa toosign en toohello las máquinas virtuales con. |
| dnsNameforIPv4LbIP |Especifique el nombre de host DNS de Hola que quiera tooassign como el nombre público de Hola Hola de equilibrador de carga. Este nombre resuelve dirección IPv4 pública del equilibrador de carga toohello. nombre de Hello debe estar en minúsculas y coincide con regex hello: ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$. |
| dnsNameforIPv6LbIP |Especifique el nombre de host DNS de Hola que quiera tooassign como el nombre público de Hola Hola de equilibrador de carga. Este nombre resuelve la dirección de IPv6 público del equilibrador de carga toohello. nombre de Hello debe estar en minúsculas y coincide con regex hello: ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$. Esto puede ser Hola mismo nombre como Hola dirección IPv4. Cuando un cliente envía una consulta DNS para este nombre de Azure devolverá Hola A y registros AAAA al nombre de Hola se comparte. |
| vmNamePrefix |Especifique el prefijo de nombre VM de Hola. plantilla de Hello anexa un número (0, 1, etc.) toohello nombre cuando hello se crean las máquinas virtuales. |
| nicNamePrefix |Especifique el prefijo de nombre de interfaz de red de Hola. plantilla de Hello anexa un número (0, 1, etc.) toohello nombre cuando se crean interfaces de red de Hola. |
| storageAccountName |Escriba Hola nombre de una cuenta de almacenamiento existente o especificar nombre de Hola de un uno toobe nuevo creado por la plantilla de Hola. |
| availabilitySetName |Escriba el nombre de la disponibilidad de hello establecer toobe utilizado con hello las máquinas virtuales |
| addressPrefix |prefijo de dirección de Hello usa el intervalo de direcciones de hello toodefine de hello red Virtual |
| subnetName |nombre de Hola de subred de hello en creado para hello red virtual |
| subnetPrefix |prefijo de dirección de Hello usa el intervalo de direcciones de hello toodefine de subred de Hola |
| vnetName |Especifique el nombre de Hola para hello usa hello las máquinas virtuales de red virtual. |
| ipv4PrivateIPAddressType |método de asignación de Hello destinadas Hola privada dirección IP (estática o dinámica) |
| ipv6PrivateIPAddressType |método de asignación de Hello destinadas Hola privada dirección IP (dinámico). IPv6 solo admite la asignación dinámica. |
| numberOfInstances |número de Hola de carga equilibrada instancias implementadas por plantilla de Hola |
| ipv4PublicIPAddressName |Especifique el nombre DNS de hello desea toouse toocommunicate con la dirección IPv4 pública de Hola Hola de equilibrador de carga. |
| ipv4PublicIPAddressType |método de asignación de Hello utilizado para hello dirección IP pública (estática o dinámica) |
| Ipv6PublicIPAddressName |Especifique el nombre DNS de hello desea toouse toocommunicate con la dirección de IPv6 público Hola Hola de equilibrador de carga. |
| ipv6PublicIPAddressType |método de asignación de Hello usada para la dirección IP pública de hello (dinámico). IPv6 solo admite la asignación dinámica. |
| lbName |Especifique el nombre de Hola Hola de equilibrador de carga. Este nombre se muestra en el portal de Hola o usa al hacer referencia a tooit con un comando CLI o PowerShell. |

las variables restantes de Hello en plantilla Hola contienen valores derivados que se asignan cuando Azure crea recursos Hola. No cambie esas variables.
