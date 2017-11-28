---
title: aaaView SAML devuelto por hello Access Control Service (Java)
description: "Obtenga información acerca de cómo tooview SAML que devuelve Hola Access Control Service en aplicaciones de Java se hospeda en Azure."
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
ms.openlocfilehash: b6733bc98b505cfa89a4ce456f368ee15da11427
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a><span data-ttu-id="9fa70-103">Cómo tooview SAML devuelve hello Azure Access Control Service</span><span class="sxs-lookup"><span data-stu-id="9fa70-103">How tooview SAML returned by hello Azure Access Control Service</span></span>
<span data-ttu-id="9fa70-104">Esta guía le mostrará cómo hello tooview subyacente de lenguaje de marcado de aserción de seguridad (SAML) devuelve tooyour aplicación hello Azure Access Control Service (ACS).</span><span class="sxs-lookup"><span data-stu-id="9fa70-104">This guide will show you how tooview hello underlying Security Assertion Markup Language (SAML) returned tooyour application by hello Azure Access Control Service (ACS).</span></span> <span data-ttu-id="9fa70-105">Guía de Hola se basa en hello [cómo tooAuthenticate usuarios Web con Azure Access Control Service mediante Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) tema, al proporcionar código que muestra información de SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fa70-105">hello guide builds on hello [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays hello SAML information.</span></span> <span data-ttu-id="9fa70-106">aplicación Hello completado tendrá un aspecto similar a continuación toohello.</span><span class="sxs-lookup"><span data-stu-id="9fa70-106">hello completed application will look similar toohello following.</span></span>

![Salida de SAML de ejemplo][saml_output]

<span data-ttu-id="9fa70-108">Para obtener más información sobre ACS, vea hello [pasos siguientes](#next_steps) sección.</span><span class="sxs-lookup"><span data-stu-id="9fa70-108">For more information on ACS, see hello [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="9fa70-109">Hola filtro de Control de servicios de acceso de Azure es community technology preview.</span><span class="sxs-lookup"><span data-stu-id="9fa70-109">hello Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="9fa70-110">Como versión preliminar de software, no cuenta formalmente con el respaldo de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9fa70-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="9fa70-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9fa70-111">Prerequisites</span></span>
<span data-ttu-id="9fa70-112">tareas de hello toocomplete en esta guía, completa Hola ejemplo en [cómo tooAuthenticate usuarios Web con Azure Access Control Service mediante Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) y usarlo como punto de partida para este tutorial de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fa70-112">toocomplete hello tasks in this guide, complete hello sample at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as hello starting point for this tutorial.</span></span>

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a><span data-ttu-id="9fa70-113">Agregar Hola JspWriter biblioteca tooyour implementación y ruta de acceso del ensamblado de compilación</span><span class="sxs-lookup"><span data-stu-id="9fa70-113">Add hello JspWriter library tooyour build path and deployment assembly</span></span>
<span data-ttu-id="9fa70-114">Agregar la biblioteca de Hola que contiene Hola **javax.servlet.jsp.JspWriter** clase tooyour ensamblado de implementación y ruta de acceso de compilación.</span><span class="sxs-lookup"><span data-stu-id="9fa70-114">Add hello library that contains hello **javax.servlet.jsp.JspWriter** class tooyour build path and deployment assembly.</span></span> <span data-ttu-id="9fa70-115">Si usas Tomcat, biblioteca de hello es **jsp api.jar**, que se encuentra en hello Apache **lib** carpeta.</span><span class="sxs-lookup"><span data-stu-id="9fa70-115">If you are using Tomcat, hello library is **jsp-api.jar**, which is located in hello Apache **lib** folder.</span></span>

1. <span data-ttu-id="9fa70-116">En el Explorador de proyectos de Eclipse, haga clic en **MyACSHelloWorld**, haga clic en **Build Path**, haga clic en **configurar la ruta de acceso de compilación**, haga clic en hello **bibliotecas** ficha y, a continuación, haga clic en **agregar JAR externo**.</span><span class="sxs-lookup"><span data-stu-id="9fa70-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click hello **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="9fa70-117">Hola **JAR de selección** cuadro de diálogo, desplácese toohello JAR necesario, selecciónelo y, a continuación, haga clic en **abiertos**.</span><span class="sxs-lookup"><span data-stu-id="9fa70-117">In hello **JAR Selection** dialog, navigate toohello necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="9fa70-118">Con hello **propiedades de MyACSHelloWorld** diálogo sigue abierto, haga clic en **ensamblado de implementación**.</span><span class="sxs-lookup"><span data-stu-id="9fa70-118">With hello **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="9fa70-119">Hola **ensamblado de implementación Web** cuadro de diálogo, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="9fa70-119">In hello **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="9fa70-120">Hola **nueva directiva de ensamblado** cuadro de diálogo, haga clic en **las entradas de ruta de acceso de compilación de Java** y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9fa70-120">In hello **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="9fa70-121">Seleccione una biblioteca adecuada de Hola y haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="9fa70-121">Select hello appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="9fa70-122">Haga clic en **Aceptar** tooclose hello **propiedades de MyACSHelloWorld** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9fa70-122">Click **OK** tooclose hello **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-hello-jsp-file-toodisplay-saml"></a><span data-ttu-id="9fa70-123">Modificar el archivo toodisplay SAML de hello JSP</span><span class="sxs-lookup"><span data-stu-id="9fa70-123">Modify hello JSP file toodisplay SAML</span></span>
<span data-ttu-id="9fa70-124">Modificar **index.jsp** hello toouse siguiente código.</span><span class="sxs-lookup"><span data-stu-id="9fa70-124">Modify **index.jsp** toouse hello following code.</span></span>

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

                                 // If it is a text node, just print hello text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out hello child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate hello names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish hello sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process hello child nodes.
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

            // Iterate hello child nodes of hello doc.
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

## <a name="run-hello-application"></a><span data-ttu-id="9fa70-125">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="9fa70-125">Run hello application</span></span>
1. <span data-ttu-id="9fa70-126">Ejecutar la aplicación en el emulador de cálculo de Hola o implementar tooAzure, mediante los pasos de hello documentados en [cómo tooAuthenticate usuarios Web con Azure Access Control Service mediante Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="9fa70-126">Run your application in hello computer emulator or deploy tooAzure, using hello steps documented at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="9fa70-127">Inicie un explorador y abra la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="9fa70-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="9fa70-128">Después de que ha iniciado sesión en la aplicación tooyour, podrá ver información de SAML, incluida la aserción de seguridad de hello proporcionada por el proveedor de identidades de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fa70-128">After you log on tooyour application, you'll see SAML information, including hello security assertion provided by hello identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fa70-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9fa70-129">Next steps</span></span>
<span data-ttu-id="9fa70-130">toofurther explorar la funcionalidad de ACS y tooexperiment con escenarios más complejos, vea [Access Control Service 2.0][Access Control Service 2.0].</span><span class="sxs-lookup"><span data-stu-id="9fa70-130">toofurther explore ACS's functionality and tooexperiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
