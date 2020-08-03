
# Admin Only NSG Template

### Implemented NSG Rules
| NSG Rule  | Ports Exposed   | Remarks |
| ------------ | ------------ | ------------ |
|  AppgatewayPorts | 65200-65535   |  Managed by GatewayManager.<br/> sourceAddressPrefix: GatewayManager. destinationAddressPrefix: *  <br/>|
|  WebLogicAdminPorts |  7001,7002 |  Default access to only subnet. sourceAddressPrefix : 10.0.0.0/24.  DestinationAddressPrefix: \*. <br/> Adding public ip to sourceAddressPrefix will give access |
|  AppGatewayHTTPSPort | 80,443  | All public access </br> sourceAddressPrefix : \*</br> destinationAddressPrefix: \*</br>  |

### Test Scenarios
•	NSG Rule 105 – Needs to be removed 7001 port from deny
•	For t3 access, need to try without VPN

| Sl.No   |  Scenario  | Expected   | Result   |
| ------------ | ------------ | ------------ | ------------ |
|  1  |  Accessing admin console. </br> Default NSG rule. | Access denied. Connection timed out  |  :tw-2705: |
|  2  |Accessing admin console </br> Default NSG rule + public ip entry   | Admin console should be accessible   |  :tw-2705:  |
|  3 | Accessing T3 connection to admin server</br> Default NSG rule  | Unreachable   |   :tw-2705: |
|  4 | Accessing T3 connection to admin server</br> Default NSG rule  + public ip entry  | Accessible   |   :tw-2705: |


