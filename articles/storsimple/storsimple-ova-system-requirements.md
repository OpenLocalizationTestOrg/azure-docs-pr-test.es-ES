---
title: requisitos de sistema de Azure StorSimple Virtual Array aaaMicrosoft | Documentos de Microsoft
description: "Obtenga información acerca de los requisitos de software y las redes de hello para la matriz Virtual de StorSimple"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: ea1d3bca-e71b-453d-aa82-440d2638f5e3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.openlocfilehash: 7a124873fdd806d409c7279851456e6347e7ec0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-system-requirements"></a>Requisitos del sistema de la matriz virtual de StorSimple
## <a name="overview"></a>Información general
Este artículo describen los requisitos de sistema importante de hello para la matriz Virtual de Microsoft Azure StorSimple y para los clientes de almacenamiento de hello obtiene acceso a matriz Hola. Se recomienda que revise cuidadosamente información Hola antes de implementar el sistema de StorSimple y, a continuación, hacen referencia tooit según sea necesario durante la implementación y las operaciones subsiguientes.

los requisitos de sistema de Hello incluyen:

* **Requisitos de software para los clientes de almacenamiento** -describe Hola admitida plataformas de virtualización, exploradores web, iniciadores iSCSI, los clientes SMB, los requisitos mínimos del dispositivo virtual y los requisitos adicionales para estos sistemas operativos.
* **Requisitos de red para el dispositivo StorSimple hello** -proporciona información acerca de los puertos de hello ese toobe necesidad abierto en el firewall tooallow para el tráfico de iSCSI, de nube o de administración.

requisitos del sistema StorSimple Hola información publicada en este artículo se aplica tooStorSimple arreglos de discos virtuales solo.

* Para dispositivos 8000 serie, vaya demasiado[requisitos del sistema para el dispositivo de la serie StorSimple 8000](storsimple-system-requirements.md).
* Para los dispositivos de la 7000 serie, vaya demasiado[requisitos del sistema para el dispositivo de la serie StorSimple 5000-7000](http://onlinehelp.storsimple.com/1_StorSimple_System_Requirements).

## <a name="software-requirements"></a>Requisitos de software
requisitos de software de Hello incluyen información de hello en los exploradores web compatibles de hello, versiones SMB, plataformas de virtualización y los requisitos mínimos del dispositivo virtual Hola.

### <a name="supported-virtualization-platforms"></a>Plataformas de virtualización admitidas
| **Hipervisor** | **Versión** |
| --- | --- |
| Hyper-V |Windows Server 2008 R2 SP1 y posterior |
| VMware ESXi |Versión 5.5 y versiones posteriores. |

### <a name="virtual-device-requirements"></a>Requisitos de los dispositivos virtuales
| **Componente** | **Requisito** |
| --- | --- |
| Número mínimo de procesadores virtuales (núcleos) |4 |
| Cantidad mínima de memoria (RAM) |8 GB <br> Para un servidor de archivos, 8 GB para menos de 2 millones de archivos y 16 GB para 2-4 millones de archivos|
| Espacio en disco<sup>1</sup> |Disco de sistema operativo: 80 GB  <br></br>Disco de datos: 500 GB too8 TB |
| Número mínimo de interfaces de red |1 |
| Ancho de banda mínimo de Internet<sup>2</sup> |5 Mbps |

<sup>1</sup> : con aprovisionamiento fino

<sup>2</sup> -requisitos de red pueden variar según la tasa de cambio de datos diario Hola. Por ejemplo, si un dispositivo necesita tooback 10 GB o más cambios durante un día, a continuación, hello copia de seguridad diaria a través de una conexión de Mbps 5 puede tardar horas too4.25 (si no se pudo comprimir ni desduplican datos hello).

### <a name="supported-web-browsers"></a>Exploradores web compatibles
| **Componente** | **Versión** | **Requisitos/notas adicionales** |
| --- | --- | --- |
| Microsoft Edge |La versión más reciente | |
| Internet Explorer |La versión más reciente |Probado con Internet Explorer 11 |
| Google Chrome |La versión más reciente |Probado con Chrome 46 |

### <a name="supported-storage-clients"></a>Clientes de almacenamiento compatibles
Hola según los requisitos de software es para los iniciadores iSCSI de Hola que tienen acceso a la matriz Virtual de StorSimple (configurado como un servidor de iSCSI).

| **Sistemas operativos compatibles** | **Versión requerida** | **Requisitos/notas adicionales** |
| --- | --- | --- |
| Windows Server |2008R2 SP1, 2012, 2012R2 |StorSimple puede crear volúmenes con aprovisionamiento fino y totalmente aprovisionados. No puede crear volúmenes aprovisionados parcialmente. Solo se admiten volúmenes de iSCSI de StorSimple para:  <ul><li>Volúmenes simples en discos básicos de Windows.</li><li>NTFS de Windows para dar formato a un volumen.</li> |

Hola según los requisitos de software es para hello los clientes SMB que tienen acceso a la matriz Virtual de StorSimple (configurado como un servidor de archivos).

| **Versión de SMB** |
| --- |
| SMB 2.x |
| SMB 3.0 |
| SMB 3.02 |

> [!IMPORTANT]
> No copie ni almacenar archivos protegidos por el servidor de archivos de sistema de archivos cifrados (EFS) de Windows toohello StorSimple Virtual Array; el resultado será una configuración no admitida. 
> 

### <a name="supported-storage-format"></a>Formato de almacenamiento compatible.
Se admite solo Hola almacenamiento de blobs de bloques de Azure. No se admiten los blobs en páginas. Más información sobre [blobs en bloques y blobs en páginas](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).

## <a name="networking-requirements"></a>Requisitos de red
Hello tabla siguiente enumeran los puertos de Hola que necesitan toobe abierto en su tooallow de firewall para iSCSI, SMB, en la nube o el tráfico de administración. En esta tabla, *en* o *entrada* hace referencia dirección toohello desde el que las solicitudes de cliente entrantes, tener acceso a su dispositivo. *Out* o *saliente* hace referencia en el que el dispositivo StorSimple envía datos externamente, más allá de la implementación de Hola de dirección de toohello: por ejemplo, saliente toohello de Internet.

| **Nº de puerto<sup>1</sup>** | **Dentro o fuera** | **Ámbito de puerto** | **Obligatorio** | **Notas** |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP) |Fuera |WAN |No |Puerto de salida se usa para las actualizaciones de tooretrieve de acceso a Internet. <br></br>proxy web de salida de Hello es configurable por el usuario. |
| TCP 443 (HTTPS) |Fuera |WAN |Sí |Puerto de salida se usa para tener acceso a datos en la nube de Hola. <br></br>proxy web de salida de Hello es configurable por el usuario. |
| UDP 53 (DNS) |Fuera |WAN |En algunos casos; consulte las notas. |Este puerto es necesario solo si está utilizando un servidor DNS basado en Internet. <br></br> Tenga en cuenta que si implementa un servidor de archivos, le recomendamos que use el servidor DNS local. |
| UDP 123 (NTP) |Fuera |WAN |En algunos casos; consulte las notas. |Este puerto solo es necesario si está utilizando un servidor DNS basado en Internet.<br></br> Tenga en cuenta que si implementa un servidor de archivos, le recomendamos que sincronice la hora con los controladores de dominio de Active Directory. |
| TCP 80 (HTTP) |En el |LAN |Sí |Esto es Hola puerto de entrada para la interfaz de usuario local en el dispositivo de StorSimple de hello para la administración local. <br></br> Tenga en cuenta que obtiene acceso a Hola interfaz de usuario local a través de HTTP le redirigirá automáticamente tooHTTPS. |
| TCP 443 (HTTPS) |En el |LAN |Sí |Esto es Hola puerto de entrada para la interfaz de usuario local en el dispositivo de StorSimple de hello para la administración local. |
| TCP 3260 (iSCSI) |En el |LAN |No |Este puerto es usado tooaccess datos a través de iSCSI. |

