---
title: "Fix Port number for Service Fabric ASP.NET Core on the local development machine"
date: 2020-11-15T19:45:09Z
draft: false
---
# Fix Port number for Service Fabric ASP.NET Core on the local development machine

You can run ASP.NET Core API app as a Service Fabric service. By default, the port number of the api host will be decided by the Service Fabric service. This cause one issue that the port number can change when you restart the cluster. When you run your integration tests locally, you want the API port number to be fixed like "http://localhost:8221"

To do so, you need to fix the port number for your local machine. On other environments like Staging or Production, you can let the Service Fabric service decide it.

## ApplicationManifest.xml

Update the manifest file to have ResourceOverrides with Endpoint settings. Add a parameter for port number.

```markup
<Parameters>
  ...
  <Parameter Name="Api_Port" DefaultValue="" />
</Parameters>
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Service.ApiPkg"
   ServiceManifestVersion="1.0.0" />
  <ConfigOverrides />
  <ResourceOverrides>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint" Port="[Api_Port]"
       Protocol="http" Type="Input" />
    </Endpoints>
  </ResourceOverrides>
  ...
```

The defaultt value is empty, which means the Service Fabric service will decide it.

In ApplicationParameters directory, you have 3 files

* Cloud.xml
* Local.1Node.xml
* Local.5Node.xml

Cloud.xml contains parameter values for remote environments like Production. Local.xNode.xml files have the same parameters for local environment as the name suggest.

```markup
# Cloud.xml
<Parameter Name="Api_Port" Value="" />

# Local.1Node.xml, Local.5Node.xml
<Parameter Name="Api_Port" Value="8221" />
```

Then the port number will be 8221 on the local cluster only.

