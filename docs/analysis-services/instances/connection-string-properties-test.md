---
title: "Connection string properties (Analysis Services) | Microsoft Docs"
ms.date: 04/01/2020
ms.prod: sql
ms.technology: analysis-services
ms.custom:
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
monikerRange: "asallproducts-allversions || azure-analysis-services-current || power-bi-premium-current || >= sql-analysis-services-2016"
---
# Connection string properties

[!INCLUDE[ssas-appliesto-sqlas-all-aas-pbip](../../includes/ssas-appliesto-sqlas-all-aas-pbip.md)]

This article describes connection string properties used by client applications that connect to and query Analysis Services data.

Properties described here are used by the Analysis Services client libraries, ADOMD.NET, AMO, and OLE DB (MSOLAP) provider for Analysis Services. The majority of connection string properties can be used with all three client libraries. Exceptions are called out in the description.

Only a subset of the available properties are described here. The complete list includes numerous server and database properties, allowing you to customize a connection for a specific application, independent of how the instance or database is configured on the server. Developers creating custom connection strings in application code should review the API documentation for ADOMD.NET client to view a more detailed list: <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>  

## Connection properties

The following properties apply to Azure Analysis Services, Power BI Premium, and SQL Server Analysis Services.

### Data Source or DataSource

#### Applies to

Azure AS, SSAS, Power BI

#### Description

Specifies the server instance. This property is required for all connections. Valid values include the network name or IP address of the server, local or localhost for local connections, a URL if the server is configured for HTTP or HTTPS access, or the name of a local cube (.cub) file. 

Valid value for Azure Analysis Services, `<protocol>://<region>/<servername>` where protocol is string asazure, region is the Uri where the server was created (for example, westus.asazure.windows.net) and servername is the name of your unique server within the region.

Valid value for Power BI Premium, `powerbi://api.powerbi.com/v1.0/[tenant name]/[workspace name]` where protocol is string powerbi, Uri is api.powerbi.com, tenant name is the origanization tenant name or myorg, and workspace name is the name of a workspace assigned to a dedicated capacity.|`Data source=asazure://westus.asazure.windows.net/myasserver` for Azure Analysis Services.

#### Example

`powerbi://api.powerbi.com/v1.0/contoso.com/Sales Workspace` for a Power BI Premium workspace.

`Data source=AW-SRV01` for the default instance and port (TCP 2383).

`Data source=AW-SRV01$Finance:8081` for a named instance ($Finance) and fixed port.

`Data source=AW-SRV01.corp.Adventure-Works.com` for a fully qualified domain name, assuming the default instance and port.

`Data source=172.16.254.1` for an IP address of the server, bypassing DNS server lookup, useful for troubleshooting connection problems.


### Initial Catalog or Catalog

#### Applies to

Azure AS, SSAS, Power BI

#### Description

Specifies the name of the Analysis Services database or Power BI Premium dataset to connect to. The database must be deployed on Analysis Services or a Power BI Premium workspace, and you must have permission to connect to it. This property is optional for AMO connections, but required for ADOMD.NET.

#### Example

`Initial catalog=AdventureWorks`

### Provider

#### Applies to

Azure AS, SSAS, Power BI

#### Description

This property is **optional**. By default, the client libraries read the current version of the OLE DB provider from the registry. 

Set this property only if a specific version of the data provider is required. Valid values include MSOLAP.\<version>, where \<version> is either 4, 5, 6 or 7.For example, MSOLAP.7 released in SQL Server 2016.

#### Example

`Provider=MSOLAP.7` is used for connections that require the SQL Server 2016 version of the OLE DB provider for Analysis Services.

### Cube

#### Applies to

Azure AS, SSAS, Power BI

#### Description

Cube name or perspective name. A database can contain multiple cubes and perspectives. When multiple targets are possible, include the cube or perspective name on the connection string.

#### Example

`Cube=SalesPerspective` shows that you can use the Cube connection string property to specify either the name of a cube or the name of a perspective.

  
## Authentication and security properties

 Azure Analysis Services and Power BI Premium use Integrated Azure Active Directory authentication (recommended), Azure Active Directory authentication with username and password, or Windows authentication.

 SQL Server Analysis Services uses Windows authentication only, but you can set properties on the connection string to pass in a specific user name and password.  
  
 Properties are listed in alphabetical order.  

### EffectiveUserName

#### Applies to

SSAS

#### Description

