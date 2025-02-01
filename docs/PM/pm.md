 
### ИЕРАРХИЯ
??? fit failure
    ??? PINCAPT_M40_1 failure
    ??? PINCAPT_M40_2 failure
    ??? PINCAPT_M40_3 failure
    PINCAPT_M40_3 failure
    PINCAPT_M40_3 failure
### XDC
??? XDC failure
    ![alt text](IMG/image.png)
    ![alt text](IMG/image_1.png)

### Недороботаное 
??? pin_capt failure
    ``` mermaid
    flowchart LR

    D-->|text|A -->|ptime2:0|TDC1_CHA/TDCCHAN
    D-->|text|A -->|ptime2:0|DC1_CHB/TDCCHAN_HD168
    D-->|text|A -->|ptime2:0|TDC1_CHC/TDCCHAN_HD192
    D-->|text|A -->|ptime2:0|TDC1_CHD

    D-->|text|A -->|p|PLL1(CLK600_pll)
    ```
