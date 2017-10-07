---
title: Validar VPN rendimiento tooa red Virtual de Microsoft Azure | Documentos de Microsoft
description: "propósito de este documento Hello es toohelp un usuario validar el rendimiento de la red de Hola desde su tooan de recursos locales máquina virtual de Azure."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a>La red virtual de toovalidate VPN rendimiento tooa

Una conexión VPN de puerta de enlace le permite tooestablish la conectividad entre entornos seguros, entre la red Virtual dentro de Azure y sus instalaciones de infraestructura de TI.

Este artículo muestra cómo toovalidate rendimiento de la red de hello local recursos tooan máquina virtual de Azure. También proporciona orientación para la solución de errores.

>[!NOTE]
>Este artículo está destinado toohelp diagnosticar y corregir problemas comunes. Si le problema de hello toosolve no se puede mediante el uso de hello después de obtener información, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
>
>

## <a name="overview"></a>Información general

Hola conexión de puerta de enlace VPN implica Hola de los componentes siguientes:

- Dispositivo VPN local (vea una lista de [dispositivos VPN validados)](vpn-gateway-about-vpn-devices.md#devicetable).
- Internet público
- Azure VPN Gateway
- Máquina virtual de Azure

Hola siguiente diagrama muestra hello lógica a la conectividad de un tooan de red local red virtual de Azure a través de VPN.

![Lógica tooMSFT de conectividad de red de cliente de red con VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a>Calcular Hola máximo esperado entrada/salida

1.  Determine los requisitos de rendimiento de la línea de base de la aplicación.
2.  Establezca los límites de rendimiento de la puerta de enlace de VPN de Azure. Para obtener ayuda, consulte sección Hola "rendimiento agregado por tipo SKU y VPN" de [planificación y diseño para la puerta de enlace VPN](vpn-gateway-plan-design.md).
3.  Determinar hello [Guía de rendimiento de máquina virtual de Azure](../virtual-machines/virtual-machines-windows-sizes.md) para el tamaño de la máquina virtual.
4.  Establezca el ancho de banda del proveedor de servicios de Internet (ISP).
5.  Calcule el rendimiento esperado: menor ancho de banda de (VM, puerta de enlace e ISP) * 0,8.

Si el rendimiento calculado no cumple los requisitos de rendimiento de línea de base de la aplicación, necesita ancho de banda de tooincrease Hola de recursos de Hola que ha identificado como cuello de botella de Hola. tooresize una puerta de enlace de VPN de Azure, consulte [cambiar una SKU de puerta de enlace](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku). tooresize una máquina virtual, consulte [cambiar el tamaño de una máquina virtual](../virtual-machines/virtual-machines-windows-resize-vm.md). Si no tiene previsto ancho de banda de Internet, también puede toocontact su ISP.

## <a name="validate-network-throughput-by-using-performance-tools"></a>Validación del rendimiento de red mediante el uso de herramientas de rendimiento

Esta validación debe realizarse durante las horas de poca actividad, ya que la saturación de rendimiento del túnel VPN durante las pruebas provoca que no se produzcan resultados precisos.

herramienta de Hola que se usa para esta prueba es iPerf, que funciona en Windows y Linux y tiene los modos de cliente y servidor. Es limitado too3 GB/s para máquinas virtuales de Windows.

Esta herramienta no lleva a cabo cualquier toodisk de operaciones de lectura/escritura. Solamente se produce el tráfico TCP generado automáticamente desde un toohello de final otros. Generan estadísticas basadas en experimentación que mide Hola de ancho de banda disponible entre los nodos de cliente y servidor. Cuando se prueba entre dos nodos, uno actúa como servidor de Hola y Hola otro como un cliente. Una vez completada esta prueba, se recomienda que invertir Hola roles tootest ambos cargar y descargar el rendimiento en ambos nodos.

### <a name="download-iperf"></a>Descarga de iPerf
Descargue [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip). Para más información, vea la [documentación de Ambari](https://iperf.fr/iperf-doc.php).

 >[!NOTE]
 >productos de terceros de Hola que se explica en este artículo están fabricados por compañías independientes de Microsoft. Microsoft no otorga ninguna garantía, implícita o de otro tipo, sobre el rendimiento de Hola o la confiabilidad de estos productos.
 >
 >

### <a name="run-iperf-iperf3exe"></a>Ejecución de iPerf (iperf3.exe)
1. Habilitar una regla ACL de GSN/permitiendo el tráfico de hello (para la dirección IP pública pruebas en la máquina virtual de Azure).

2. En ambos nodos, habilite una excepción de firewall para el puerto 5001.

    **Windows:** siguiente Hola de ejecución de comandos como administrador:

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    regla de hello tooremove cuando se prueba está completa, ejecute este comando:

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    **Azure Linux**: las imágenes de Azure Linux tienen firewalls permisivos. Si hay una aplicación escuchando en un puerto, se permite el tráfico de Hola a través. Las imágenes personalizadas que se protegen pueden necesitar puertos abiertos de forma explícita. Los firewalls de nivel de sistema operativo Linux comunes incluyen `iptables`, `ufw`, o `firewalld`.

3. En el nodo del servidor hello, cambie el directorio de toohello donde se extrae iperf3.exe. A continuación, ejecutar iPerf en modo de servidor y ha configurado toolisten en el puerto 5001 como Hola siguientes comandos:

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. En el nodo de cliente hello, cambie el directorio de toohello donde se extrae y a continuación, ejecute el siguiente comando de hello iperf herramienta:

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    cliente de Hello es inducción de tráfico en el servidor de puertos 5001 toohello durante 30 segundos. Hola marca '-P ' que indica que estamos usando 32 nodos de servidor toohello de conexiones simultáneas.

    Hello pantalla siguiente muestra la salida de hello de este ejemplo:

    ![Salida](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. (Opcional) toopreserve Hola pruebas resultados, ejecute este comando:

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. Después de completar los pasos anteriores de hello, ejecutar Hola invierten mismos pasos con roles de hello, por lo que hello nodo servidor ahora será cliente hello y viceversa.

## <a name="address-slow-file-copy-issues"></a>Solución de problemas de copia de archivos lenta
Puede experimentar una copia de archivos lenta cuando use el Explorador de Windows o arrastre suelte en una sesión RDP. Este problema suele ser debido a tooone o ambos de hello siguientes factores:

- Las aplicaciones de copia de archivos, como el Explorador de Windows y RDP, no utilizan varios subprocesos al copiar archivos. Para mejorar el rendimiento, use una aplicación de copia de archivo multiproceso como [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy archivos mediante el uso de 16 o 32 subprocesos. número de subprocesos de hello toochange de copia de archivo en Richcopy, haga clic en **acción** > **copiar opciones** > **copiar el archivo**.<br><br>
![Problemas de copia de archivos lenta](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)<br>
- Velocidad de lectura/escritura del disco de VM insuficiente. Para más información, vea [Solución de problemas de Azure Storage](../storage/common/storage-e2e-troubleshooting.md).

## <a name="on-premises-device-external-facing-interface"></a>Interfaz con orientación externa del dispositivo local
Si el dispositivo VPN dirección IP a través de Internet se incluye en hello en local de hello [red local](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definición en Azure, es posible que experimente incapacidad toobring Hola se desconecta de la VPN, esporádico o problemas de rendimiento.

## <a name="checking-latency"></a>Comprobación de la latencia
Usar tracert tootrace tooMicrosoft Azure borde dispositivo toodetermine si hay retrasos superior a 100 ms. entre saltos.

Desde la red local de hello, ejecute *tracert* toohello VIP de hello puerta de enlace de Azure o la máquina virtual. Una vez que vea sólo * devuelve, sabrá que ha alcanzado hello borde de Azure. Cuando vea los nombres DNS que incluyan "MSN" devuelto, sabrá que ha alcanzado la red troncal de Microsoft de Hola.<br><br>
![Comprobación de la latencia](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información o ayuda, visite Hola siguientes vínculos:

- [Optimización del rendimiento de red en las máquinas virtuales de Azure](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [Ayuda y soporte técnico de Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
