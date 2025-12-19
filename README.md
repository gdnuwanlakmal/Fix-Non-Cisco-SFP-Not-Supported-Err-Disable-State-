<img width="340" height="340" alt="image" src="https://github.com/user-attachments/assets/b824638f-097f-4714-b5da-a024099431a4" />



# Fix: Non-Cisco SFP Not Supported (Err-Disable State)
Cisco switches may place an interface into an err-disable state when a non-Cisco SFP module is detected. This behavior is enforced by default to ensure hardware compatibility. This repository documents the issue and provides steps to recover and allow third-party SFP transceivers.
### Problem Description
When a non-Cisco SFP is inserted, the switch may display errors such as:

- %PHY-4-SFP_NOT_SUPPORTED
- Interface goes into err-disable state
- Link remains down even after reinserting the module

### Cause
Cisco IOS, by default, restricts the use of third-party SFP modules and disables the port to prevent unsupported hardware operation.

### Solution
You can recover the interface and allow third-party SFPs by enabling err-disable recovery and unsupported transceiver support.
```shell
conf t
service unsupported-transceiver
errdisable recovery cause gbic-invalid
errdisable recovery interval 30
end
write memory
```
⚠️ Warning: Using unsupported transceivers may affect warranty or TAC support.

### Apply Changes
After completing the configuration:

1. Unplug the SFP module
2. Wait 1 minute
3. Reinsert the SFP module

This allows the switch to re-detect the transceiver and bring the interface out of the err-disable state.

### Verification

Check interface and SFP status:
```shell
show interface status
show inventory
show errdisable recovery
```
### - Disclaimer
### This information is provided for educational purposes. Always test changes in a lab environment before applying them in production.
