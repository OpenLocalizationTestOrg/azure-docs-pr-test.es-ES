---
title: 'Azure Active Directory B2C: Disponibilidad en regiones y residencia de datos | Microsoft Docs'
description: Un tema en tipos de Hola de inquilinos de Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: d382921fe9d62183b6d52c47d62f952dabd116c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a>Azure Active Directory B2C: Disponibilidad en regiones y residencia de datos
Disponibilidad de la región y residencia de datos son dos conceptos muy diferentes que aplican tooAzure AD B2C de manera diferente del resto de Hola de Azure. En este artículo se explican las diferencias de hello entre estos dos conceptos y comparar cómo se aplica tooAzure frente a Azure AD B2C.

## <a name="summary"></a>Resumen
B2C de Azure AD es **suelen estar disponibles en todo el mundo** con la opción de Hola para **residencia de datos en Estados Unidos o en Europa**.

## <a name="concepts"></a>Conceptos
* **Disponibilidad de la región** hace referencia toowhere un servicio está disponible para su uso.
* **Residencia datos** hace referencia se almacenan los datos de usuario de toowhere.

## <a name="region-availability"></a>Disponibilidad en regiones
B2C de Azure AD está disponible en todo el mundo a través de hello nube pública de Azure. 

Esto difiere del modelo de hello mayoría de los demás seguimiento de los servicios de Azure que acoplar disponibilidad con residencia de datos. Puede ver ejemplos de esto en ambos Azure [productos disponibles por región](https://azure.microsoft.com/regions/services/) hello y página [Calculadora de precios B2C de Active Directory](https://azure.microsoft.com/pricing/details/active-directory-b2c/).

## <a name="data-residency"></a>Residencia de datos
Azure AD B2C almacena los datos de usuarios en Estados Unidos o Europa.

La residencia de datos se determina en función del país o región seleccionado al [crear un inquilino de Azure AD B2C](active-directory-b2c-get-started.md).

![Captura de pantalla de un inquilino de versión preliminar](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

Datos que se encuentran en Estados Unidos de Hola para hello después de países o regiones:

> Estados Unidos, Canadá, Costa Rica, República Dominicana, El Salvador, Guatemala, México, Panamá, Puerto Rico y Trinidad y Tobago

Los datos residen en Europa para hello después de países o regiones:

> Alemania, Arabia Saudí, Argelia, Austria, Azerbaiyán, Bahréin, Bélgica, Bielorrusia, Bulgaria, Croacia, Chipre, Dinamarca, Egipto, Emiratos Árabes Unidos Eslovaquia, Eslovenia, España, Estonia, Finlandia, Francia, Grecia, Hungría, Irlanda, Islandia, Israel, Italia, Jordania, Kazajistán, Kenia, Kuwait, Letonia, Líbano, Liechtenstein, Lituania, Luxemburgo, Macedonia, Malta, Marruecos, Montenegro, Nigeria, Noruega, Omán, Países Bajos, Pakistán, Polonia, Portugal, Qatar, Reino Unido, República Checa, Rumanía, Rusia, Serbia, Sudáfrica, Suecia, Suiza, Túnez, Turquía y Ucrania.

Hola restantes países o regiones están en curso de Hola de añadidos toohello lista.  Por ahora, todavía puede usar Azure AD B2C escogiendo Hola países o regiones anteriores.

> Afganistán, Argentina, Australia, Brasil, Chile, Colombia, Corea, Ecuador, Filipinas, India, Indonesia, Iraq, Japón, Malasia, Nueva Zelanda, Paraguay, Perú, RAE de Hong Kong, Singapur, Sri Lanka, Taiwán, Tailandia, Uruguay y Venezuela.

## <a name="preview-tenant"></a>Inquilino de versión preliminar
Si había creado un inquilino de B2C durante el período de versión preliminar de Azure AD B2C, es probable que en **Tipo de inquilino** aparezca **Inquilino de vista previa**. Si éste es el caso de hello, debe usar al inquilino solo para fines de pruebas y desarrollo y no para las aplicaciones de producción.

> [!IMPORTANT]
> No hay ninguna ruta de acceso de migración desde una versión preliminar del inquilino de B2C inquilino tooa producción escala B2C. Tenga en cuenta que existen problemas conocidos cuando se elimina un inquilino de vista previa B2C y volver a crear una escala de producción B2C inquilino tenga Hola el mismo nombre de dominio. Deberá toocreate un inquilino de B2C producción escala con un nombre de dominio diferente.


![Captura de pantalla de un inquilino de versión preliminar](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
