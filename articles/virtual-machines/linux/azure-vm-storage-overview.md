---
title: "aaaAzure máquinas virtuales de Linux y el almacenamiento de Azure | Documentos de Microsoft"
description: "Describe los servicios Estándar y Premium Storage de Azure y Managed Disks y Unmanaged Disks con máquinas virtuales con Linux."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: d364c69e-0bd1-4f80-9838-bbc0a95af48c
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 2/7/2017
ms.author: rasquill
ms.openlocfilehash: d34441698a4e59721847685099e5fb3aa378c597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-storage"></a>Almacenamiento de máquinas virtuales con Linux y Azure
Almacenamiento de Azure es la solución de almacenamiento de hello en la nube para aplicaciones modernas que se basan en las necesidades de escalabilidad toomeet Hola de sus clientes, la disponibilidad y la durabilidad.  En suma toomaking sea posible para escenarios nuevos del toosupport a los desarrolladores toobuild aplicaciones a gran escala, el almacenamiento de Azure también proporciona Hola almacenamiento base máquinas virtuales de Azure.

## <a name="managed-disks"></a>Managed Disks

Máquinas virtuales de Azure ahora están disponibles mediante [discos de Azure administrados](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), lo que permite toocreate las máquinas virtuales sin crear ni administrar cualquier [cuentas de almacenamiento de Azure](../../storage/common/storage-introduction.md) usted mismo. Debe especificar si desea Premium o almacenamiento estándar y el disco de hello tamaño deben ser y, Azure crea Hola discos de máquina virtual para usted. Las VM con Managed Disks tienen muchas características importantes, como:

- Compatibilidad con escalabilidad automática. Azure crea discos de Hola y administra hello toosupport de almacenamiento subyacente seguridad too10, 000 discos por suscripción.
- Mayor confiabilidad con conjuntos de disponibilidad. Azure garantiza que los discos de VM están aislados automáticamente entre sí dentro de los conjuntos de disponibilidad.
- Mayor control de acceso. Managed Disks expone varias operaciones controladas por [Control de acceso basado en rol (RBAC) de Azure](../../active-directory/role-based-access-control-what-is.md).

