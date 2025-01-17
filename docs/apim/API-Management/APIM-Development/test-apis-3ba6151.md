<!-- loio3ba6151391bc474b9f1fa69455f65e3b -->

<link rel="stylesheet" type="text/css" href="../../css/sap-icons.css"/>

# Test APIs

Use the API Test Console to test the runtime behavior of APIs

SAP API Management provides an *API Test Console*, which enables you to test your APIs. Testing an API is essential to understand the runtime behavior of the APIs. The test console allows you to explore the resources associated with an API and execute the operations.

The API Test Console allows you to test OData and REST-based services.



## Procedure

**Context**: You have logged on to the API portal or API business hub enterprise.

1.  Log on to the API portal.

2.  From the navigation bar on the left choose the <span class="SAP-icons">?</span> *API Test Console* .
3.  A list of APIs appears on the left.

    > ### Note:  
    > An API Admin can view both registered and published APIs. However, an App Developer can only view a list of published APIs.

4.  Select the required API.

    The URL for the selected API is populated automatically in the *API Test Console*. For the selected API, the URLs of the supported resources appear in the dropdown list. One resource is selected by default.

5.  If you want to choose a different collection, use the dropdown list to select the required collection
6.  If you have the URL of the service that contains the API, enter the service URL.
7.  Choose *Authentication* to select the required type of authentication. You can choose from the following options:
    1.  *None*: No authentication required.
    2.  *Basic Authentication*: Provide a user name and password.

8.  Enable the required method:
    -   *GET*: Reads an entity
    -   *POST*: Creates an entity
    -   *PUT*: Updates an entity
    -   *DELETE*: Deletes an entity

        > ### Note:  
        > You can enable only the methods supported by the service.


9.  Enter the *Request Body* for PUT and POST methods.
10. Choose *Header* to add a header.

    > ### Note:  
    > If you want to add multiple headers, choose *Add Request Headers*.

11. Choose *Url Params* to enter the query parameter and value.

    > ### Note:  
    > If you want to add multiple query parameters, choose the button *Add URL Params*. Test Console supports passing of custom headers such as X-sap-apimgt-proxy-host:-proxy-trai and X-sap-apimgt-proxy-port:- 8080

12. Choose *Send.* 

    The response appears in the tabs:

    -   *Body*: View the formatted response.
    -   *Body \(Raw\)*: View the unformatted response.
    -   *Headers*: View the headers.
    -   *Cookies*: View the cookies.

13. If you want to use the response body as an input request, choose *Use as Request* on the *Body \(Raw\)* tab.
14. To view the transactions based on the testing activity that you did, choose *Launch API Viewer*. For more information on tracing API proxy, see [Debug API](debug-api-fb2c7aa.md)

