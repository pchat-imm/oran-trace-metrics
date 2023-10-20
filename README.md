# oran-trace-metrics
## gNB
```
           -----------------DL-----------------------|------------------UL--------------------
 pci rnti  cqi  ri  mcs  brate   ok  nok  (%)  dl_bs | pusch  mcs  brate   ok  nok  (%)    bsr
   1 4601   15   1   27    17k   20    0   0%      0 |  65.5   27   107k   40    0   0%      0
   1 4601   15   1   27    19k   22    0   0%      0 |  65.5   27   112k   42    0   0%      0
   1 4601   15   1   27    17k   20    0   0%      0 |  65.5   26   112k   42    0   0%      0
   1 4601   15   1   27    17k   20    1   4%      0 |  65.5   27   107k   40    0   0%      0
```
from: https://docs.srsran.com/projects/project/en/latest/user_manuals/source/console_ref.html \
**pci** = [Physical Cell Identifier](https://www.sharetechnote.com/html/Handbook_LTE_PCI.html) \
**rnti** = [Radio Network Temporary Identifier](https://www.sharetechnote.com/html/5G/5G_RNTI.html)(UE identifier) \
**cqi** = [Channel Quality Indicator](https://www.sharetechnote.com/html/Handbook_LTE_CQI.html) reported by the UE 1-15. Main focus on different modulation \

**ri** = 

**mcs** = [Modulation and Coding Scheme](https://www.sharetechnote.com/html/5G/5G_MCS_TBS_CodeRate.html) from 0-28. There are three tables.
**brate** = Bitrate (bit/sec)
**ok** = Number of packet successfully sent
**nok** = Number of packet dropped
**(%)** = % of packets dropped

**bsr** = [Buffer status report](https://www.sharetechnote.com/html/Handbook_LTE_BSR.html) data waiting to be transmitted as reported by the UE (bytes)




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
