---
uid: HealthEndpoints
---

# Health endpoints

You can configure Client Failover Service to produce and store health data at a designated health endpoint. You can use health data to ensure that your Client Failover Service is running properly and that data flows to the configured OMF endpoints.

## Configure health endpoint

A health endpoint designates an OMF endpoint where adapter health information is sent. You can configure multiple health endpoints.

Complete the following steps to configure health endpoints. Use the `PUT` method in conjunction with the `http://<host>:<port>/api/v1/configuration/healthendpoints` REST endpoint to initialize the configuration.

1. Using a text editor, create an empty text file.

2. Copy and paste an example configuration for health endpoints into the file.

    For sample JSON, see [Examples](#examples).

3. Update the example JSON parameters for your environment.

    For a table of all available parameters, see [Health endpoint parameters](#health-endpoint-parameters).

4. Save the file as a json file. For example, as `ConfigureHealthEndpoints.json`.

5. Open a command line session. Change directory to the location of the saved file from the previous step.

6. Enter the following cURL command (which uses the `PUT` method) to initialize the health endpoint configuration.

    ```bash
    curl -d "@<json file name>.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/system/healthendpoints"
    ```
    
 **Note:** For a list of other REST operations you can perform, like updating or replacing a health endpoints configuration, see [REST URLs](#rest-urls).

## Health endpoints schema

The full schema definition for the health endpoint configuration is in the `System_HealthEndpoints_schema.json` file located in the following folder:

`%ProgramFiles%\AVEVA\Adapters\<AdapterName>\Schemas`

## Health endpoint parameters

The following parameters are available for configuring health endpoints:

| Parameter                       | Required                            | Type      | Description                                        |
|---------------------------------|-------------------------------------|-----------|----------------------------------------------------|
| Id                        | Optional                            | `string`    | Uniquely identifies the endpoint. This can be any alphanumeric string. If left blank, a unique value is generated automatically. <br><br>Allowed value: any string identifier<br>Default value: new GUID|
| Endpoint                    | Required                            | `string`    | The URL of the OMF endpoint to receive this health data. <br><br>Allowed value: well-formed http or https endpoint string<br>Default: `null`|
| Username                    | Required for PI Web API endpoints   | `string`    | The username used to authenticate with a PI Web API OMF endpoint. <br><br>_PI server:_<br>Allowed value: any string<br>Default: `null`|
| Password                    | Required for PI Web API endpoints   | `string`    | The password used to authenticate with a PI Web API OMF endpoint. <br><br>_PI server:_<br>Allowed value: any string<br>Default: `null`|
| ClientId                    | Required for AVEVA Data Hub endpoints          | `string`    | The client ID used for authentication with an AVEVA Cloud Services OMF endpoint. <br><br>Allowed value: any string<br>Default: `null` |
| ClientSecret                | Required for AVEVA Data Hub endpoints          | `string`    | The client secret used for authentication with an AVEVA Cloud Services OMF endpoint. <br><br>Allowed value: any string<br>Default: `null`|
| TokenEndpoint | Optional for AVEVA Data Hub endpoints | `string` | Retrieves an AVEVA Data Hub token from an alternative endpoint. <br><br>Allowed value: well-formed http or https endpoint string <br>Default value: `null` |
| ValidateEndpointCertificate | Optional | `boolean`      | Disables verification of destination security certificate. Use for testing only with self-signed certificates; AVEVA recommends keeping this set to the default, true, in production environments. <br><br>Allowed value: `true` or `false`<br>Default value: `true`|

## Examples

### AVEVA Data Hub endpoint

```code
{
    "Id": "AVEVA Data Hub",
    "Endpoint": "https://<AVEVA Data Hub OMF endpoint>",
    "ClientId": "<clientid>",
    "ClientSecret": "<clientsecret>"
}
```

### PI Web API endpoint

```code
{
    "Id": "PI Web API",
    "Endpoint": "https://<pi web api server>:<port>/piwebapi/omf/",
    "Username": "<username>",
    "Password": "<password>"
}
```

**Note:** The property pair Username/Password is only for basic authentication with PI Web API.  The pair ClientId/ClientSecret is only for authentication with ADH. For PI Web API, if Username/Password are omitted, then Kerberos/NTLM is used instead.

## REST URLs

| Relative URL                                              | HTTP verb | Action               |
|-----------------------------------------------------------|-----------|----------------------|
| api/v1/configuration/system/healthEndpoints      | GET       | Gets all configured health endpoints |
| api/v1/configuration/system/healthEndpoints      | DELETE    | Deletes all configured health endpoints |
| api/v1/configuration/system/healthEndpoints      | POST      | Adds an array of health endpoints or a single endpoint. Fails if any endpoint already exists |
| api/v1/configuration/system/healthEndpoints      | PUT       | Replaces all health endpoints. **Note:** Requires an array of endpoints |
| api/v1/configuration/system/healthEndpoints     | PATCH     | Allows partial updating of configured health endpoints<br>**Note:** The request must be an array containing one or more health endpoints. Each health endpoint in the array must include its *Id*.  |
| api/v1/configuration/system/healthEndpoints/*Id* | GET       | Gets configured health endpoint by *Id* |
| api/v1/configuration/system/healthEndpoints/*Id*| DELETE     | Deletes configured health endpoint by *Id* |
| api/v1/configuration/system/healthEndpoints/*Id* | PUT       | Updates or creates a new health endpoint with the specified *Id* |
| api/v1/configuration/system/healthEndpoints/*Id* | PATCH     | Allows partial updating of configured health endpoint by *Id* |

**Note:** Replace *Id* with the ID of the health endpoint.

