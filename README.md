# azure-rg-vnet

# Clone the repo

cd ~/azure-rg-vnet

# 1. Build

```
az bicep build \
  --file modules/main.bicep
```

# 2. Validate

```
az deployment sub validate \
  --location centralus \
  --template-file modules/main.bicep \
  --parameters environments/dev.bicepparam
```

# 3. What-If

```
az deployment sub what-if \
  --location centralus \
  --template-file modules/main.bicep \
  --parameters environments/dev.bicepparam
```
# 4. Deploy

```
az deployment sub create \
  --location centralus \
  --template-file modules/main.bicep \
  --parameters environments/dev.bicepparam
```

# Verify Template 1

```
# Resource Group
az group show \
  --name rg-sql-ag-dev \
  --output table
```

# VNet

```
az network vnet show \
  --resource-group rg-sql-ag-dev \
  --name vnet-sql-ag-dev \
  --query "{Name:name,Location:location,AddressSpace:addressSpace.addressPrefixes}" \
  --output table

# Subnets
az network vnet subnet list \
  --resource-group rg-sql-ag-dev \
  --vnet-name vnet-sql-ag-dev \
  --query "[].{Name:name,Prefix:addressPrefix}" \
  --output table
```


