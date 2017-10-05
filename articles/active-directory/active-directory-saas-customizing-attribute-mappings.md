---
title: "Personalización de asignaciones de atributos de Azure AD | Microsoft Docs"
description: "Conozca cuáles son las asignaciones de atributos para aplicaciones SaaS en Azure Active Directory y cómo puede modificarlas para satisfacer sus necesidades empresariales."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6ca2fdc9c68ea0030d938eeaebd57aafa0e2790f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="73c00-103">Personalización de asignaciones de atributos de aprovisionamiento de usuarios para aplicaciones SaaS en Azure Active Directory de usuarios</span><span class="sxs-lookup"><span data-stu-id="73c00-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="73c00-104">Microsoft Azure AD proporciona soporte para el aprovisionamiento de usuarios para aplicaciones SaaS de terceros como Salesforce, Google Apps y otras.</span><span class="sxs-lookup"><span data-stu-id="73c00-104">Microsoft Azure AD provides support for user provisioning to third-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="73c00-105">Si dispone de aprovisionamiento de usuarios para una aplicación SaaS de terceros habilitada, el Portal de administración de Azure controla sus valores de atributo en forma de una configuración denominada "asignación de atributos".</span><span class="sxs-lookup"><span data-stu-id="73c00-105">If you have user provisioning for a third-party SaaS application enabled, the Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="73c00-106">Hay un conjunto preconfigurado de asignaciones de atributos entre los objetos de usuario de Azure AD y los objetos de usuario de cada aplicación SaaS.</span><span class="sxs-lookup"><span data-stu-id="73c00-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="73c00-107">Algunas aplicaciones administran otros tipos de objetos, como grupos o contactos.</span><span class="sxs-lookup"><span data-stu-id="73c00-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="73c00-108">Puede personalizar las asignaciones de atributos predeterminadas según sus necesidades empresariales.</span><span class="sxs-lookup"><span data-stu-id="73c00-108">You can customize the default attribute mappings according to your business needs.</span></span> <span data-ttu-id="73c00-109">Esto significa que puede cambiar o eliminar asignaciones de atributos existentes o crear nuevas asignaciones de atributos.</span><span class="sxs-lookup"><span data-stu-id="73c00-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="73c00-110">En el portal de Azure AD, se puede acceder a esta característica haciendo clic en una configuración de **Asignaciones** en **Aprovisionamiento** en la sección **Administrar** de una **aplicación empresarial**.</span><span class="sxs-lookup"><span data-stu-id="73c00-110">In the Azure AD portal, you can access this feature by clicking a **Mappings** configuration under **Provisioning** in the **Manage** section of an **Enterprise application**.</span></span>


![Salesforce][5] 

<span data-ttu-id="73c00-112">Al hacer clic en una configuración de **Asignaciones**, se abre la hoja **Asignación de atributos**.</span><span class="sxs-lookup"><span data-stu-id="73c00-112">Clicking a **Mappings** configuration, opens the related **Attribute Mapping** blade.</span></span>  
<span data-ttu-id="73c00-113">Hay asignaciones de atributos que una aplicación SaaS necesita para funcionar correctamente.</span><span class="sxs-lookup"><span data-stu-id="73c00-113">There are attribute mappings that are required by a SaaS application to function correctly.</span></span> <span data-ttu-id="73c00-114">Para los atributos necesarios, la característica **Eliminar** no está disponible.</span><span class="sxs-lookup"><span data-stu-id="73c00-114">For required attributes, the **Delete** feature is unavailable.</span></span>


![Salesforce][6]  

<span data-ttu-id="73c00-116">En el ejemplo anterior, puede ver que el atributo **Username** de un objeto administrado en Salesforce se rellena con el valor de **userPrincipalName** del objeto vinculado de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="73c00-116">In the example above, you can see that the **Username** attribute of a managed object in Salesforce is populated with the **userPrincipalName** value of the linked Azure Active Directory Object.</span></span>

