# NSG Rules Implementation for Weblogic on Azure
## WebLogic Admin Only NSG Template

### Implemented NSG Rules
| NSG Rule  | Ports Exposed   | Remarks |
| ------------ | ------------ | ------------ |
|  AppgatewayPorts | 65200-65535   |  Managed by GatewayManager.<br/> sourceAddressPrefix: GatewayManager. destinationAddressPrefix: *  <br/>|
|  WebLogicAdminPorts |  7001,7002 |  Default access to only subnet. sourceAddressPrefix : 10.0.0.0/24.  DestinationAddressPrefix: \*. <br/> Adding public ip to sourceAddressPrefix will give access |
|  AppGatewayHTTPSPort | 80,443  | All public access </br> sourceAddressPrefix : \*</br> destinationAddressPrefix: \*</br>  |

### Test Scenarios
•	NSG Rule 105 – Needs to be removed 7001 port from deny </br>
•	For t3 access, need to try without VPN

| Sl.No   |  Scenario  | Expected   | Result   |
| ------------ | ------------ | ------------ | ------------ |
|  1  |  Accessing admin console. </br> Default NSG rule. | Access denied. Connection timed out  |  :heavy_check_mark: |
|  2  |Accessing admin console </br> Default NSG rule + public ip entry   | Admin console should be accessible   |  :heavy_check_mark:  |
|  3 | Accessing T3 connection to admin server</br> Default NSG rule  | Unreachable   |   :heavy_check_mark: |
|  4 | Accessing T3 connection to admin server</br> Default NSG rule  + public ip entry  | Accessible   |   :heavy_check_mark: |

## WebLogic Static Cluster NSG Template

### Implemented NSG Rules
| NSG Rule  | Ports Exposed   | Remarks |
| ------------ | ------------ | ------------ |
|  AppgatewayPorts | 65200-65535   |  Managed by GatewayManager.<br/> sourceAddressPrefix: GatewayManager. destinationAddressPrefix: *  <br/>|
|  WebLogicAdminPorts |  7001,7002 |  Default access to only subnet. sourceAddressPrefix : 10.0.0.0/24.  DestinationAddressPrefix: \*. <br/> Adding public ip to sourceAddressPrefix will give access |
|  AppGatewayHTTPSPort | 80,443  | All public access </br> sourceAddressPrefix : \*</br> destinationAddressPrefix: \*</br>  |
|  WebLogicMSPorts | 8001  | Default access to only subnet. sourceAddressPrefix : 10.0.0.0/24.  DestinationAddressPrefix: \*. <br/> Adding public ip to sourceAddressPrefix will give access  |
|  WebLogicMSChannelPorts | 8501  | Default access to only subnet. sourceAddressPrefix : 10.0.0.0/24.  DestinationAddressPrefix: \*. <br/> Adding public ip to sourceAddressPrefix will give access  |



### Test Scenarios
•	NSG Rule 105 – Needs to be removed 7001 port from deny </br>
•	For t3 access, need to try without VPN

| Sl.No   |  Scenario  | Expected   | Result   |
| ------------ | ------------ | ------------ | ------------ |
|  1  |  Accessing admin console. </br> Default NSG rule. | Access denied. Connection timed out  |  :heavy_check_mark: |
|  2  |Accessing admin console </br> Default NSG rule + public ip entry   | Admin console should be accessible   |  :heavy_check_mark:  |
|  3 | Accessing T3 connection to admin server</br> Default NSG rule  | Unreachable   |   :heavy_check_mark: |
|  4 | Accessing T3 connection to admin server</br> Default NSG rule  + public ip entry  | Accessible   |   :heavy_check_mark: |
|  5 | Accessing deployed app through Appgateway </br> Default NSG rule  | Accessible   |   :heavy_check_mark: |
|  6 | Accessing managed server 8001 port using weblogic/ready /br> Default NSG rule   | Access denied   |   :heavy_check_mark: |
|  7 | Accessing managed server 8001 port using weblogic/ready /br> Default NSG rule + public ip entry   | Accessible   |   :heavy_check_mark: |
|  8 | Accessing T3 connection  to 8001 port <br> Default NSG rule    | Unreachable   |   :heavy_check_mark: |
|  9 | Accessing T3 connection  to 8001 port <br> Default NSG rule + public ip entry   | Accessible   |   :x: |



