graph LR
    %% 중앙 애플리케이션 영역 (Monolithic Streamlit App)
    subgraph Central Application
        direction TB
        %% 프레임워크
        StreamlitLogo[Streamlit Logo]
        
        %% 기능별 처리 파이프라인
        subgraph 피부암 진단 파이프라인
            ImageIcon[이미지 아이콘] --> PillowLogo[Pillow 로고] --> TensorFlowLogo[TensorFlow 로고] --> SkinCancerResult[결과 아이콘]
            style SkinCancerResult fill:#FFD166,stroke:#000
        end
        
        subgraph 인바디 분석 파이프라인
            PDFIcon[PDF 아이콘] --> PyPDF2Logo[PyPDF2 로고] --> LangChainLogo[LangChain 로고] --> OpenAILogo[OpenAI 로고] --> InbodyResult[결과 아이콘]
            style InbodyResult fill:#FFD166,stroke:#000
        end
        
        subgraph 챗봇 파이프라인
            ChatIcon[채팅 아이콘] --> LangChainLogo2[LangChain 로고] --> OpenAILogo2[OpenAI 로고] --> ChatbotResult[결과 아이콘]
            style ChatbotResult fill:#FFD166,stroke:#000
        end
        
        %% 공통 기능
        CommonTTSInput --> gTTSLogo[gTTS 로고]
        SkinCancerResult --> CommonTTSInput
        InbodyResult --> CommonTTSInput
        ChatbotResult --> CommonTTSInput
    end

    %% 사용자 및 외부 연동 영역
    UserArea[USER] <--> CentralApplication
    DataModels[Local Models & Data\nskin_cancer_models.h5] --> TensorFlowLogo

    %% 개발, 배포 및 관리 영역
    GitHubArea[GitHub] --> CentralApplication
    StreamlitCloudArea[Streamlit Cloud] --> CentralApplication
    ConfigFiles[requirements.txt\nsecrets.toml] --> CentralApplication

    %% 레이블
    classDef pipeline fill:#F8F9FA,stroke:#E0E0E0,stroke-width:2px
    class 피부암진단파이프라인,인바디분석파이프라인,챗봇파이프라인 pipeline