<span data-ttu-id="73c00-117">Puede personalizar las **asignaciones de atributos** existentes haciendo clic en una asignación.</span><span class="sxs-lookup"><span data-stu-id="73c00-117">You can customize existing **Attribute Mappings** by clicking a mapping.</span></span> <span data-ttu-id="73c00-118">Se abre la hoja **Editar atributo**.</span><span class="sxs-lookup"><span data-stu-id="73c00-118">This opens the **Edit Attribute** blade.</span></span>

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="73c00-120">Información sobre los tipos de asignación de atributos</span><span class="sxs-lookup"><span data-stu-id="73c00-120">Understanding attribute mapping types</span></span>
<span data-ttu-id="73c00-121">Con asignaciones de atributos, puede controlar cómo se rellenan los atributos en una aplicación SaaS de terceros.</span><span class="sxs-lookup"><span data-stu-id="73c00-121">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="73c00-122">Se admiten cuatro tipos de asignaciones diferentes:</span><span class="sxs-lookup"><span data-stu-id="73c00-122">There are four different mapping types supported:</span></span>

* <span data-ttu-id="73c00-123">**Directa** : el atributo de destino se rellena con el valor de un atributo del objeto vinculado en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73c00-123">**Direct** – the target attribute is populated with the value of an attribute of the linked object in Azure AD.</span></span>
* <span data-ttu-id="73c00-124">**Constante** : el atributo de destino se rellena con una cadena específica que se ha especificado.</span><span class="sxs-lookup"><span data-stu-id="73c00-124">**Constant** – the target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="73c00-125">**Expresión** : el atributo de destino se rellena según el resultado de una expresión similar a un script.</span><span class="sxs-lookup"><span data-stu-id="73c00-125">**Expression** - the target attribute is populated based on the result of a script-like expression.</span></span> 
  <span data-ttu-id="73c00-126">Para más información, consulte [Escritura de expresiones para la asignación de atributos en Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="73c00-126">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="73c00-127">**Ninguno** : el atributo de destino se deja sin modificar.</span><span class="sxs-lookup"><span data-stu-id="73c00-127">**None** - the target attribute is left unmodified.</span></span> <span data-ttu-id="73c00-128">Sin embargo, si el atributo de destino está vacío, se rellena con el valor predeterminado que especifique.</span><span class="sxs-lookup"><span data-stu-id="73c00-128">However, if the target attribute is ever empty, it is populated with the Default value that you specify.</span></span>

<span data-ttu-id="73c00-129">Además de estos cuatro tipos básicos de asignaciones de atributos, las asignaciones de atributos personalizadas admiten el concepto de una asignación de valor **predeterminada** opcional.</span><span class="sxs-lookup"><span data-stu-id="73c00-129">In addition to these four basic attribute mapping types, custom attribute mappings support the concept of an optional **default** value assignment.</span></span> <span data-ttu-id="73c00-130">La asignación de valor predeterminada garantiza que un atributo de destino se rellene con un valor si no hay ningún valor en Azure AD ni en el objeto de destino.</span><span class="sxs-lookup"><span data-stu-id="73c00-130">The default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on the target object.</span></span> <span data-ttu-id="73c00-131">La configuración más habitual consiste en dejarlo en blanco.</span><span class="sxs-lookup"><span data-stu-id="73c00-131">The most common configuration is to leave this blank.</span></span>


## <a name="understanding-attribute-mapping-properties"></a><span data-ttu-id="73c00-132">Información sobre las propiedades de asignación de atributos</span><span class="sxs-lookup"><span data-stu-id="73c00-132">Understanding attribute mapping properties</span></span>

<span data-ttu-id="73c00-133">En la sección anterior, ya ha introducido la propiedad de tipo de asignación de atributos.</span><span class="sxs-lookup"><span data-stu-id="73c00-133">In the previous section, you have already been introduced to the attribute mapping type property.</span></span>
<span data-ttu-id="73c00-134">Además de esta propiedad, las asignaciones de atributos también admiten los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="73c00-134">In addition to this property, attribute mappings do also support the following attributes:</span></span>

- <span data-ttu-id="73c00-135">**Atributo de origen**: especifica el atributo de usuario del sistema de origen (p. ej.: Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="73c00-135">**Source attribute** - The user attribute from the source system (e.g.: Azure Active Directory).</span></span>
- <span data-ttu-id="73c00-136">**Atributo de destino**: especifica el atributo de usuario en el sistema de destino (p. ej.: ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="73c00-136">**Target attribute** – The user attribute in the target system (e.g.: ServiceNow).</span></span>
- <span data-ttu-id="73c00-137">**Hacer coincidir objetos con este atributo**: especifica si se debe usar o no esta asignación para identificar de forma unívoca a los usuarios entre los sistemas de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="73c00-137">**Match objects using this attribute** – Whether or not this mapping should be used to uniquely identify users between the source and target systems.</span></span> <span data-ttu-id="73c00-138">Normalmente esto se establece en el atributo userPrincipalName o mail en Azure AD, que se suele asignar a un campo de nombre de usuario en una aplicación de destino.</span><span class="sxs-lookup"><span data-stu-id="73c00-138">This is typically set on the userPrincipalName or mail attribute in Azure AD, which is typically mapped to a username field in a target application.</span></span>
- <span data-ttu-id="73c00-139">**Precedencia de coincidencia**: se pueden establecer varios atributos coincidentes.</span><span class="sxs-lookup"><span data-stu-id="73c00-139">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="73c00-140">Si hay varios, se evalúan en el orden definido por este campo.</span><span class="sxs-lookup"><span data-stu-id="73c00-140">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="73c00-141">En el momento en que se encuentre una coincidencia, no se evaluarán más atributos coincidentes.</span><span class="sxs-lookup"><span data-stu-id="73c00-141">As soon as a match is found, no further matching attributes are evaluated.</span></span>
- <span data-ttu-id="73c00-142">**Aplicar esta asignación**</span><span class="sxs-lookup"><span data-stu-id="73c00-142">**Apply this mapping**</span></span>
    - <span data-ttu-id="73c00-143">**Siempre**: esta asignación se aplica a las acciones de creación y actualización de usuarios</span><span class="sxs-lookup"><span data-stu-id="73c00-143">**Always** – Apply this mapping on both user creation and update actions</span></span>
    - <span data-ttu-id="73c00-144">**Solo durante la creación**: esta asignación se aplica solo a las acciones de creación de usuarios</span><span class="sxs-lookup"><span data-stu-id="73c00-144">**Only during creation** - Apply this mapping only on user creation actions</span></span>


## <a name="what-you-should-know"></a><span data-ttu-id="73c00-145">Qué debería saber</span><span class="sxs-lookup"><span data-stu-id="73c00-145">What you should know</span></span>

<span data-ttu-id="73c00-146">Microsoft Azure AD proporciona una implementación eficaz de un proceso de sincronización.</span><span class="sxs-lookup"><span data-stu-id="73c00-146">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="73c00-147">En un entorno inicializado, sólo los objetos que requieren actualizaciones se procesan durante un ciclo de sincronización.</span><span class="sxs-lookup"><span data-stu-id="73c00-147">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="73c00-148">Actualizar las asignaciones de atributos repercute en el rendimiento de un ciclo de sincronización.</span><span class="sxs-lookup"><span data-stu-id="73c00-148">Updating attribute mappings has an impact on the performance of a synchronization cycle.</span></span> <span data-ttu-id="73c00-149">Una actualización de la configuración de la asignación de atributos requiere que se vuelvan a evaluar todos los objetos administrados.</span><span class="sxs-lookup"><span data-stu-id="73c00-149">An update to the attribute mapping configuration requires all managed objects to be reevaluated.</span></span> <span data-ttu-id="73c00-150">Es un procedimiento recomendado mantener el número mínimo de cambios consecutivos de las asignaciones de atributos.</span><span class="sxs-lookup"><span data-stu-id="73c00-150">It is a recommended best practice to keep the number of consecutive changes to your attribute mappings at a minimum.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73c00-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="73c00-151">Next steps</span></span>

* [<span data-ttu-id="73c00-152">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73c00-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="73c00-153">Automatización del aprovisionamiento y desaprovisionamiento de usuarios para aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73c00-153">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="73c00-154">Escritura de expresiones para asignaciones de atributos</span><span class="sxs-lookup"><span data-stu-id="73c00-154">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="73c00-155">Filtros de ámbito para el aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="73c00-155">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="73c00-156">Uso de SCIM para habilitar el aprovisionamiento automático de usuarios y grupos de Azure Active Directory a aplicaciones</span><span class="sxs-lookup"><span data-stu-id="73c00-156">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="73c00-157">Notificaciones de aprovisionamiento de cuentas</span><span class="sxs-lookup"><span data-stu-id="73c00-157">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="73c00-158">Lista de tutoriales sobre cómo integrar aplicaciones SaaS</span><span class="sxs-lookup"><span data-stu-id="73c00-158">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

