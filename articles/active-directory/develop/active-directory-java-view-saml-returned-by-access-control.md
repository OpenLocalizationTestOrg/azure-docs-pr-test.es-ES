---
title: "Visualización del SAML que devuelve el servicio de control de acceso (Java)"
description: "Obtenga información acerca de cómo ver SAML devuelto por el servicio de Control de acceso en las aplicaciones de Java hospedadas en Azure."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6cd216f9-eb43-46b4-b30d-f194d0ae2d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: 1552e624a4703138ab82f7133ceaec3dbd04e1db
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-view-saml-returned-by-the-azure-access-control-service"></a><span data-ttu-id="b941f-103">Visualización del SAML que devuelve el servicio de control de acceso de Azure</span><span class="sxs-lookup"><span data-stu-id="b941f-103">How to view SAML returned by the Azure Access Control Service</span></span>
<span data-ttu-id="b941f-104">En esta guía se explica cómo ver el lenguaje de marcado de aserción de seguridad (SAML) subyacente devuelto a la aplicación mediante el servicio de control de acceso de Azure (ACS).</span><span class="sxs-lookup"><span data-stu-id="b941f-104">This guide will show you how to view the underlying Security Assertion Markup Language (SAML) returned to your application by the Azure Access Control Service (ACS).</span></span> <span data-ttu-id="b941f-105">La guía se elabora a partir del tema [Autenticación de usuarios web con el servicio de control de acceso de Azure mediante Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) y proporciona código que muestra la información de SAML.</span><span class="sxs-lookup"><span data-stu-id="b941f-105">The guide builds on the [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays the SAML information.</span></span> <span data-ttu-id="b941f-106">La aplicación completa tendrá un aspecto similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="b941f-106">The completed application will look similar to the following.</span></span>

![Salida de SAML de ejemplo][saml_output]

<span data-ttu-id="b941f-108">Para obtener más información sobre ACS, consulte la sección [Pasos siguientes](#next_steps) .</span><span class="sxs-lookup"><span data-stu-id="b941f-108">For more information on ACS, see the [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="b941f-109">El filtro de control de los servicios de acceso de Azure es una Community Technology Preview.</span><span class="sxs-lookup"><span data-stu-id="b941f-109">The Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="b941f-110">Como versión preliminar de software, no cuenta formalmente con el respaldo de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b941f-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b941f-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b941f-111">Prerequisites</span></span>
<span data-ttu-id="b941f-112">Para llevar a cabo las tareas de esta guía, complete el ejemplo de [Autenticación de usuarios web con Azure Access Control Service mediante Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) y úselo como punto de partida de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b941f-112">To complete the tasks in this guide, complete the sample at [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as the starting point for this tutorial.</span></span>

## <a name="add-the-jspwriter-library-to-your-build-path-and-deployment-assembly"></a><span data-ttu-id="b941f-113">Incorporación de la biblioteca JspWriter a la ruta de acceso de compilación y el ensamblado de implementación</span><span class="sxs-lookup"><span data-stu-id="b941f-113">Add the JspWriter library to your build path and deployment assembly</span></span>
<span data-ttu-id="b941f-114">Agregue la biblioteca que contiene la clase **javax.servlet.jsp.JspWriter** a la ruta de acceso de la compilación y el ensamblado de implementación.</span><span class="sxs-lookup"><span data-stu-id="b941f-114">Add the library that contains the **javax.servlet.jsp.JspWriter** class to your build path and deployment assembly.</span></span> <span data-ttu-id="b941f-115">Si usa Tomcat, la biblioteca es **jsp-api.jar**, que se encuentra en la carpeta **lib** de Apache.</span><span class="sxs-lookup"><span data-stu-id="b941f-115">If you are using Tomcat, the library is **jsp-api.jar**, which is located in the Apache **lib** folder.</span></span>

1. <span data-ttu-id="b941f-116">En el Explorador de proyectos de Eclipse, haga clic con el botón derecho en **MyACSHelloWorld**, haga clic en **Build Path** (Ruta de acceso de compilación), después en **Configure Build Path** (Configurar ruta de acceso de compilación), seguidamente en la pestaña **Libraries** (Bibliotecas) y, por último, en **Add External JARs** (Agregar JAR internos).</span><span class="sxs-lookup"><span data-stu-id="b941f-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click the **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="b941f-117">En el cuadro de diálogo **JAR Selection** (Selección de JAR), navegue hasta el JAR necesario, selecciónelo y, haga clic en **Open** (Abrir).</span><span class="sxs-lookup"><span data-stu-id="b941f-117">In the **JAR Selection** dialog, navigate to the necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="b941f-118">Con el cuadro de diálogo **Properties for MyACSHelloWorld** (Propiedades de MyACSHelloWorld) abierto, haga clic en **Deployment Assembly** (Ensamblado de implementación).</span><span class="sxs-lookup"><span data-stu-id="b941f-118">With the **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="b941f-119">En el cuadro de diálogo **Web Deployment Assembly** (Ensamblado de implementación web), haga clic en **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="b941f-119">In the **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="b941f-120">En el cuadro de diálogo **New Assembly Directive** (Nueva directiva de ensamblado), haga clic en **Java Build Path Entries** (Entradas de ruta de acceso de compilación de Java) y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="b941f-120">In the **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="b941f-121">Seleccione la biblioteca pertinente y haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="b941f-121">Select the appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="b941f-122">Haga clic en **OK** (Aceptar) para cerrar el cuadro de diálogo **Properties for MyACSHelloWorld** (Propiedades de MyACSHelloWorld).</span><span class="sxs-lookup"><span data-stu-id="b941f-122">Click **OK** to close the **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-the-jsp-file-to-display-saml"></a><span data-ttu-id="b941f-123">Modificación del archivo JSP para que muestre el SAML</span><span class="sxs-lookup"><span data-stu-id="b941f-123">Modify the JSP file to display SAML</span></span>
<span data-ttu-id="b941f-124">Modifique **index.jsp** para que use el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="b941f-124">Modify **index.jsp** to use the following code.</span></span>

    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
        <%@ page import="javax.xml.parsers.*"
                 import="javax.xml.transform.*"
                 import="org.w3c.dom.*"
                 import="java.io.*"
                 import="javax.xml.transform.stream.*"
                 import="javax.xml.transform.dom.*"
                 import="javax.xml.xpath.*"
                 import="javax.servlet.jsp.JspWriter" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Sample ACS Filter</title>
    </head>
    <body>
        <h3>SAML information from sample ACS program</h3>
        <%!
        void displaySAMLInfo(Node node, String parent, JspWriter out)
        {

            try
            {
                String nodeName;
                int nChild, i;

                nodeName = node.getNodeName();
                out.println("<br>");
                out.println("<u>Examining <b>" + parent + nodeName + "</b></u><br>");

                   // Attributes.
                   NamedNodeMap attribsMap = node.getAttributes();
                   if (null != attribsMap)
                   {
                         for (i=0; i < attribsMap.getLength(); i++)
                         {
                                Node attrib = attribsMap.item(i);
                                out.println("Attribute: <b>" + attrib.getNodeName() + "</b>: " + attrib.getNodeValue()  + "<br>");
                         }
                   }

                   // Child nodes.
                   NodeList list = node.getChildNodes();
                   if (null != list)
                    {
                          nChild = list.getLength();
                          if (nChild > 0)
                          {                    

                                 // If it is a text node, just print the text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out the child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate the names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish the sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process the child nodes.
                                     for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);
                                        displaySAMLInfo(temp, parent + nodeName + "\\", out);
                                     }
                               }
                          }
                      }
                  }
                catch (Exception e)
                {
                    System.out.println("Exception encountered.");
                    e.printStackTrace();            
                }
            }
        %>

        <%
        try
        {
            String data  = (String) request.getAttribute("ACSSAML");

            DocumentBuilder docBuilder;
            Document doc = null;
            DocumentBuilderFactory docBuilderFactory = DocumentBuilderFactory.newInstance();
            docBuilderFactory.setIgnoringElementContentWhitespace(true);
            docBuilder = docBuilderFactory.newDocumentBuilder();
            byte[] xmlDATA = data.getBytes();

            ByteArrayInputStream in = new ByteArrayInputStream(xmlDATA);
            doc = docBuilder.parse(in);
            doc.getDocumentElement().normalize();

            // Iterate the child nodes of the doc.
            NodeList list = doc.getChildNodes();

            for (int i=0; i < list.getLength(); i++)
            {
                displaySAMLInfo(list.item(i), "", out);
            }
        }
        catch (Exception e)
        {
            out.println("Exception encountered.");
            e.printStackTrace();
        }

        %>
    </body>
    </html>

## <a name="run-the-application"></a><span data-ttu-id="b941f-125">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="b941f-125">Run the application</span></span>
1. <span data-ttu-id="b941f-126">Ejecute la aplicación en el emulador del equipo o realice la implementación en Azure; para ello, siga los pasos descritos en [Autenticación de usuarios web con Azure Access Control Service mediante Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="b941f-126">Run your application in the computer emulator or deploy to Azure, using the steps documented at [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="b941f-127">Inicie un explorador y abra la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b941f-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="b941f-128">Después de iniciar sesión en la aplicación, verá la información de SAML, incluida la aserción de seguridad proporcionada por el proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="b941f-128">After you log on to your application, you'll see SAML information, including the security assertion provided by the identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b941f-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b941f-129">Next steps</span></span>
<span data-ttu-id="b941f-130">Para seguir explorando la funcionalidad de ACS y experimentar con escenarios más sofisticados, consulte [Access Control Service 2.0][Access Control Service 2.0].</span><span class="sxs-lookup"><span data-stu-id="b941f-130">To further explore ACS's functionality and to experiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify the JSP file to display SAML]: #modify_jsp
[Add the JspWriter library to your build path and deployment assembly]: #add_library
[Run the application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How to Authenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
