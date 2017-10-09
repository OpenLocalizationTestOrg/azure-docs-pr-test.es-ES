---
title: "aaaUsing SAP en máquinas virtuales de Windows | Documentos de Microsoft"
description: "Obtenga información sobre cómo usar SAP en máquinas virtuales (VM) de Windows en Microsoft Azure"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: 1b455be4-c02f-43e3-8d39-c2d5f216e646
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: 6c4d8a066a4a8805668e78e67fd2110f2000ee75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-windows-virtual-machines-in-azure"></a>Uso de SAP en máquinas virtuales Windows en Azure
Informática en la nube es un término ampliamente utilizado que está adquiriendo cada vez más importancia en hello sector de TI, desde las pequeñas empresas de las organizaciones toolarge y multinacional. Microsoft Azure es la plataforma de servicios de nube de Microsoft que ofrece una amplia gama de nuevas posibilidades de Hola. Ahora los clientes están toorapidly puede aprovisionar y eliminación aprovisionar aplicaciones como servicios en la nube, por lo que no son tootechnical limitado o restricciones presupuestarias. En lugar de invertir tiempo y presupuesto en infraestructura de hardware, las empresas pueden centrarse en la aplicación hello, procesos empresariales y sus ventajas para los clientes y los usuarios.

Con las máquinas virtuales de Microsoft Azure, Microsoft ofrece una completa plataforma de infraestructura como servicio (IaaS). Las aplicaciones de basadas en SAP NetWeaver son compatibles en las máquinas virtuales de Azure (IaaS). notas del producto Hola siguientes describen cómo tooplan e implementar SAP NetWeaver aplicaciones basadas en máquinas virtuales de Windows en Azure. También puede implementar aplicaciones basadas en SAP NetWeaver en [máquinas virtuales Linux](../../linux/classic/sap-get-started.md).

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure---ha"></a>SAP NetWeaver en Azure - Alta disponibilidad
título: aaaSAP NetWeaver en Azure: agrupación en clústeres SAP ASCS/SCS instancias con clúster de conmutación por error de Windows Server en Azure con SIOS DataKeeper

Resumen: ' este documento se describe cómo toouse SIOS DataKeeper tooset una configuración de SAP ASCS/SCS de alta disponibilidad en Azure. SAP protege su punto único de componentes de error como SAP ASCS/SCS o Enqueue Replication Services con las configuraciones de clúster de conmutación por error de Windows Server que requieren los discos compartidos. Estos componentes SAP son esenciales para la funcionalidad de Hola de un sistema SAP. Por lo tanto, necesidades de funcionalidad de alta disponibilidad toobe colocar en coloque toomake seguro de que dichos componentes pueden soportar un error de un servidor o una máquina virtual tal como hizo con las configuraciones de clúster de Windows para entornos de Hyper-V y de reconstrucción completa. A partir de agosto de 2015 Azure en sí mismo no puede proporcionar los discos compartidos que serían necesarios para Windows hello basadas en configuraciones de alta disponibilidad necesarias para estos componentes críticos de SAP. Sin embargo con ayuda de Hola de producto de hello DataKeeper de SIOS, se pueden crear configuraciones de clúster de conmutación por error de Windows Server según sea necesario para SAP ASCS/SCS en plataforma de IaaS de Azure Hola. Este documento describe un método paso a paso cómo tooinstall proporcionado de una configuración de clúster de conmutación por error de Windows Server con el disco compartido que SIOS DataKeeper proporciona en Azure. documento de Hola se explican los detalles de las configuraciones en lado de Azure, Windows y SAP de Hola que configuración de alta disponibilidad de hello funcione de manera óptima. Hola papel complementa Hola documentación de la instalación de SAP y las notas de SAP que representan recursos principales de Hola para las instalaciones e implementaciones de software SAP en correctos plataformas.

Actualizado: agosto de 2015

[Descargar esta guía ahora](http://go.microsoft.com/fwlink/?LinkId=613056)

