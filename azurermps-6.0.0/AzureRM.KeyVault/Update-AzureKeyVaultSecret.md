---
external_help_file: Microsoft.Azure.Commands.KeyVault.dll-Help.xml
Module_Name: AzureRM.KeyVault
online_version: https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/update-azurekeyvaultsecret
schema: 2.0.0
content_git_url: https://github.com/Azure/azure-powershell/blob/preview/src/ResourceManager/KeyVault/Commands.KeyVault/help/Update-AzureKeyVaultSecret.md
original_content_git_url: https://github.com/Azure/azure-powershell/blob/preview/src/ResourceManager/KeyVault/Commands.KeyVault/help/Update-AzureKeyVaultSecret.md
---

# Update-AzureKeyVaultSecret

## SYNOPSIS
Updates attributes of a secret in a key vault.

## SYNTAX

### Default (Default)
```
Update-AzureKeyVaultSecret [-VaultName] <String> [-Name] <String> [[-Version] <String>] [-Enable <Boolean>]
 [-Expires <DateTime>] [-NotBefore <DateTime>] [-ContentType <String>] [-Tag <Hashtable>] [-PassThru]
 [-DefaultProfile <IAzureContextContainer>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### InputObject
```
Update-AzureKeyVaultSecret [-InputObject] <PSKeyVaultSecretIdentityItem> [[-Version] <String>]
 [-Enable <Boolean>] [-Expires <DateTime>] [-NotBefore <DateTime>] [-ContentType <String>] [-Tag <Hashtable>]
 [-PassThru] [-DefaultProfile <IAzureContextContainer>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION
The **Update-AzureKeyVaultSecret** cmdlet updates editable attributes of a secret in a key vault.

## EXAMPLES

### Example 1: Modify the attributes of a secret
```
PS C:\> $Expires = (Get-Date).AddYears(2).ToUniversalTime()
PS C:\> $Nbf = (Get-Date).ToUniversalTime()
PS C:\> $Tags = @{ 'Severity' = 'medium'; 'HR' = null}
PS C:\> $ContentType= 'xml'
PS C:\> Update-AzureKeyVaultSecret -VaultName 'ContosoVault' -Name 'HR' -Expires $Expires -NotBefore $Nbf -ContentType $ContentType -Enable $True -Tag $Tags -PassThru
```

The first four commands define attributes for the expiry date, the NotBefore date, tags, and
context type, and store the attributes in variables.

The final command modifies the attributes for the secret named HR in the key vault named
ContosoVault, using the stored variables.

### Example 2: Delete the tags and content type for a secret
```
PS C:\> Update-AzureKeyVaultSecret -VaultName 'ContosoVault' -Name 'HR' -Version '9EEA45C6EE50490B9C3176A80AC1A0DF' -ContentType '' -Tag -@{}
```

This command deletes the tags and the content type for the specified version of the secret named HR
in the key vault named Contoso.

### Example 3: Disable the current version of secrets whose name begins with IT
```
PS C:\> $Vault = 'ContosoVault'
PS C:\> $Prefix = 'IT'
PS C:\> Get-AzureKeyVaultSecret $Vault | Where-Object {$_.Name -like $Prefix + '*'} | Update-AzureKeyVaultSecret -Enable $False
```

The first command stores the string value Contoso in the $Vault variable.

The second command stores the string value IT in the $Prefix variable.

The third command uses the Get-AzureKeyVaultSecret cmdlet to get the secrets in the specified key
vault, and then passes those secrets to the **Where-Object** cmdlet. The **Where-Object** cmdlet
filters the secrets for names that begin with the characters IT. The command pipes the secrets that
match the filter to the Update-AzureKeyVaultSecret cmdlet, which disables them.

### Example 4: Set the ContentType for all versions of a secret
```
PS C:\> $VaultName = 'ContosoVault'
PS C:\> $Name = 'HR'
PS C:\> $ContentType = 'xml'
PS C:\> Get-AzureKeyVaultKey -VaultName $VaultName -Name $Name -IncludeVersions | Update-AzureKeyVaultSecret -ContentType $ContentType
```

The first three commands define string variables to use for the *VaultName*, *Name*, and
*ContentType* parameters. The fourth command uses the Get-AzureKeyVaultKey cmdlet to get the
specified keys, and pipes the keys to the Update-AzureKeyVaultSecret cmdlet to set their
content type to XML.

## PARAMETERS

### -ContentType
Secret's content type.
If not specified, the existing value of the secret's content type remains unchanged.
Remove the existing content type value by specifying an empty string.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -DefaultProfile
The credentials, account, tenant, and subscription used for communication with Azure.

```yaml
Type: IAzureContextContainer
Parameter Sets: (All)
Aliases: AzureRmContext, AzureCredential

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Enable
If present, enable a secret if value is true.
Disable a secret if value is false.
If not specified, the existing value of the secret's enabled/disabled state remains unchanged.

```yaml
Type: Boolean
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Expires
The expiration time of a secret in UTC time.
If not specified, the existing value of the secret's expiration time remains unchanged.

```yaml
Type: DateTime
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -InputObject
Secret object

```yaml
Type: PSKeyVaultSecretIdentityItem
Parameter Sets: InputObject
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Name
Secret name.
Cmdlet constructs the FQDN of a secret from vault name, currently selected environment and secret name.

```yaml
Type: String
Parameter Sets: Default
Aliases: SecretName

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -NotBefore
The UTC time before which secret can't be used.
If not specified, the existing value of the secret's NotBefore attribute remains unchanged.

```yaml
Type: DateTime
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -PassThru
Cmdlet does not return object by default.
If this switch is specified, return Secret object.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Tag
A hashtable representing secret tags.
If not specified, the existing tags of the secret remain unchanged.
Remove a tag by specifying an empty Hashtable.

```yaml
Type: Hashtable
Parameter Sets: (All)
Aliases: Tags

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VaultName
Vault name.
Cmdlet constructs the FQDN of a vault based on the name and currently selected environment.

```yaml
Type: String
Parameter Sets: Default
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Version
Secret version.
Cmdlet constructs the FQDN of a secret from vault name, currently selected environment, secret name and secret version.

```yaml
Type: String
Parameter Sets: (All)
Aliases: SecretVersion

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Confirm
Prompts you for confirmation before running the cmdlet.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf
Shows what would happen if the cmdlet runs.
The cmdlet is not run.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### Microsoft.Azure.Commands.KeyVault.Models.PSKeyVaultSecretIdentityItem

## OUTPUTS

### Microsoft.Azure.Commands.KeyVault.Models.PSKeyVaultSecret

## NOTES

## RELATED LINKS