Los precios de Managed Disks son distintos de los precios de los discos no administrados. Para esa información, consulte [Pricing and Billing for Managed Disks](../windows/managed-disks-overview.md#pricing-and-billing) (Precios y facturación de Managed Disks).

Puede convertir máquinas virtuales existentes que usan discos de toouse administrado de discos no administrados con [convertir vm az](/cli/azure/vm#convert). Para obtener más información, consulte [cómo tooconvert una VM Linux de código no discos discos administrados de tooAzure](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). No se puede convertir un disco no administrado en un disco administrado si disco no administrado de hello está en una cuenta de almacenamiento, o en cualquier momento ha sido, cifrado con [cifrado de servicio de almacenamiento de Azure (SSE)](../../storage/common/storage-service-encryption.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Hola siguientes pasos le indican cómo tootooconvert no administrada de discos que están, o bien hubieran, en una cuenta de almacenamiento cifrada de detalle:

- Copie el disco duro virtual (VHD) de hello con [inicio de copia de blob de almacenamiento az](/cli/azure/storage/blob/copy#start) tooa cuenta de almacenamiento que nunca se ha habilitado para el cifrado de servicio de almacenamiento de Azure.
- Cree una VM que use discos administrados y especifique el archivo de VHD durante la creación con [az vm create](/cli/azure/vm#create).
- Adjuntar Hola copia VHD con [adjuntar el disco de vm az](/cli/azure/vm/disk#attach) tooa ejecutando la máquina virtual con discos administrados.


## <a name="azure-storage-standard-and-premium"></a>Azure Storage: Standard y Premium
Las VM de Azure, ya sea que usen Managed Disks o discos no administrados, se pueden crean en discos de almacenamiento estándar o en discos de Premium Storage. Cuando se usa la máquina virtual de hello portal toochoose debe activar o desactivar una lista desplegable en hello **Fundamentos** pantalla tooview discos estándar y premium. Cuando las unidades de tooSSD alternada, solo el almacenamiento premium se mostrará en máquinas virtuales habilitadas todos respaldada por SSD.  Cuando se muestran tooHDD alternada, máquinas virtuales de almacenamiento estándar habilitado respaldadas por unidades de unidades de disco junto con el almacenamiento premium respaldadas por SSD de las máquinas virtuales.

Al crear una máquina virtual de hello `azure-cli` puede elegir entre standard y premium al elegir el tamaño de la máquina virtual de Hola a través de hello `-z` o `--vm-size` marca de cli.

## <a name="creating-a-vm-with-a-managed-disk"></a>Creación de una VM con un disco administrado

el ejemplo siguiente se Hello requiere Hola 2.0 de CLI de Azure, que puede [instalar aquí](/cli/azure/install-azure-cli).

En primer lugar, cree un hello toomanage de grupo de recursos recursos con [crear grupo az](/cli/azure/group#create):

```azurecli
az group create --location westus --name myResourceGroup
```

Ahora cree Hola VM con [crear vm az](/cli/azure/vm#create). Especifique un `--public-ip-address-dns-name`argumento único, ya que `mypublicdns` es probable que ya esté tomado.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns
```

ejemplo de Hola anterior crea una máquina virtual con un disco administrado en una cuenta de almacenamiento estándar. toouse una cuenta de almacenamiento Premium, agregar hello `--storage-sku Premium_LRS` argumento, como el siguiente ejemplo de Hola:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns \
    --storage-sku Premium_LRS
```

## <a name="standard-storage"></a>Standard storage
El almacenamiento de Azure estándar es tipo de almacenamiento predeterminado de Hola.  Standard Storage es un sistema rentable que sigue teniendo un buen rendimiento.  

## <a name="premium-storage"></a>Premium Storage
El Almacenamiento premium de Azure le ofrece soporte de disco de alto rendimiento y latencia baja para máquinas virtuales con cargas de trabajo intensivas de E/S. Discos de máquinas virtuales que usan datos de almacén de Almacenamiento premium en unidades de estado sólido (SSD). Puede migrar tooAzure de discos de máquina virtual de su aplicación ventaja de tootake de almacenamiento Premium de velocidad de Hola y el rendimiento de estos discos.

Características de Premium Storage:

* Los discos de almacenamiento Premium: Almacenamiento Premium de Azure es compatible con discos de máquina virtual que pueden ser tooDS adjunto, DSv2 o máquinas virtuales de la serie GS Azure.
* Blob en páginas Premium: Almacenamiento Premium es compatible con Blobs de página de Azure, que son discos persistentes toohold usado para máquinas virtuales de Azure (VM).
* Almacenamiento con redundancia local Premium: Una cuenta de almacenamiento Premium solo admite localmente redundante almacenamiento (LRS) como opción de replicación de Hola y mantiene tres copias de datos de hello en una única región.
* [Premium Storage](../../storage/common/storage-premium-storage.md)

## <a name="premium-storage-supported-vms"></a>Máquinas virtuales compatibles con Premium Storage
Premium Storage es compatible con las máquinas virtuales de Azure de las series DS, DSv2, GS y Fs. Puede usar discos de Standard Storage y Premium Storage con las máquinas virtuales compatibles con Premium Storage. Sin embargo, no puede utilizar discos de Premium Storage con series de máquinas virtuales que no son compatibles con este tipo de almacenamiento.

Los siguientes son hello las distribuciones de Linux que se valida con el almacenamiento Premium.

| Distribución | Versión | Kernel compatible |
| --- | --- | --- |
| Ubuntu |12.04 |3.2.0-75.110+ |
| Ubuntu |14.04 |3.13.0-44.73+ |
| Debian |7.x, 8.x |3.16.7-ckt4-1+ |
| SLES |SLES 12 |3.12.36-38.1+ |
| SLES |SLES 11 SP4 |3.0.101-0.63.1+ |
| CoreOS |584.0.0+ |3.18.4+ |
| CentOS |6.5, 6.6, 6.7, 7.0, 7.1 |3.10.0-229.1.2.el7+ |
| RHEL |6.8+, 7.2+ | |

## <a name="azure-file-storage"></a>Almacenamiento de archivos de Azure
Almacenamiento de archivos de Azure ofrece recursos compartidos de archivos en la nube de hello mediante el protocolo SMB estándar de Hola. Archivos de Azure, puede migrar las aplicaciones empresariales que se basan en tooAzure de servidores de archivos. Las aplicaciones que se ejecutan en Azure pueden montar fácilmente recursos compartidos de archivos de máquinas virtuales de Azure que ejecutan Linux. Y con la versión más reciente de Hola de almacenamiento de archivos, se puede montar un recurso compartido de archivos desde una aplicación local que es compatible con SMB 3.0.  Dado que los recursos compartidos de archivos son recursos compartidos de SMB, puede tener acceso a ellos a través de las API del sistema de archivos estándar.

Almacenamiento de archivos se basa en hello misma tecnología que el almacenamiento de Blob, tabla y cola, por lo que el almacenamiento de archivos ofrece disponibilidad hello, durabilidad, escalabilidad y la redundancia geográfica que está integrada en la plataforma de almacenamiento de Azure Hola. Para más información sobre los límites y objetivos de rendimiento de Azure Storage, vea Objetivos de escalabilidad y rendimiento del almacenamiento de Azure.

* [¿Cómo toouse almacenamiento de archivos de Azure con Linux](../../storage/files/storage-how-to-use-files-linux.md)

## <a name="hot-storage"></a>Almacenamiento de acceso frecuente
capa de almacenamiento de acceso rápido de Azure de Hello está optimizado para almacenar datos que se accede con frecuencia.  Almacenamiento activa es el tipo de almacenamiento predeterminado de Hola para almacenes de blobs.

## <a name="cool-storage"></a>Almacenamiento de acceso esporádico
capa de almacenamiento de acceso esporádico de Azure de Hello está optimizado para almacenar datos con poca frecuencia acceso y larga duración. Entre los casos de uso de este tipo de almacenamiento se encuentran las copias de seguridad, el contenido multimedia, los datos científicos, la información de cumplimiento y los datos de archivo. En general, cualquier dato al que rara vez se obtiene acceso es un candidato perfecto para el almacenamiento de acceso esporádico.

|  | capa de almacenamiento de acceso frecuente | capa de almacenamiento de acceso esporádico |
|:--- |:---:|:---:|
| Disponibilidad |99,9 % |99% |
| Disponibilidad (lecturas de RA-GRS) |99,99% |99,9 % |
| Cargos de uso |Mayores costos de almacenamiento |Menores costos de almacenamiento |
| Menor acceso |Mayor acceso | |
| y costos de transacción |y costos de transacción | |

## <a name="redundancy"></a>Redundancia
datos de Hello en su cuenta de almacenamiento siempre es de Microsoft Azure replican tooensure durabilidad y alta disponibilidad, cumpliendo Hola SLA de almacenamiento de Azure incluso de cara de Hola de errores de hardware transitorios.

Cuando se crea una cuenta de almacenamiento, debe seleccionar una de las siguientes opciones de replicación de hello:

* Almacenamiento con redundancia local (LRS)
* Almacenamiento con redundancia de zona (ZRS)
* Almacenamiento con redundancia geográfica (GRS)
* Almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS).

### <a name="locally-redundant-storage"></a>Almacenamiento con redundancia local
Almacenamiento con redundancia local (LRS) replica los datos dentro de la región de hello en el que creó la cuenta de almacenamiento. toomaximize durabilidad, cada solicitud realizada en los datos de la cuenta de almacenamiento se replica tres veces. Cada una de estas tres réplicas reside en dominios de error y dominios de actualización independientes.  Una solicitud se devuelve correctamente únicamente cuando ha sido escrito tooall tres réplicas.

### <a name="zone-redundant-storage"></a>Almacenamiento con redundancia de zona
Almacenamiento con redundancia de zona (ZRS) replica los datos entre dos toothree instalaciones, dentro de una única región o entre dos regiones, lo que proporciona mayor durabilidad que el LRS. Si la cuenta de almacenamiento tiene ZRS habilitado, los datos sean duraderos incluso en caso de hello de error en una de las instalaciones de Hola de.

### <a name="geo-redundant-storage"></a>Almacenamiento con redundancia geográfica
Almacenamiento con redundancia geográfica (GRS) replica la región secundaria de tooa de datos que se encuentra a cientos de millas fuera de la región principal de Hola. Si la cuenta de almacenamiento tiene GRS habilitado, los datos sean duraderos incluso en caso de hello de una interrupción regional completa o un desastre en qué Hola región principal no es recuperable.

### <a name="read-access-geo-redundant-storage"></a>Almacenamiento con redundancia geográfica con acceso de lectura
Almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS) maximiza la disponibilidad de la cuenta de almacenamiento, proporcionando datos de toohello de acceso de solo lectura en la ubicación secundaria de hello, además toohello replicación entre dos regiones proporcionada por GRS. En el caso de hello que los datos no están disponibles en la región principal de hello, la aplicación puede leer datos de la región secundaria Hola.

Para profundizar en la redundancia de Azure Storage, vea:

* [Replicación de almacenamiento de Azure](../../storage/common/storage-redundancy.md)

## <a name="scalability"></a>Escalabilidad
Almacenamiento de Azure es escalable de forma masiva, por lo que puede almacenar y procesar cientos de terabytes de escenarios de grandes cantidades de datos de datos toosupport Hola requeridos por los análisis financieros, científicos y aplicaciones multimedia. O bien, puede almacenar pequeñas cantidades de datos necesarios para un sitio Web de pequeñas empresas de Hola. Siempre que se encuentran en sus necesidades, solo paga por los datos de hello que almacena. Actualmente, Azure Storage alberga decenas de billones de objetos de cliente únicos y administra, por término medio, millones de solicitudes por segundo.

En el caso de cuentas de almacenamiento estándar: una cuenta de almacenamiento estándar tiene una tasa total máxima de solicitudes de 20 000 E/S por segundo. Hello IOPS totales en todos los discos de máquina virtual en una cuenta de almacenamiento estándar no debe superar este límite.

En el caso de cuentas de Premium Storage: una cuenta de Premium Storage tiene una capacidad total máxima de proceso de 50 Gbps. capacidad total de Hello en todos los discos de máquina virtual no debe superar este límite.

## <a name="availability"></a>Disponibilidad
Garantizamos que al menos 99,99% (99,9% de nivel de acceso inactivo) de tiempo de hello, se guardará correctamente los datos de tooread de solicitudes de proceso desde cuentas de almacenamiento con redundancia geográfica de acceso de lectura (RA-GRS), siempre que no se pudo intentos tooread datos de la región principal de Hola vuelve a intentar en la región secundaria Hola.

Garantizamos que al menos un 99,9% (99% de nivel de acceso inactivo) de tiempo de hello, haremos correctamente procesen solicitudes tooread datos desde almacenamiento redundante local (LRS), almacenamiento de redundancia de zona (ZRS) y las cuentas de almacenamiento con redundancia geográfica (GRS).

Garantizamos que al menos un 99,9% (99% de nivel de acceso inactivo) de tiempo de hello, haremos correctamente procesen solicitudes toowrite datos tooLocally almacenamiento redundante (LRS), zona redundantes almacenamiento (ZRS) y las cuentas de almacenamiento (GRS) redundancia geográfica y redundancia geográfica de acceso de lectura Cuentas de almacenamiento (RA-GRS).

* [Acuerdo de Nivel de Servicio para Azure Storage](https://azure.microsoft.com/support/legal/sla/storage/v1_1/)

## <a name="regions"></a>Regiones
Azure está disponible con carácter general en 30 regiones alrededor de Hola a todos y ha anunciado planes para 4 otras regiones. Expansión geográfica es una prioridad para Azure porque permite que nuestros clientes tooachieve un rendimiento mayor y compatible con sus requisitos y las preferencias con respecto a la ubicación de los datos.  Azures toolaunch de región más reciente se encuentra en Alemania.

Hola Alemania Microsoft Cloud proporciona una opción diferenciados toohello servicios de Microsoft Cloud ya disponibles en Europa, crear más oportunidades de innovación y el crecimiento económico para altamente reguladas asociados y clientes en Alemania, Hola hello Asociación Europea de libre comercio (AELC) y la Unión Europea (EU).

Administran datos de clientes en los centros de datos nuevo, en Magdeburg y Fráncfort, bajo el control de Hola de un usuario de confianza de datos, T-Systems internacional, una compañía de alemán independiente y subsidiaria de Deutsche Telekom. Servicios de comerciales en la nube de Microsoft en los centros de datos cumplen datos tooGerman control normativas y ofrecen opciones adicionales de cómo y dónde se procesan los datos a los clientes.

* [Mapa de las regiones de Azure](https://azure.microsoft.com/regions/)

## <a name="security"></a>Seguridad
Almacenamiento de Azure proporciona un conjunto completo de capacidades de seguridad que juntos permiten a los desarrolladores de aplicaciones seguras toobuild. propia cuenta de almacenamiento Hola se puede proteger mediante el Control de acceso basado en roles y Azure Active Directory. Los datos se pueden proteger en tránsito entre una aplicación y Azure usando cifrado de cliente, HTTPS o SMB 3.0. Se pueden establecer datos toobe cifrada automáticamente cuando escribe tooAzure almacenamiento mediante cifrado de servicio de almacenamiento (SSE). Discos de sistema operativo y los datos utilizados por máquinas virtuales se pueden establecer toobe cifrada mediante el cifrado de disco de Azure. Se pueden conceder acceso delegado toohello objetos de datos en el almacenamiento de Azure mediante firmas de acceso compartido.

### <a name="management-plane-security"></a>Seguridad en el plano de la administración
plano de administración de Hello consta de hello toomanage de recursos que usa la cuenta de almacenamiento. En esta sección, hablaremos sobre el modelo de implementación de Azure Resource Manager hello y cómo toouse toocontrol de Control de acceso basado en roles (RBAC) tener acceso a las cuentas de almacenamiento de tooyour. También hablaremos acerca de cómo administrar las claves de cuenta de almacenamiento y cómo tooregenerate ellos.

### <a name="data-plane-security"></a>Seguridad en el plano de los datos
En esta sección, trataremos permitir acceso toohello objetos de datos reales en la cuenta de almacenamiento como blobs, archivos, las colas y tablas, con firmas de acceso compartido y almacena las directivas de acceso. Nos fijaremos en las Firmas de acceso compartido tanto a nivel de servicio como a nivel de cuenta. También veremos cómo toolimit tener acceso a dirección IP específica de tooa (o intervalo de direcciones IP), cómo usar el protocolo de Hola de toolimit tooHTTPS y cómo toorevoke una firma de acceso compartido sin esperar a tooexpire.

## <a name="encryption-in-transit"></a>Cifrado en tránsito
Esta sección se describe cómo toosecure datos al transferirlos entre o salga de almacenamiento de Azure. Hablaremos acerca de hello recomendada el uso del cifrado de hello y HTTPS usado SMB 3.0 para recursos compartidos de archivos de Azure. También echaremos un vistazo a cifrado en el cliente, lo que permite tooencrypt Hola datos antes de transferirlos al almacenamiento en una aplicación cliente y toodecrypt Hola después de que se transfiere fuera de almacenamiento.

## <a name="encryption-at-rest"></a>Cifrado en reposo
Hablaremos sobre el cifrado de servicio de almacenamiento (SSE) y cómo puede habilitar para una cuenta de almacenamiento, lo que los blobs en bloques, blobs de página y anexar blobs que se cifran automáticamente cuando escribe tooAzure almacenamiento. También veremos cómo puede usar el cifrado de disco de Azure y explorar diferencias básicas de Hola y casos de cifrado del disco frente a SSE frente a cifrado en el cliente. Asimismo, estudiaremos brevemente el cumplimiento de la norma FIPS para equipos del Gobierno de EE. UU.

* [Guía de seguridad de Azure Storage](../../storage/common/storage-security-guide.md)

## <a name="temporary-disk"></a>Disco temporal
Cada máquina contiene un disco temporal. disco temporal de Hello proporciona almacenamiento a corto plazo para aplicaciones y procesos y datos de almacén de tooonly previsto como página o archivos de intercambio. Datos en disco temporal de hello podrían perderse durante un [evento de mantenimiento](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) o cuando se [volver a implementar una máquina virtual](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Durante un reinicio estándar de hello VM, deben conservar datos hello en la unidad temporal de Hola.

En máquinas virtuales Linux, disco de hello suele **/dev/sdb** y formatea y monta demasiado**/mnt** por hello agente Linux de Azure. tamaño de Hello del disco temporal de hello varía según tamaño Hola de máquina virtual de Hola. Para más información, consulte [Tamaños de las máquinas virtuales Linux en Azure](sizes.md).

Para obtener más información sobre cómo Azure utiliza disco temporal de hello, consulte [descripción de la unidad temporal de hello en máquinas virtuales de Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="cost-savings"></a>Ahorros en costos
* [Costo del almacenamiento](https://azure.microsoft.com/pricing/details/storage/)
* [Calculadora de costo de almacenamiento](https://azure.microsoft.com/pricing/calculator/?service=storage)

## <a name="storage-limits"></a>Límites de almacenamiento
* [Límites del servicio Storage](../../azure-subscription-service-limits.md#storage-limits)
