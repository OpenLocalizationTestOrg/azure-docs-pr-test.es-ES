---
title: "configuración de Azure Traffic Manager aaaVerify | Documentos de Microsoft"
description: "Este artículo lo ayudará a comprobar la configuración de Traffic Manager."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 2180b640-596e-4fb2-be59-23a38d606d12
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: c670be6cf55e140c7ab63d5d526de08e14774d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="verify-traffic-manager-settings"></a>Comprobación de la configuración de Traffic Manager

tootest la configuración de Traffic Manager, necesita toohave varios clientes, en varias ubicaciones, desde el que puede ejecutar las pruebas. A continuación, detener los extremos de hello en el perfil del Administrador de tráfico hacia abajo de uno en uno.

* Establecido el valor de TTL de DNS de hello bajo para que los cambios se propaguen rápidamente (por ejemplo, 30 segundos).
* Conozca Hola direcciones IP de los servicios de nube de Azure y sitios Web en el perfil de Hola que está probando.
* Usar herramientas que le permiten resolver una dirección IP de DNS nombre tooan y mostrar esa dirección.

Está protegiendo toosee que los nombres DNS de hello resolverán tooIP direcciones de extremos de hello en su perfil. deben resolver nombres Hola de manera coherente con los método de enrutamiento de tráfico de hello definido en el perfil de Traffic Manager de Hola. También puede usar herramientas de hello como **nslookup** o **profundizar** tooresolve los nombres de DNS.

Hello en los ejemplos siguientes le ayudarán a probar el perfil de Traffic Manager.

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a>Comprobación del perfil de Traffic Manager con nslookup e ipconfig en Windows

1. Abra un símbolo del sistema o de Windows PowerShell como administrador.
2. Tipo `ipconfig /flushdns` tooflush Hola caché de resolución DNS.
3. Escriba `nslookup <your Traffic Manager domain name>`. Por ejemplo, Hola siguiente comando Hola de comprobaciones de nombre de dominio con prefijo de hello *myapp.contoso*

        nslookup myapp.contoso.trafficmanager.net

    Un resultado típico muestra hello siguiente información:

    + Hello nombre DNS y dirección IP de hello DNS server que se va a obtener acceso a tooresolve este nombre de dominio de Traffic Manager.
    + nombre de dominio de Traffic Manager de Hola que se escribió en la línea de comandos de hello después de "nslookup" y resuelve el dominio de Traffic Manager de hello IP dirección toowhich Hola. dirección IP de la segunda Hello es una toocheck importante de Hola. Debe coincidir con una pública dirección IP virtual (VIP) para uno de los servicios de nube de Hola o sitios Web de hello perfil de Traffic Manager que está probando.

## <a name="how-tootest-hello-failover-traffic-routing-method"></a>La conmutación por error de tootest Hola tráfico método de enrutamiento

1. Deje todos los extremos activados.
2. Con un solo cliente, solicite la resolución DNS del nombre de dominio de la empresa con la utilidad nslookup u otra parecida.
3. Asegúrese de que Hola resuelve la dirección IP coincide con el extremo principal de Hola.
4. Desconecta el extremo principal o quite Hola supervisando el archivo de modo que considera Traffic Manager que Hola aplicación está inactivo.
5. Espere Hola DNS Time-to-Live (TTL) del perfil de Traffic Manager de hello además de otros dos minutos. Por ejemplo, si el TTL de DNS es de 300 segundos (5 minutos), debe esperar 7 minutos.
6. Vacíe la memoria caché del cliente DNS y solicite la resolución DNS mediante nslookup. En Windows, puede vaciar la caché DNS con el comando de hello ipconfig /flushdns.
7. Asegúrese de que Hola resuelve la dirección IP coincide con el punto de conexión secundaria.
8. Repita el proceso de hello, detenga cada punto de conexión a su vez. Compruebe que Hola DNS devuelve la dirección IP de Hola de punto de conexión siguiente de hello en lista de Hola. Cuando todos los extremos están inactivos, debe volver a obtener dirección IP de Hola de punto de conexión principal Hola.

## <a name="how-tootest-hello-weighted-traffic-routing-method"></a>Cómo tootest Hola ponderan método de enrutamiento de tráfico

1. Deje todos los extremos activados.
2. Con un solo cliente, solicite la resolución DNS del nombre de dominio de la empresa con la utilidad nslookup u otra parecida.
3. Asegúrese de que Hola resuelve la dirección IP coincide con uno de los extremos.
4. Vacíe la memoria caché del cliente DNS y repita los pasos 2 y 3 para cada punto de conexión. Debería ver diferentes direcciones IP devueltas para cada uno de los extremos.

## <a name="how-tootest-hello-performance-traffic-routing-method"></a>Cómo el rendimiento de hello tootest tráfico método de enrutamiento

tooeffectively probar un método de enrutamiento de tráfico de rendimiento, deberá tener clientes situados en diversas partes de Hola a todos. Puede crear a clientes en diferentes regiones de Azure que pueden ser utilizado tootest los servicios. Si tiene una red global, puede iniciar sesión en tooclients en otras partes de Hola a todos remotamente y ejecutar las pruebas desde allí.

Como alternativa, existen servicios gratuitos en la Web para indagación y búsqueda DNS. Algunas de estas herramientas ofrecen a Hola resolución de nombres DNS de capacidad toocheck desde diversas ubicaciones alrededor de Hola a todos. Busque con "búsqueda DNS" para obtener ejemplos. Servicios de terceros como Gomez o Keynote pueden ser usado tooconfirm que los perfiles están distribuyendo el tráfico según lo previsto.

## <a name="next-steps"></a>Pasos siguientes

* [Información acerca de los métodos de enrutamiento del tráfico del Administrador de tráfico](traffic-manager-routing-methods.md)
* [Consideraciones de rendimiento sobre el Administrador de tráfico](traffic-manager-performance-considerations.md)
* [Solución de problemas de estado degradado del Administrador de tráfico](traffic-manager-troubleshooting-degraded.md)
