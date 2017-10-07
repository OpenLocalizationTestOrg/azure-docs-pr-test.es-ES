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
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a>Cómo tooview SAML devuelve hello Azure Access Control Service
Esta guía le mostrará cómo hello tooview subyacente de lenguaje de marcado de aserción de seguridad (SAML) devuelve tooyour aplicación hello Azure Access Control Service (ACS). Guía de Hola se basa en hello [cómo tooAuthenticate usuarios Web con Azure Access Control Service mediante Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) tema, al proporcionar código que muestra información de SAML de Hola. aplicación Hello completado tendrá un aspecto similar a continuación toohello.

![Salida de SAML de ejemplo][saml_output]

Para obtener más información sobre ACS, vea hello [pasos siguientes](#next_steps) sección.

> [!NOTE]
> Hola filtro de Control de servicios de acceso de Azure es community technology preview. Como versión preliminar de software, no cuenta formalmente con el respaldo de Microsoft.
> 
> 

## <a name="prerequisites"></a>Requisitos previos
tareas de hello toocomplete en esta guía, completa Hola ejemplo en [cómo tooAuthenticate usuarios Web con Azure Access Control Service mediante Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) y usarlo como punto de partida para este tutorial de Hola.

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a>Agregar Hola JspWriter biblioteca tooyour implementación y ruta de acceso del ensamblado de compilación
Agregar la biblioteca de Hola que contiene Hola **javax.servlet.jsp.JspWriter** clase tooyour ensamblado de implementación y ruta de acceso de compilación. Si usas Tomcat, biblioteca de hello es **jsp api.jar**, que se encuentra en hello Apache **lib** carpeta.

1. En el Explorador de proyectos de Eclipse, haga clic en **MyACSHelloWorld**, haga clic en **Build Path**, haga clic en **configurar la ruta de acceso de compilación**, haga clic en hello **bibliotecas** ficha y, a continuación, haga clic en **agregar JAR externo**.
2. Hola **JAR de selección** cuadro de diálogo, desplácese toohello JAR necesario, selecciónelo y, a continuación, haga clic en **abiertos**.
3. Con hello **propiedades de MyACSHelloWorld** diálogo sigue abierto, haga clic en **ensamblado de implementación**.
4. Hola **ensamblado de implementación Web** cuadro de diálogo, haga clic en **agregar**.
5. Hola **nueva directiva de ensamblado** cuadro de diálogo, haga clic en **las entradas de ruta de acceso de compilación de Java** y, a continuación, haga clic en **siguiente**.
6. Seleccione una biblioteca adecuada de Hola y haga clic en **finalizar**.
7. Haga clic en **Aceptar** tooclose hello **propiedades de MyACSHelloWorld** cuadro de diálogo.

## <a name="modify-hello-jsp-file-toodisplay-saml"></a>Modificar el archivo toodisplay SAML de hello JSP
Modificar **index.jsp** hello toouse siguiente código.

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

## <a name="run-hello-application"></a>Ejecutar la aplicación hello
1. Ejecutar la aplicación en el emulador de cálculo de Hola o implementar tooAzure, mediante los pasos de hello documentados en [cómo tooAuthenticate usuarios Web con Azure Access Control Service mediante Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).
2. Inicie un explorador y abra la aplicación web. Después de que ha iniciado sesión en la aplicación tooyour, podrá ver información de SAML, incluida la aserción de seguridad de hello proporcionada por el proveedor de identidades de Hola.

## <a name="next-steps"></a>Pasos siguientes
toofurther explorar la funcionalidad de ACS y tooexperiment con escenarios más complejos, vea [Access Control Service 2.0][Access Control Service 2.0].

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
