```mermaid
graph TD
    %% Power Source
    VCC_5V[External 5V Power] --- Servo_Red[Servo VCC]
    VCC_5V --- ESP_Vin[ESP32 Vin Pin]
    GND_Common[Common Ground] --- ESP_GND[ESP32 GND]
    GND_Common --- Servo_Brown[Servo GND]
    GND_Common --- DHT_GND[DHT11 GND]
    GND_Common --- R10k_L[10k Resistor L]
    GND_Common --- R10k_R[10k Resistor R]

    subgraph "ESP32 DEVKIT V1"
        direction TB
        E_3V3[3.3V Pin]
        E_P34[GPIO 34 - LDR L]
        E_P35[GPIO 35 - LDR R]
        E_P18[GPIO 18 - SERVO]
        E_P04[GPIO 4 - DHT11]
    end

    subgraph "Sensors & Inputs"
        LDR_L[LDR Left]
        LDR_R[LDR Right]
        DHT[DHT11 Sensor]
    end

    %% Wiring Connections
    E_3V3 --- LDR_L & LDR_R & DHT_VCC[DHT11 VCC]
    
    LDR_L --- E_P34
    E_P34 --- R10k_L
    
    LDR_R --- E_P35
    E_P35 --- R10k_R
    
    DHT --- E_P04
    E_P18 -- "PWM Signal" --> Servo_Orange[Servo Signal]

    subgraph "Output & Monitoring"
        Servo[Servo Motor] -.-> Solar[PV Solar Panel]
        ESP32 -- "WiFi" --> Blynk[Blynk Dashboard]
    end

    style ESP32 fill:#333,color:#fff
    style Servo fill:#007bff,color:#fff
    style Solar fill:#28a745,color:#fff
    style Blynk fill:#17a2b8,color:#fff```
