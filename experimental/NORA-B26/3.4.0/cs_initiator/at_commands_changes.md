# AT Commands Changes: cs_initiator variant vs standard

This document shows the differences between the **standard** build (u-connectXpress 3.4.0 for NORA-B26) and the **cs_initiator** variant (u-connectXpress 3.4.0 for NORA-B26).

## Summary

- **Added commands:** 5
- **Removed commands:** 0
- **Renamed commands:** 0
- **Modified commands:** 1


## ✅ Added Events

#### Channel Sounding

- **+UEBTCSIQ:\<conn_handle\>,\<antenna\>,\<valid_channels\>{binary_data}** - Event Bluetooth Channel Sounding Combined PCT Data


## ✅ Added Commands

#### Channel Sounding

- **AT+UBTCSIQ** - Bluetooth Channel Sounding PCT Reporting
- **AT+UBTCSP** - Bluetooth Channel Sounding Procedure
- **AT+UBTCSREF** - Bluetooth Channel Sounding Reference PCT Preset
- **AT+UBTCSRT** - Bluetooth Channel Sounding Update Rate


## 🔄 Modified Commands

#### Channel Sounding

### AT+UBTCSM - Bluetooth Channel Sounding Mode

Set Channel Sounding mode (disable, reflector).

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTCSM=<channel_sounding_mode>` | Writes the Channel Sounding mode.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTCSM?` | Read current Channel Sounding mode. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTCSM:<channel_sounding_mode>` | Successful read response for AT+UBTCSM? |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| channel\_sounding\_mode | enumerator | Valid values:<br>0: Disable Channel Sounding.<br>1: Enable Channel Sounding as ~~reflector.~~ **reflector.<br>2: Enable Channel Sounding as initiator.**<br><br>Default value: 0 |

