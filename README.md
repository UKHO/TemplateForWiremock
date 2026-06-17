# WireMock.net Deployment Example

This provides one example of how a WireMock service can be packaged for deployment.

> For many testing needs WireMock can be used __inline__ directly from your test code. Inline use is often more convenient, and the mock code can be kept closer to the test code than when using a deployed instance. Deciding whether to use a deployed instance, a standalone instance running locally, or start an instance of wiremock directly from your code is a matter of choosing the best test design for the purpose at hand. A deployed mock might only make sense for tests run against a deployed system or service.

> **Threat modelling**: This template is a minimal functional demonstration of wiremock as a tool. Features like authentication and authorisation are not demonstrated, though these can be implemented at the wiremock layer if not available at the hosting layer. You will need to conduct your own threat modelling as part of your project. Deploying the application in this template *as is* will grant unrestricted access to the mock server in a given network context.


See https://github.com/WireMock-Net/WireMock.Net/wiki for an outline of the different use cases (including 'unit tesing', standalone and deployed).

## Start up

Running `dotnet run` from TemplateForWiremock\WireMockTemplate will start the web application. Deployment to an azure app service can also be done in the usual way.

## Using this app you will get:
- A web application hosting a WireMock instance with configurable responses as defined by the json files in the `__admin\mappings` folder in the repo
- Automatic recording of requests received by the mock. Records of requests can be accessed from the `http://localhost:5161/__admin/requests` endpoint
- A starting point for using more advanced features of WireMock.

## Other considerations
- When hosting as a web application in Azure, consider attaching a blob storage container or similar to a web application at the path `__admin\mappings` where the mappings are held, so that mock behavior can be changed in-flight by just modifying the mapping files.
- There is a library available for remotely controlling deployed WireMock instances from .net projects: https://www.nuget.org/packages/WireMock.Net.RestClient

## Example mappings

- The example mappings in this template are set so that:
    - At the endpoint `/my_stub_endpoint`, POST requests not matching other rules should be given a 200 OK response. 
    - To demonstrate request matching, If the POST request to `/my_stub_mapping` contained an XML body:
        `<PRODUCTNAME>000XX5</PRODUCTNAME>` with `XX5` in `<PRODUCTNAME>`, the server is set to return a 500 Server Error.  With `XX0` in the product name, the server is set to delay a 200 OK response by 10 seconds.

## Contributing

Currently we are not accepting contributions to this repository. You can read the [UKHO's Open Source Policy here](https://github.com/UKHO/docs/blob/main/software-engineering-policies/OpenSourceContribution/OpenSourceContributionPolicy.md)
