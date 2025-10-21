Diagrama de Fluxo de Dados: Sistema de Agricultura Inteligente (IA-IoT)

Tarefa 2: Conceito IA-IoT
Cenário: Otimização de Irrigação e Nutrientes em Cultivo de Uva.

graph TD
    subgraph Edge Layer (Campo/Dispositivo)
        S1[Sensor: Umidade Solo] -- Dados em tempo real --> G(Gateway IoT - RPi)
        S2[Sensor: Temp/Umidade Ar] -- Dados em tempo real --> G
        S3[Sensor: NPK Nutrientes] -- Dados em tempo real --> G
        G -- Comando de Ação (A) --> A[Atuadores: Válvulas, Bombas]
    end
    
    G -- MQTT/HTTPS (Transmissão) --> C[Cloud/Servidor Central]
    
    subgraph Cloud Layer (Data Center)
        C -- Armazenamento --> DB(Banco de Dados Time-Series)
        DB -- Histórico + Tempo Real --> LSTM(Modelo de IA: RNN-LSTM)
        LSTM -- Previsão (Requisito de Água/Nutrientes) --> D(Módulo de Decisão Otimizada)
    end
    
    D -- Comando de Ação Otimizada --> C
    C -- Envia Comando (A) --> G
    
    style S1 fill:#c7f9f7,stroke:#333;
    style S2 fill:#c7f9f7,stroke:#333;
    style S3 fill:#c7f9f7,stroke:#333;
    style A fill:#a0d4ff,stroke:#333;
    style LSTM fill:#a0ffb0,stroke:#333;
    
    % Ciclo de Feedback
    A -- Alteração do Ambiente --> S1


Descrição do Fluxo (Resumo):

Aquisição (Edge): Sensores coletam dados e os enviam ao Gateway IoT.

Processamento (Cloud): O Gateway envia os dados para o Servidor Central. O Modelo RNN-LSTM processa a série temporal de dados para prever a necessidade hídrica e nutricional futura.

Decisão: O Módulo de Decisão (IA) calcula a ação ideal (Comando de Ação Otimizada).

Ação (Edge): O comando é enviado de volta ao Gateway, que aciona os Atuadores (válvulas de irrigação) para fechar o loop de otimização.