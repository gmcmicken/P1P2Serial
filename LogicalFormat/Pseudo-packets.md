# Pseudo-packet data format

Packet types 08-0F have not been observed on the P1/P2 bus. These packet types are additionally generated by P1P2Monitor and P1P2-bridge-esp8266/P1P2MQTT to add internal state information in the raw encoded data.

When these packet types are decoded, they may generate MQTT parameter output including WiFi signal strengh, uptimes, free memory information, etcetera.

Please [read me](README.md) first for the general format description.

## Packet types 08 - 0C

Pseudo packets 08 and 0C may be used in future for additional pseudo-packets.

Pseudo packets 09-0B are used by the ESP01 when MQTT_INPUT_BINDATA or MQTT_INPUT_HEXDATA is being used instead of 0D-0F.

## Packet type 0D

### Packet type 0D generated by P1P2Monitor

Header: 00000D

| Byte      | Hex value          | Description                          | Data type
|:----------|:-------------------|:-------------------------------------|:-
| 0-19      | 00                 | Reserved                             |

### Packet type 0D generated by P1P2-bridge-esp8266/P1P2MQTT

Header: 40000D

| Byte      | Hex value          | Description                          | Data type
|:----------|:-------------------|:-------------------------------------|:-
| 0         | XX                 | ESP_Compile_Options                  | u8
| 1-2       | XX XX              | MQTT_messages_skipped_not_connected  | u16
| 3-6       | XX XX XX XX        | MQTT_messages_published              | u32
| 7-8       | XX XX              | MQTT_disconnected_time               | u16
| 9         | XX                 | WiFi_RSSI                            | s8
| 10        | XX                 | WiFi_status                          | u8
| 11-19     | 00                 | Reserved                             |

## Packet type 0E

### Packet type 0E generated by P1P2Monitor

Header: 00000E

| Byte      | Hex value          | Description                          | Data type
|:----------|:-------------------|:-------------------------------------|:-
| 0-3       | XX XX XX XX        | ATmega_Uptime                        | u32
| 4-7       | XX XX XX XX        | CPU_Frequency                        | u32
| 8         | XX                 | Writes_Refused                       | u8
| 9         | XX                 | Counter_Request_Repeat               | u8
| 10        | XX                 | Counter_Request_Counter              | u8
| 11        | XX                 | Error_Oversized_Packet_Count         | u8
| 12        | XX                 | Parameter_Write_Request              | u8
| 13        | XX                 | Parameter_Write_Packet_Type          | u8
| 14-15     | XX XX              | Parameter_Write_Nr                   | u16
| 16-19     | XX XX XX XX        | Parameter_Write_Value                | u32

### Packet type 0E generated by P1P2-bridge-esp8266/P1P2MQTT

Header: 40000E

| Byte      | Hex value          | Description                          | Data type
|:----------|:-------------------|:-------------------------------------|:-
| 0-3       | XX XX XX XX        | ESP_Uptime                           | u32
| 4-7       | XX XX XX XX        | MQTT_Acknowledged                    | u32
| 8-11      | XX XX XX XX        | MQTT_Gaps                            | u32
| 12-13     | XX XX              | MQTT_Min_Memory_Size                 | u16
| 14-15     | XX XX              | ESP_Output_Mode                      | u16
| 16-19     | XX XX XX XX        | ESP_Max_Loop_Time                    | u32

## Packet type 0F

### Packet type 0F generated by P1P2Monitor

Header: 00000F

| Byte      | Hex value          | Description                          | Data type
|:----------|:-------------------|:-------------------------------------|:-
| 0         | XX                 | Compile_Options_ATmega               | u8
| 1         | XX                 | Verbose                              | u8
| 2         | XX                 | Reboot_MCUSR                         | u8
| 3         | XX                 | Write_Budget                         | u8
| 4         | XX                 | Error_Budget                         | u8
| 5-6       | XX XX              | Counter_Parameter_Writes");          | u16
| 7-8       | XX XX              | Delay_Packet_Write                   | u16
| 9-10      | XX XX              | Delay_Packet_Write_Timeout           | u16
| 11        | 00                 | Reserved                             |
| 12        | XX                 | Control_ID_EEPROM                    | u8
| 13        | XX                 | Verbose_EEPROM                       | u8
| 14        | XX                 | Counter_Request_Repeat_EEPROM        | u8
| 15        | XX                 | EEPROM_Signature_Match               | u8
| 16        | 00                 | Reserved                             |
| 17        | XX                 | Error_Read_Count                     | u8
| 18        | XX                 | Error_Read_Type                      | u8
| 19        | XX                 | Control_ID                           | u8

### Packet type 0F generated by P1P2-bridge-esp8266/P1P2MQTT

Header: 40000F

| Byte      | Hex value          | Description                          | Data type
|:----------|:-------------------|:-------------------------------------|:-
| 0         | XX                 | ESP_telnet_connected                 | u8
| 1         | XX                 | ESP_Output_Filter                    | u8
| 2-3       | XX XX              | ESP_Mem_free                         | u16
| 4-5       | XX XX              | MQTT_disconnected_time_total         | u16
| 6-7       | XX XX              | Sprint_buffer_overflow               | u16
| 8         | XX                 | ESP_serial_input_Errors_Data_Short   | u8
| 9         | XX                 | ESP_serial_input_Errors_CRC          | u8
| 10-13     | XX XX XX XX        | MQTT_Wait_Counter                    | u32
| 14-15     | XX XX              | MQTT_disconnects                     | u16
| 16-17     | XX XX              | MQTT_disconnected_skipped_packets    | u16
| 18-19     | XX XX              | MQTT_messages_skipped_low_mem        | u16