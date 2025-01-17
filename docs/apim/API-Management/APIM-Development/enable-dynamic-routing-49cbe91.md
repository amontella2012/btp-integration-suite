<!-- loio49cbe91782a34f8996204eb16c237204 -->

# Enable Dynamic Routing

Define route rules to enable dynamic routing in an API proxy.



## Context

A route connects an API proxy endpoint to an API target endpoint. It governs the path of a request from proxy endpoint to target endpoint and determines which target endpoint to invoke based on the condition defined in proxy EndPoint definition. Typically, a route includes a URL used to access the API proxy endpoint and a URL of the backend service defined in target endpoint definition.

In API Management, when you create an API proxy, a deafult route rule is set and it always forwards the request to the default target endpoint defined in target endpoint definition. When more than one target endpoint is defined, the route rule evaluates the condition set in proxy endpoint definition. If the condition evaluates to true, it forwards the request to the named target endpoint.

The following procedure describes how to achieve dynamic routing in API Management. Let’s say you want to route an API proxy request to two different target endpoints, a default target endpoint and a new target endpoint based on a condition set in the proxy endpoint definition.

For our implementation, let’s consider the following two target endpoints:

-   Target\_Endpoint\_1 \(default\)

    `https://services.odata.org/V2/Northwind/Northwind.svc/`

-   Target\_Endpoint\_2

    `https://services.odata.org/V2/OData/OData.svc/`




## Procedure

1.  **Creating a simple API proxy**
2.  Navigate to API portal.

3.  Choose the navigation icon on the left and choose *Develop*.

4.  Under *APIs*, choose *Create* to create a simple API proxy.

5.  In the *Create API* wizard, choose the *URL* radio button.

    > ### Note:  
    > You can also choose to create an API by choosing the *API Provider* option. For more information, see [Create an API](create-an-api-c0842d5.md) 

6.  In the *URL* field, enter the target URL of your backend service. In this case, URL pointing to Target\_Endpoint\_1 \(default\).

7.  Enter a name and a title for your API proxy. In this case, let’s enter the API proxy name as `Dynamic_Routing`.

8.  Scroll down the wizard and enter the base path of your API proxy in the *API Base Path* field. In this case, let’s enter the base path as `/multitargets`.

9.  Choose *Create*.

10. Save and deploy your API proxy.

    > ### Note:  
    > When the API proxy is created, the default route rule is set. It points to the default target endpoint and no rule is attached to it.

11. **Steps for defining new target endpoint**
12. Navigate to the *Develop* tab. From the *APIs* list, choose the API proxy that you deployed.

13. Download the newly deployed API proxy using the *Export* option. For more information, see [Export an API](export-an-api-420abb6.md)

    A zip file called `Dynamic_Routing.zip` is downloaded.

14. Unzip the `Dynamic_Routing.zip` file.

    A parent folder called `APIProxy` is created. The `APIProxy` folder consists of various subfolders and files. For more information, see [API Proxy Structure](api-proxy-structure-4dfd54a.md).

15. Open the `APITargetEndPoint` subfolder.

    You see a file named `default.xml`. The `default.xml` file contains the URL of the default target endpoint.

16. Create a new XML file named `Target_EndPoint_2.xml` with the following content. In the `Target_EndPoint_2.xml file`, you need to enter a name and the URL of the new target endpoint to which the request must be routed dynamically.

    > ### Note:  
    > The ***<isDefault\>*** attribute must be set to `false` for all the new target endpoints that you define. Whereas, for the default target endpoint the ***<isDefault\>*** attribute would by default be set to `true`.

    > ### Sample Code:  
    > ```
    > <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    > <TargetEndPoint>
    >     <name>Target_EndPoint_2</name>
    >     <url>https://services.odata.org/V2/OData/OData.svc/</url>
    >     <provider_id>NONE</provider_id>
    >     <isDefault>false</isDefault>
    >     <properties/>
    >     <faultRules/>
    >     <preFlow>
    >         <name>PreFlow</name>
    >     </preFlow>
    >     <postFlow>
    >         <name>PostFlow</name>
    >     </postFlow>
    >     <conditionalFlows/>
    > </TargetEndPoint>
    > 
    > ```

    You see two files named `default.xml` and `Target_EndPoint_2.xml` in the `APITargetEndPoint` subfolder.