Use when an end user identity must be impersonated on the server. Specify the account in a domain\user format. To use this property, the caller must have administrative permissions in Analysis Services. For more information about using this property in an Excel workbook from SharePoint, see [Use Analysis Services EffectiveUserName in SharePoint Server 2013](https://go.microsoft.com/fwlink/?LinkId=311905).

**EffectiveUserName** is used in a [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint installation to capture usage information. The user identity is provided to the server so that events or errors that include user identity can be recorded in the log files. In the case of [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], it is not used for authorization purposes.

### Encrypt Password

#### Applies to

SSAS

#### Description

Specifies whether a local password is to be used to encrypt local cubes. Valid values are True or False. The default is False.

###

#### Applies to

#### Description


###

#### Applies to

#### Description


###

#### Applies to

#### Description


###

#### Applies to

#### Description





|Property|Description|  
|--------------|-----------------|
|**EffectiveUserName**|Applies to: SSAS.<br /><br /> Use when an end user identity must be impersonated on the server. Specify the account in a domain\user format. To use this property, the caller must have administrative permissions in Analysis Services. For more information about using this property in an Excel workbook from SharePoint, see [Use Analysis Services EffectiveUserName in SharePoint Server 2013](https://go.microsoft.com/fwlink/?LinkId=311905).<br /><br /> **EffectiveUserName** is used in a [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint installation to capture usage information. The user identity is provided to the server so that events or errors that include user identity can be recorded in the log files. In the case of [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], it is not used for authorization purposes.|  
|**Encrypt Password**|Applies to: SSAS.<br /><br /> Specifies whether a local password is to be used to encrypt local cubes. Valid values are True or False. The default is False.|  
|**Encryption Password**|Applies to: SSAS.<br /><br /> The password used to decrypt an encrypted local cube. Default value is empty. This value must be explicitly set by the user.|  
|**Impersonation Level**|Applies to: SSAS.<br /><br /> Indicates the level of impersonation that the server is allowed to use when impersonating the client. Valid values include:<br /><br /> -   Anonymous. The client is anonymous to the server. The server process cannot obtain information about the client, nor can the client be impersonated.<br />-   Identify. The server process can get the client identity. The server can impersonate the client identity for authorization purposes but cannot access system objects as the client.<br />-   Impersonate. This is the default value. The client identity can be impersonated, but only when the connection is established, and not on every call.<br />-   Delegate. The server process can impersonate the client security context while acting on behalf of the client. The server process can also make outgoing calls to other servers while acting on behalf of the client.|  
|**Integrated Security**|Applies to: Azure AS, SSAS, Power BI.<br /><br /> The Windows identity of the caller is used to connect to Analysis Services. Valid values are blank, SSPI, and BASIC.<br /><br /> **Integrated Security**=**SSPI** is the default value for TCP connections, allowing NTLM, Kerberos, or Anonymous authentication. Blank is the default value for HTTP connections.<br /><br /> When using **SSPI**, **ProtectionLevel** must be set to one of the following: **Connect**, **PktIntegrity**, **PktPrivacy**.|  
|**Persist Encrypted**|Applies to: Azure AS, SSAS, Power BI.<br /><br /> Set this property when the client application requires the data source object to persist sensitive authentication information, such as a password, in encrypted form. By default, authentication information is not persisted.|  
|**Persist Security Info**|Applies to: Azure AS, SSAS, Power BI.<br /><br /> Valid values are True and False. When set to True, security information, such as the user identity or password previously specified on the connection string, can be obtained from the connection after the connection is made. The default value is False.|  
|**Protection Level**|Applies to: SSAS.<br /><br /> Determines the security level used on the connection. Valid values are:<br /><br /> -   **None**. Unauthenticated or anonymous connections. Performs no authentication on data sent to the server.<br />-   **Connect**. Authenticated connections. Authenticates only when the client establishes a relationship with a server.<br />-   **Pkt Integrity**. Encrypted connections. Verifies that all data is received from the client and that it has not been changed in transit.<br />-   **Pkt Privacy**. Signed encryption, supported only for XMLA. Verifies that all data is received from the client, that it has not been changed in transit, and protects the privacy of the data by encrypting it.<br /><br /> For more information, see [Establishing Secure Connections in ADOMD.NET](https://docs.microsoft.com/analysis-services/adomd/multidimensional-models-adomd-net-client/connections-in-adomd-net-establishing-secure-connections)|  
|**Roles**|Applies to: Azure AS, SSAS.<br /><br /> Specify a comma-delimited list of predefined roles to connect to a server or database using permissions conveyed by that role. If this property is omitted, all roles are used, and the effective permissions are the combination of all roles. Setting the property to an empty value (for example, Roles=' ') the client connection has no role membership.<br /><br /> An administrator using this property connects using the permissions conveyed by the role. Some commands might fail if the role does not provide sufficient permission.|  
|**SSPI**|Applies to: Azure AS, SSAS, Power BI.<br /><br /> Explicitly specifies which security package to use for client authentication when **Integrated Security** is set to **SSPI**. SSPI supports multiple packages, but you can use this property to specify a particular package. Valid values are Negotiate, Kerberos, NTLM, and Anonymous User. If this property is not set, all packages will be available to the connection.|  
|**Use Encryption for Data**|Applies to: Azure AS, SSAS, Power BI.<br /><br /> Encrypts data transmissions. Value values are True and False.|  
|**User ID**=...; **Password**=|Applies to: Azure AS, SSAS, Power BI.<br /><br /> **User ID** and **Password** are used together. Analysis Services impersonates the user identity specified through these credentials. On an Analysis Services connection, putting credentials on the command line is used only when the server is configured for HTTP access, and you specified Basic authentication instead of integrated security on the IIS virtual directory. When connecting directly to the server, **UserID** and **Password** connection string params are ignored and the connection is made using the context of the logged on user. <br /><br />The user name and password must be the credentials of a Windows identity, either a local or a domain user account. Notice that **User ID** has an embedded space. Other aliases for this property include **UserName** (no space), and **UID**. Alias for **Password** is **PWD**.|

::: moniker range="asallproducts-allversions || >= sql-analysis-services-2016"

## Special purpose properties

 These properties are used to ensure specific connection behaviors required by an application.

 Properties are listed in alphabetical order.  

|Property|Description|  
|--------------|-----------------|
|**Application Name**|Applies to: SSAS.<br /><br /> Sets the name of the application associated with the connection. This value can be useful when monitoring tracing events, especially when you have several applications accessing the same databases. For example, adding Application Name='test' to a connection string causes 'test' to appear in a SQL Server Profiler trace, as shown in the following screenshot:<br /><br /> ![SSAS_AppNameExcample](../../analysis-services/instances/media/ssas-appnameexcample.gif "SSAS_AppNameExcample")<br /><br /> Aliases for this property include **sspropinitAppName**, **AppName**. For more information, see [Application Name for SQL Server Connections](https://www.connectionstrings.com/use-application-name-sql-server/).|  
|**AutoSyncPeriod**|Applies to: SSAS.<br /><br /> Sets the frequency (in milliseconds) of client and server cache synchronization. ADOMD.NET provides client caching for frequently used objects that have minimal memory overhead. This helps reduce the number of round trips to the server. The default is 10000 milliseconds (or 10 seconds). When set to null or 0, automatic synchronization is turned off.|  
|**Character Encoding**|Applies to: SSAS.<br /><br /> Defines how characters are encoded on the request. Valid values are Default or UTF-8 (these are equivalent), and UTF-16| 
|**CommitTimeout**|Applies to: SSAS.<br /><br /> An XMLA property. Determines how long, in milliseconds, the commit phase of a currently running command waits before rolling back. When greater than 0, overrides the value of the corresponding CommitTimeout property in the server configuration. |   
|**CompareCaseSensitiveStringFlags**|Applies to: SSAS.<br /><br /> Adjusts case-sensitive string comparisons for a specified locale.|  
|**Compression Level**|Applies to: SSAS.<br /><br /> If **TransportCompression** is XPRESS, you can set the compression level to control how much compression is used. Valid values are 0 through 9, with 0 having least compression, and 9 having the most compression. Increased compression slows performance. The default value is 0.|  
|**Connect Timeout**|Applies to: SSAS.<br /><br /> Determines the maximum amount of time (in seconds) the client attempts a connection before timing out. If a connection does not succeed within this period, the client quits trying to connect and generates an error.|  
|**DbpropMsmdRequestMemoryLimit**|Applies to: SSAS.<br /><br /> This property overrides the [Memory\QueryMemoryLimit](../server-properties/memory-properties.md) server property value for a connection. Specified in kilobytes. |
|**MDX Compatibility**|Applies to: SSAS.<br /><br /> The purpose of this property is to ensure a consistent set of MDX behaviors for applications that issue MDX queries. Excel, which uses MDX queries to populate and calculate a PivotTable connected to Analysis Services, sets this property to 1, to ensure that placeholder members in ragged hierarchies are visible in a PivotTable. Valid values include 0, 1, 2.<br /><br /> 0 and 1 expose placeholder members; 2 does not. If this is empty, 0 is assumed.|  
|**MDX Missing Member Mode=Error**|Applies to: SSAS.<br /><br /> Indicates whether missing members are ignored in MDX statements. Valid values are Default, Error, and Ignore. Default uses a server-defined value. Error generates an error when a member does not exist. Ignore specifies that missing values should be ignored.|  
|**Optimize Response**|Applies to: SSAS.<br /><br /> A bitmask indicating which of the following query response optimizations are enabled.<br /><br /> -   0x01 Use the NormalTupleSet (this is the default)<br />-   0x02 Use when slicers are empty|  
|**Packet Size**|Applies to: SSAS.<br /><br /> A network packet size (in bytes) between 512 and 32,767. The default network packet size is 4096.|  
|**Protocol Format**|Applies to: SSAS.<br /><br /> Sets the format of the XML sent to the server. Valid values are Default, XML, or Binary. The protocol is XMLA. You can specify that the XML be sent in compressed form (this is the default), as raw XML, or in a binary format. Binary format encodes XML elements and attributes, making them smaller. Compression is a proprietary format that further reduces the size of requests and responses. Compression and binary formats are used to speed up data transfer requests and responses.<br /><br /> You must use a client library on the connection if using binary or compressed format. OLE DB provider can format requests and responses in binary or compressed format. AMO and ADOMD.NET format the requests as Text, but accept responses in binary or compressed format.<br /><br /> This connection string property is equivalent to the **EnableBinaryXML** and **EnableCompression** server configuration settings.|  
|**Real Time Olap**|Applies to: SSAS.<br /><br /> Set this property to bypass caching, causing all partitions to actively listen for query notifications. By default, this property is not set.|  
|**Safety Options**|Applies to: SSAS.<br /><br /> Sets the safety level for user-defined functions and actions. Valid values are 0, 1, 2. In an Excel connection this property is Safety Options=2. Details about this option can be found in <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>.|  
|**SQLQueryMode**|Applies to: SSAS.<br /><br /> Specifies whether SQL queries include calculations. Valid values are Data, Calculated, IncludeEmpty. Data means that no calculations are allowed. Calculated allows calculations. IncludeEmpty allows calculations and empty rows to be returned in the query result.|  
|**Timeout**|Applies to: SSAS.<br /><br /> Specifies how long (in seconds) the client library waits for a command to complete before generating an error.|  
|**Transport Compression**|Applies to: SSAS.<br /><br /> Defines how client and server communications are compressed, when compression is specified via the **Protocol Format** property. Valid values are Default, None, Compressed and **gzip**. Default is no compression for TCP, or **gzip** for HTTP. None indicates that no compression is used. Compressed uses XPRESS compression. **gzip** is only valid for HTTP connections, where the HTTP request includes Accept-Encoding=gzip.|  
|**UseExistingFile**|Applies to: SSAS.<br /><br /> Used when connecting to a local cube. This property specifies whether the local cube is overwritten. Valid values are True or False. If set to True, the cube file must exist. The existing file will be the target of the connection. If set to False, the cube file is overwritten.|  
|**VisualMode**|Applies to: SSAS.<br /><br /> Set this property to control how members are aggregated when dimension security is applied.<br /><br /> For cube data that everyone is allowed to see, aggregating all of the members makes sense because all of the values that contribute to the total are visible. However, if you filter or restrict dimensions based on user identity, showing a total based on all the members (combining both restricted and allowed values into a single total) might be confusing or show more information than should be revealed.<br /><br /> To specify how members are aggregated when dimension security is applied, you can set this property to True to use only allowed values in the aggregation, or False to exclude restricted values from the total.<br /><br /> When set on the connection string, this value applies to the cube or perspective level. Within a model, you can control visual totals at a more granular level.<br /><br /> Valid values are 0, 1, and 2.<br /><br /> -   0 is the default. Currently, the default behavior is equivalent to 2, where aggregations include values that are hidden from the user.<br />-   1 excludes hidden values from the total. This is the default for Excel.<br />-   2 includes hidden values in the total. This is the default value on the server.<br /><br /> Aliases for this property include **Visual Total** or **Default MDX Visual Mode**.|  

::: moniker-end
  
## See also

[Connecting to Azure Analysis Services servers](https://docs.microsoft.com/azure/analysis-services/analysis-services-connect)   
[Power BI dataset connectivity with the XMLA endpoint](https://docs.microsoft.com/power-bi/service-premium-connect-tools)