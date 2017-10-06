---
title: "requisitos previos de aaaTechnical para crear una imagen de máquina virtual para hello Azure Marketplace | Documentos de Microsoft"
description: "Comprender los requisitos de Hola para crear e implementar un toohello de imagen de máquina virtual Azure Marketplace para que otros lo toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: fcae4d9e052581e3c1dfe7962e6d50ec31040419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-hello-azure-marketplace"></a>Requisitos previos técnicos para crear una imagen de máquina virtual para hello Azure Marketplace
Leer proceso Hola exhaustivamente antes de comenzar y comprender dónde y por qué se realiza cada paso. Tanto como sea posible, debe preparar la información de su empresa y otros datos, descargue las herramientas necesarias, o quiere crear componentes técnicos antes de comenzar el proceso de creación de hello oferta. Estos elementos deben estar claros tras la revisión de este artículo.  

## <a name="download-needed-tools--applications"></a>Descargar herramientas y aplicaciones necesarias
Debe tener Hola siguientes elementos listos antes de comenzar el proceso de hello:

* Dependiendo del sistema operativo de destino, instale hello [cmdlets de PowerShell de Azure](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) o [herramienta de interfaz de línea de comandos de Linux](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) de hello [descargas de Azure](https://azure.microsoft.com/downloads/) página.
* Instale el Explorador de almacenamiento de Azure desde CodePlex.
* Descargue e instale Hola herramienta Certification Test de Azure Certified:
  * [http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913). Necesita una herramienta de certificados de equipo basado en Windows toorun Hola. Si no tiene un equipo basado en Windows disponible, puede ejecutar la herramienta de hello en una máquina virtual basada en Windows Azure.

## <a name="platforms-supported"></a>Plataformas compatibles
Puede desarrollar VM basadas en Azure en Windows o Linux. Algunos elementos del programa Hola proceso, como la creación de un compatible con Azure disco duro virtual (VHD)--Utilice distintas herramientas y pasos dependiendo del sistema operativo que esté usando de publicación:  

* Si usas Linux, consulte toohello "Crear un disco duro virtual de Azure compatible (basado en Linux)" sección de hello [Guía de publicación de imagen de máquina Virtual](marketplace-publishing-vm-image-creation.md).
* Si usas Windows, consulte la sección de "Crear un disco duro virtual de Azure compatible (basado en Windows)" de toohello de hello [Guía de publicación de imagen de máquina Virtual](marketplace-publishing-vm-image-creation.md).

> [!NOTE]
> Necesita tener acceso a tooa máquina de Windows para:
> 
> * Ejecute la herramienta de validación de certificados de Hola.
> * Crear URL de firma de acceso de disco duro virtual compartido de Hola para hello envío de certificación de disco duro virtual.
> 
> 

## <a name="develop-your-vhd"></a>Desarrollar el disco duro virtual
Puede desarrollar discos duros virtuales de Azure en la nube de Hola o de forma local:

* El desarrollo basado en la nube significa que todos los pasos de desarrollo se realizan de forma remota en un disco duro virtual residente en Azure.
* Para el desarrollo local se requiere la descarga de un disco duro virtual y su desarrollo mediante infraestructura local. Aunque esto es posible, no lo recomendamos. Tenga en cuenta que desarrollar para Windows o SQL local requiere toohave Hola local relevante claves de licencia. No puede incluir ni instalar SQL Server tras crear una máquina virtual. También deberá basar su oferta en una imagen SQL aprobada de hello portal de Azure. Si decide toodevelop local, debe realizar algunos pasos de manera diferente que si estuviese desarrollando en la nube de Hola. Encontrará información pertinente en [Creación de una imagen de máquina virtual local](marketplace-publishing-vm-image-creation-on-premise.md).

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