<sup>1</sup> ningún puerto de entrada necesario toobe abierto en Hola Internet pública.

> [!IMPORTANT]
> Asegúrese de que firewall de hello no modificar o descifrar todo el tráfico SSL entre el dispositivo de StorSimple de Hola y Azure.
> 
> 

### <a name="url-patterns-for-firewall-rules"></a>Patrones de URL para reglas de firewall
Los administradores de red a menudo pueden configurar firewall avanzada reglas basadas en Hola Hola de toofilter de patrones de dirección URL de entrada y de Hola el tráfico saliente. La matriz virtual y Hola servicio Administrador de dispositivos de StorSimple dependen de otras aplicaciones de Microsoft como Service Bus de Azure, Azure Active Directory Access Control, cuentas de almacenamiento y servidores de Microsoft Update. patrones de dirección URL de Hello asociadas a estas aplicaciones pueden ser tooconfigure usa reglas de firewall. Es importante toounderstand que pueden cambiar los patrones de dirección URL de hello asociadas a estas aplicaciones. Esto a su vez necesitarán toomonitor de administrador de red de Hola y actualizar las reglas de firewall para StorSimple como y cuando sea necesario. 

Se recomienda que establezca las reglas de firewall para el tráfico saliente, basándose en las direcciones IP fijas de StorSimple, de forma generosa en la mayoría de los casos. Sin embargo, puede utilizar información de hello debajo tooset avanzadas reglas de firewall que son entornos seguros toocreate necesarios.

> [!NOTE]
> 
> * siempre se debe establecer el dispositivo de Hello (origen) de direcciones IP interfaces de red para la nube de tooall Hola. 
> * destino de Hello direcciones IP deben establecerse demasiado[intervalos IP del centro de datos Azure](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653).
> 
> 

| Patrón de URL | Componente o funcionalidad |
| --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*` |Servicio de administrador de dispositivos de StorSimple<br>Access Control Service<br>Bus de servicio |
| `http://*.backup.windowsazure.com` |Registro de dispositivos |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Revocación de certificados |
| `https://*.core.windows.net/*`<br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Supervisión y cuentas de Almacenamiento de Azure |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Servidores de Microsoft Update<br> |
| `http://*.deploy.akamaitechnologies.com` |CDN de Akamai |
| `https://*.partners.extranet.microsoft.com/*` |Paquete de soporte |
| `http://*.data.microsoft.com ` |Servicio de telemetría en Windows, vea hello [actualización para la experiencia del usuario y telemetría de diagnóstico](https://support.microsoft.com/en-us/kb/3068708) |

## <a name="next-step"></a>Paso siguiente
* [Preparar Hola portal toodeploy la matriz Virtual de StorSimple](storsimple-virtual-array-deploy1-portal-prep.md)

