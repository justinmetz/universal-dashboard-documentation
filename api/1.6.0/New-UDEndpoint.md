---
external help file: PowerShellProTools.UniversalDashboard.dll-Help.xml
Module Name: UniversalDashboard
online version: 
schema: 2.0.0
---

# New-UDEndpoint

## SYNOPSIS
Creates a new REST API endpoint.

## SYNTAX

```
New-UDEndpoint -Endpoint <ScriptBlock> -Url <String> [-Method <String>] [<CommonParameters>]
```

## DESCRIPTION
Creates a new REST API endpoint. This can be used with Start-UDDashboard and Start-UDRestApi. All URLs are automatically prefixed with /api.

## EXAMPLES

### Example 1
```
PS C:\> New-UDEndpoint -Url "user" -Method "GET" -Endpoint {
	@("Adam", "Sarah", "Bill") | ConvertTo-Json
}
```

Creates a new REST API endpoint with a URL of "/api/user" that returns Adam, Sarah and Bill as a JSON array. 

### Example 2
```
PS C:\> New-UDEndpoint -Url "/process/:id" -Method "DELETE" -Endpoint {
	param($id)

	Stop-Process -Id $Id
}
```

Creates a REST API endpoint that stops the process with the ID specified in the URL. You could invoke this endpoint by calling /api/process/1234.

### Example 3
```
PS C:\> $Endpoint = New-UDEndpoint -Url "/process" -Method "POST" -Endpoint {
	param($Name)

	Start-Process -FilePath $Name
}
PS C:\> Start-UDRestApi -Endpoint $Endpoint
PS C:\> Invoke-RestMethod -Uri http://localhost:80/api/process -Body @{Name = "code.exe"} -Method POST
```

Creates a REST API endpoint that accepts a HTTP POST with a name parameter in the body. Then it starts the server and invokes the endpoint with Invoke-RestMethod.

## PARAMETERS

### -Endpoint
The script block endpoint that is invoked when the URL is called. This script block can provide a param block with arguments that will be passed in from the URL or the body of the request.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases: 

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Method
The HTTP method for this endpoint.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 
Accepted values: GET, POST, DELETE, PUT

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Url
The URL for this endpoint. All URLs are automatically prefixed with "/api/". Any portion of the URL that starts with a colon ":", will be treated as a varied and can be accessed in the endpoint script block.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None

## OUTPUTS

### System.Object

## NOTES

## RELATED LINKS

