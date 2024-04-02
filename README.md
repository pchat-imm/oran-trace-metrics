### General metrics showing 
description gNB: https://docs.srsran.com/projects/project/en/latest/user_manuals/source/console_ref.html \
and: https://docs.srsran.com/projects/4g/en/latest/usermanuals/source/srsenb/source/6_enb_commandref.html \
description UE: https://docs.srsran.com/projects/4g/en/latest/usermanuals/source/srsue/source/6_ue_commandref.html#ue-commandref 
wireshark: https://docs.srsran.com/projects/project/en/latest/user_manuals/source/outputs.html
grafana: https://docs.srsran.com/projects/project/en/latest/user_manuals/source/grafana_gui.html

to get log files check
```
# gnb
>> /tmp/gnb.log
>> /tmp/gnb_mac.pcap

# ue
>> /tmp/ue.log
>> /tmp/ue_metrics.csv
```

| metrics | full name | expected value | note |
|---|---|---|---|
|**pci**|[Physical Cell Identifier](https://www.sharetechnote.com/html/Handbook_LTE_PCI.html)| number|identification of a cell physical layer, determined bt PSS (Primary Sync Signal) and SSS (Secondary Sync Signal) |
|**mcs**|[Modulation and Coding Scheme](https://www.sharetechnote.com/html/5G/5G_MCS_TBS_CodeRate.html)| 0 (low target code rate) - 28 (high target code rate) | There are three tables |
|**brate**|Bitrate| bit/sec |
|**rsrp** |Reference Signal Receive Power | dBm |
|**snr**| [signal to noise ratio](https://www.sharetechnote.com/html/RF_Handbook_SNR.html) | dB |
|**ok**|Number of packet successfully sent| no. of pkg |
|**nok**|Number of packet dropped| no. of pkg |
|**(%)**|% of packets dropped| % |

 
## gNB
```
           -----------------DL-----------------------|------------------UL--------------------
 pci rnti  cqi  ri  mcs  brate   ok  nok  (%)  dl_bs | pusch  mcs  brate   ok  nok  (%)    bsr
   1 4601   15   1   27    17k   20    0   0%      0 |  65.5   27   107k   40    0   0%      0
   1 4601   15   1   27    19k   22    0   0%      0 |  65.5   27   112k   42    0   0%      0
   1 4601   15   1   27    17k   20    0   0%      0 |  65.5   26   112k   42    0   0%      0
   1 4601   15   1   27    17k   20    1   4%      0 |  65.5   27   107k   40    0   0%      0
```

### ----DL---- (gNB -> UE)
| metrics | full name | expected value | note |
|---|---|---|---|
|**rnti**|[Radio Network Temporary Identifier](https://www.sharetechnote.com/html/5G/5G_RNTI.html)| 0000-FFFF |UE identifier|
|**cqi**|[Channel Quality Indicator](https://www.sharetechnote.com/html/Handbook_LTE_CQI.html)|1 (poor) - 15 (best), 0 is out of range|reported by the UE. Main focus on different modulation |
|**ri**| [rank indicator](https://www.sharetechnote.com/html/Handbook_LTE_RI.html) | 1 (worst performance) or 2 (best performance) | reported from the UE showing how well multiple antenna work, 2 means no correlation/interference between the antenna, 1 means signal from two Tx Antenna perceived by UE to be like single signal from single antenna |
|**dl_bs**| ????? |

### ----UL---- (UE -> gNB)
| metrics | full name | expected value | note |
|---|---|---|---|
|**pusch**| PUSCH SINR (Signal-to-Interference-plus-Noise Ratio) | dB |
|**bsr**|[Buffer status report](https://www.sharetechnote.com/html/Handbook_LTE_BSR.html)| bytes |data waiting to be transmitted as reported by the UE |

## UE
```
---------Signal-----------|-----------------DL-----------------|-----------UL-----------
rat  pci  rsrp   pl   cfo | mcs  snr  iter  brate  bler  ta_us | mcs   buff  brate  bler
 nr    1    39    0 -6.0u |  26   65   1.0    16k    0%    0.0 |  26    0.0   109k    0%
 nr    1    39    0 -4.0u |  26   67   1.4    19k    0%    0.0 |  26    0.0   112k    0%
 nr    1    39    0  415n |  27   68   2.5    17k    0%    0.0 |  26     90   104k    0%
 nr    1    39    0 -2.0u |  27   66   2.3    18k    0%    0.0 |  26     90   111k    0%
```
### ----Signal----
| metrics | full name | expected value | note |
|---|---|---|---|
|**rat** |component carrier|lte or nr|
|**pl**| path loss | dB |
|**cfo**| Carrier Frequency Offset | Hz | mismatch carrier frequency between transmitted signal and recieved signal |

### ----DL----
| metrics | full name | expected value | note |
|---|---|---|---|
|**iter**| | Average number of turbo decider iterations |
|**bler**| block error rate | | rate of transmitted block/error recieved block) |
|**ta_us**| [timing advance](https://www.sharetechnote.com/html/Handbook_LTE_TimingAdvance.html) | microsec |

### ----UL----
| metrics | full name | expected value | note |
|---|---|---|---|
|**buff**| [uplink buffer status](https://www.sharetechnote.com/html/Handbook_LTE_BSR.html) | byte | data waiting to be transmitted |


<details>
  <summary>CQI table</summary>

  ### [CQI table](https://www.sharetechnote.com/html/5G/5G_CSI_Report.html)
  38.214 - Table 5.2.2.1-3: 4-bit CQI Table 2 \ 
  support 256 QAM - Target transport block error rate not exceed 0.1
  | CQI index | code rate x 1024 | modulation | efficiency |
  |---|---|---|---|
  | 0 |  | out of range |
  | 1 | 78 | QPSK | 0.1523 |
  | 2 | 193 | QPSK | 0.3770 |
  | 3 | 449 | QPSK | 0.8770 |
  | 4 | 378 | 16QAM | 1.4766 |
  | 5 | 490 | 16QAM | 1.9141 |
  | 6 | 616 | 16QAM | 2.4063 |
  | 7 | 466 | 64QAM | 2.7305 |
  | 8 | 567 | 64QAM | 3.3223 |
  | 9 | 666 | 64QAM | 3.9023 |
  | 10 | 772 | 64QAM | 4.5234 |
  | 11 | 873 | 64QAM | 5.1152 |
  | 12 | 711 | 256QAM | 5.5547 |
  | 13 | 797 | 256QAM | 6.2266 |
  | 14 | 885 | 256QAM | 6.9141 |
  | 15 | 948 | 256QAM | 7.4063 |
</details>

## Wireshark
following this link: https://docs.srsran.com/projects/project/en/latest/user_manuals/source/outputs.html

- add entry of DLT_User with specified protocol (edit->preference->protocols->DLT_user)
![Screenshot from 2024-04-02 13-55-27](https://github.com/pchat-imm/oran-trace-metrics/assets/40858099/d1b4341e-658f-46ec-b54f-8e5a82c43b86)

1. MAC PCAP
- enable on gnb config
![Screenshot from 2024-04-02 14-01-53](https://github.com/pchat-imm/oran-trace-metrics/assets/40858099/3737f4d7-9441-427f-b04a-4e97c5dc0129)
- enable MAC_NR protocol (analyze->enabled protocols->MAC_NR-> enable mac_nr_udp)
- edit preference of the protocol (edit->preference->protocols->MAC_NR => enable both "Attemtps to...", set LCID->DRB mapping to "From configuration protocol"
- see result in wireshark
![Screenshot from 2024-04-02 13-47-29](https://github.com/pchat-imm/oran-trace-metrics/assets/40858099/71662f1a-3abb-4bda-95b3-e088f00b781c)


## Grafana GUI
following this link: https://docs.srsran.com/projects/project/en/latest/user_manuals/source/grafana_gui.html

- add metrics in gnb config file
```
metrics:
    enable_json_metrics: true       # Enable reporting metrics in JSON format
    addr: 172.19.1.4                # Metrics-server IP
    port: 55555                     # Metrics-server Port
```
- launching GUI
```
sudo docker compose -f docker/docker-compose.yml up grafana
```
- the following should show
```
Creating network "docker_ran" with the default driver
Starting metrics_server ...
Starting metrics_server ... done
Creating grafana        ... done
Attaching to grafana
```
- go to `http://localhost:3300/` in your browser
![Screenshot from 2024-04-02 15-10-59](https://github.com/pchat-imm/oran-trace-metrics/assets/40858099/d89b56eb-5bce-48d3-9dbc-3c70a0923b9e)