17. **Steps for defining conditions using Route Rule**
18. Open the `APIProxyEndPoint` subfolder.

    You see a file named `default.xml` file.

19. Open the `default.xml` file.

    The default.xml file contains information about your API proxy such as base path, flows, policies and, the default route rule.

    > ### Sample Code:  
    > ```
    > <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    > <ProxyEndPoint default="true">
    >     <name>default</name>
    >     <base_path>/multitargets</base_path>
    >     <properties/>
    >     <routeRules>
    >         <routeRule>
    >             <name>default</name>
    >             <targetEndPointName>default</targetEndPointName>
    >             <sequence>1</sequence>
    >             <faultRules/>
    >         </routeRule>
    >     </routeRules>
    >     <faultRules/>
    >     <preFlow>
    >         <name>PreFlow</name>
    >     </preFlow>
    >     <postFlow>
    >         <name>PostFlow</name>
    >     </postFlow>
    >     <conditionalFlows/>
    > </ProxyEndPoint>
    > 
    > 
    > ```

20. Update the value of the `<sequence>` attribute to 2.

    > ### Sample Code:  
    > ```
    > <routeRule>
    >             <name>default</name>
    >             <targetEndPointName>default</targetEndPointName>
    >             <sequence>2</sequence>
    >             <faultRules/>
    >         </routeRule>
    > 
    > ```

    The resulting default.xml file must reflect the following content.

    > ### Sample Code:  
    > ```
    > <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    > <ProxyEndPoint default="true">
    >     <name>default</name>
    >     <base_path>/multitargets</base_path>
    >     <properties/>
    >     <routeRules>
    >             <routeRule>
    >             <name>default</name>
    >             <targetEndPointName>default</targetEndPointName>
    >             <sequence>2</sequence>
    >             <faultRules/>
    >         </routeRule>
    >     </routeRules>
    >     <faultRules/>
    >     <preFlow>
    >         <name>PreFlow</name>
    >     </preFlow>
    >     <postFlow>
    >         <name>PostFlow</name>
    >     </postFlow>
    >     <conditionalFlows/>
    > </ProxyEndPoint>
    > 
    > ```

21. Define a new route rule named `Target_EndPoint_2` by adding the following content to the `default.xml` file.

    > ### Sample Code:  
    > ```
    > <routeRule>
    >             <name>Target_EndPoint_2</name>
    >              <targetEndPointName>Target_EndPoint_2</targetEndPointName>
    >             <sequence>1</sequence>
    > 	<faultRules/>
    > </routeRule>
    > 
    > ```

    The resulting default.xml file must reflect the following content.

    > ### Sample Code:  
    > ```
    > <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    > <ProxyEndPoint default="true">
    >     <name>default</name>
    >     <base_path>/multitargets</base_path>
    >     <properties/>
    >     <routeRules>
    >         <routeRule>
    >             <name>Target_EndPoint_2</name>
    >             <targetEndPointName>Target_EndPoint_2</targetEndPointName>
    >             <sequence>1</sequence>
    >             <faultRules/>
    >         </routeRule>
    >         <routeRule>
    >             <name>default</name>
    >             <targetEndPointName>default</targetEndPointName>
    >             <sequence>2</sequence>
    >             <faultRules/>
    >         </routeRule>
    >     </routeRules>
    >     <faultRules/>
    >     <preFlow>
    >         <name>PreFlow</name>
    >     </preFlow>
    >     <postFlow>
    >         <name>PostFlow</name>
    >     </postFlow>
    >     <conditionalFlows/>
    > </ProxyEndPoint>
    > 
    > ```

