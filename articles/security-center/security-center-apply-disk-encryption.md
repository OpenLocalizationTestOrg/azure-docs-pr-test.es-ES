---
title: cifrado del disco aaaApply en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** aplicar el cifrado de disco **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 6cc7824a-8d6b-4a5f-ab40-e3bbaebc4a91
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: cd803f1120018c5c86da91186eec1e59d425ede7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="apply-disk-encryption-in-azure-security-center"></a>Aplicación del cifrado de discos en el Centro de seguridad de Azure
Azure Security Center recomienda que aplique el cifrado de discos si tiene discos de máquina virtual de Windows o Linux que no estén cifrados con Azure Disk Encryption. El Cifrado de discos permite cifrar los discos de máquina virtual IaaS de Windows y Linux.  El cifrado se recomienda para hello SO y volúmenes de datos en la máquina virtual.

Cifrado de disco usa estándar del sector hello [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) característica de Windows y hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) característica de Linux. Estas características proporcionan SO y toohelp de cifrado de datos, proteger y proteger sus datos y satisfagan los compromisos de cumplimiento de normas y la seguridad de la organización. Cifrado del disco se integra con [el almacén de claves de Azure](https://azure.microsoft.com/documentation/services/key-vault/) toohelp controlar y administrar claves de cifrado de disco de Hola y secretos en su suscripción de almacén de claves, asegurándose de que todos los datos en discos de máquina virtual de Hola se cifran en reposo en su [ Almacenamiento de Azure](https://azure.microsoft.com/documentation/services/storage/).

> [!NOTE]
> Cifrado de disco Azure es compatible con hello después de sistemas de operativos Windows server - Windows Server 2008 R2, Windows Server 2012 y Windows Server 2012 R2. Se admite el cifrado de disco en hello después de sistemas operativos Linux - Ubuntu, CentOS, SUSE y SUSE Linux Enterprise Server (SLES).
>
>

## <a name="implement-hello-recommendation"></a>Implementar la recomendación de Hola
1. Hola **recomendaciones** hoja, seleccione **aplicar el cifrado de disco**.
2. Hola **aplicar el cifrado de disco** hoja, verá una lista de máquinas virtuales para el que se recomienda el cifrado del disco.
3. Siga toothese de cifrado de hello instrucciones tooapply máquinas virtuales.

![][1]

tooencrypt máquinas virtuales de Azure que se han identificado por el centro de seguridad como la necesidad de cifrado, se recomienda Hola pasos:

* Instale y configure Azure PowerShell. Esto le permite toorun Hola PowerShell comandos necesario tooset seguridad Hola requisitos previos necesarios tooencrypt máquinas virtuales de Azure.
* Obtener y ejecutar el script de PowerShell de Azure de requisitos previos de cifrado de disco de Azure de Hola.
* Cifre las máquinas virtuales.

[Encrypt an Azure Virtual Machine](security-center-disk-encryption.md) (Cifrado de una máquina virtual de Azure) le guiará a través de estos pasos.  En este tema se da por supuesto que usa Windows 10 como equipo de cliente de hello en el que configurar el cifrado del disco.

Existen varios enfoques que se pueden usar para Azure Virtual Machines. Si ya están muy versado en Azure PowerShell o CLI de Azure, quizás prefiera toouse los métodos alternativos. toolearn sobre estos otros enfoques, consulte [cifrado de disco de Azure](../security/azure-security-disk-encryption.md).

## <a name="see-also"></a>Otras referencias
Este documento se ha explicado cómo tooimplement Hola centro de seguridad recomendación "aplicar cifrado del disco." toolearn más información acerca del cifrado del disco, vea Hola recursos siguientes:

* [Cifrado y administración de claves con el almacén de claves de Azure](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (vídeo, 36 39 min.): Obtenga información acerca de cómo toouse disco de administración de cifrado para las máquinas virtuales IaaS y almacén de claves de Azure toohelp protección y protección sus datos.
* [Cifrar una máquina Virtual de Azure](security-center-disk-encryption.md) (documento): Obtenga información acerca de cómo tooencrypt máquinas virtuales de Azure.
* [Cifrado de disco de Azure](../security/azure-security-disk-encryption.md) (documento): Obtenga información acerca de cómo tooenable disco cifrado para Windows y máquinas virtuales de Linux.

toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad en el centro de seguridad de Azure](security-center-policies.md) : Obtenga información acerca de cómo las directivas de seguridad de tooconfigure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre publicaciones de blog sobre el cumplimiento y la seguridad de Azure.

<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png