22. Define a condition based on which you want to route the request dynamically. In this case, let’s add a `proxy.pathsuffix MatchesPath` condition under the Target\_EndPoint\_2 Route Rule and set it to the path called `/Categories`.

    > ### Sample Code:  
    > ```
    > <routeRule>
    >             <name>Target_EndPoint_2</name>
    > 		  <conditions>proxy.pathsuffix MatchesPath "/Categories"</conditions>
    >             <targetEndPointName>Target_EndPoint_2</targetEndPointName>
    >             <sequence>1</sequence>
    >             <faultRules/>
    > 
    > ```

    The resulting default.xml file must reflect the following content.

    > ### Sample Code:  
    > ```
    > <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    > <ProxyEndPoint default="true">
    >     <name>default</name>
    >     <base_path>/multitargets</base_path>
    >     <properties/>
    >     <routeRules>
    >         <routeRule>
    >             <name>Target_EndPoint_2</name>
    >             <conditions>proxy.pathsuffix MatchesPath "/Categories"</conditions>
    >             <targetEndPointName>Target_EndPoint_2</targetEndPointName>
    >             <sequence>1</sequence>
    >             <faultRules/>
    >         </routeRule>
    >         <routeRule>
    >             <name>default</name>
    >             <targetEndPointName>default</targetEndPointName>
    >             <sequence>2</sequence>
    >             <faultRules/>
    >         </routeRule>
    >     </routeRules>
    >     <faultRules/>
    >     <preFlow>
    >         <name>PreFlow</name>
    >     </preFlow>
    >     <postFlow>
    >         <name>PostFlow</name>
    >     </postFlow>
    >     <conditionalFlows/>
    > </ProxyEndPoint>
    > 
    > ```

    > ### Note:  
    > If you have defined more than one route rule in the proxy endpoint as shown in the above codeblock, their sequence in the XML configuration is important. The first Route Rule to match gets executed. \(Route rules with no condition always match\). In the above codebloack, if the `default` route rule appeared first, it would be executed even if the condition of the `Target_EndPoint_2` route rule would have matched. Hence, it is always recommended to list your conditional route rules before an unconditional route rule.

23. Open the `<API_Proxy_Name>.xml` file. In this case, `Dynamic_Routing.xml` file.

24. Add the new target endpoint name that you defined.

    > ### Sample Code:  
    > ```
    > <targetEndPoints>
    >         <targetEndPoint>Target_EndPoint_2</targetEndPoint>
    >         <targetEndPoint>default</targetEndPoint>
    >     </targetEndPoints>
    > 
    > ```

25. **Steps for viewing dynamic routing**
26. Compress the `APIProxy` parent folder.

27. Navigate to API portal and import the compressed `APIProxy.zip` file. For more information, see [Import an API](import-an-api-9342a93.md).

28. Choose the imported API proxy.

29. Under *Proxy EndPoint* tab, in the *Route Rules* section, you must see two Route Rules that you defined earlier.

    > ### Note:  
    > You can also add route conditions directly in API portal User Interface instead of adding it manually in the API proxy EndPoint definition file as shown in step 19.

30. Click on the API proxy URL.

    The request must be routed to the default target endpoint.

31. Append `/Categories` to the API proxy URL in your browser.

    The request must be routed dynamically to the new target endpoint.

    To validate the response, copy and paste the actual URL of the backend service with path suffix `/Categories`.

    The response obtained must match the response obtained in step 27.

    > ### Note:  
    > All the policies that you attach in the target endpoint via the API portal user interface are applied only to the default target endpoint. In case, if you need to enforce policies on the non-default target endpoint, then you must import the API proxy bundle and manually add the policies in the required target endpoint definition file.


**Related Information**  


[https://blogs.sap.com/2019/06/03/building-a-loopback-api-using-sap-cloud-platform-api-management/](https://blogs.sap.com/2019/06/03/building-a-loopback-api-using-sap-cloud-platform-api-management/)

