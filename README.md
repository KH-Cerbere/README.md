```mermaid
graph TD
    %% 定义节点样式
    classDef database fill:#e1f5fe,stroke:#01579b,stroke-width:2px;
    classDef process fill:#fff9c4,stroke:#fbc02d,stroke-width:2px;
    classDef result fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px;
    classDef exclude fill:#ffebee,stroke:#c62828,stroke-width:1px,stroke-dasharray: 5 5;

    %% 阶段1：识别 (Identification)
    subgraph Identification [阶段 1: 文献识别]
        DB1[Web of Science]:::database
        DB2[Scopus]:::database
        DB3["IEEE Xplore<br>(n = 430)"]:::database
        
        Total_Raw["原始检索总量<br>(n = 3,255)"]:::process
    end

    %% 阶段2：筛选 (Screening)
    subgraph Screening [阶段 2: 文献筛选]
        Dedup["剔除重复文献<br>(n = 1,850 剩余)"]:::process
        TitleAbs["标题与摘要筛选<br>(基于纳入/排除标准)"]:::process
        
        Exclude1["排除文献 (n = 1,420)<br>1. 单体建筑研究<br>2. 纯宏观经济模型<br>3. 非相关主题"]:::exclude
    end

    %% 阶段3：合格性 (Eligibility)
    subgraph Eligibility [阶段 3: 全文评估]
        FullText["全文检索与评估<br>(n = 430)"]:::process
        
        Exclude2["排除全文 (n = 280)<br>1. 缺乏具体建模方法<br>2. 数据来源描述不清<br>3. 质量评估未达标"]:::exclude
    end

    %% 阶段4：纳入 (Included)
    subgraph Included [阶段 4: 最终纳入]
        FinalSet["最终纳入综述分析的文献<br>(n = 150)"]:::result
        
        %% 分类以便后续章节撰写
        Cat1["物理建模类<br>(n ~40)"]
        Cat2["数据驱动/感知类<br>(n ~70)"]
        Cat3["碳中和应用类<br>(n ~40)"]
    end

    %% 连线逻辑
    DB1 & DB2 & DB3 --> Total_Raw
    Total_Raw --> Dedup
    Dedup --> TitleAbs
    TitleAbs --> Exclude1
    TitleAbs --> FullText
    FullText --> Exclude2
    FullText --> FinalSet
    
    FinalSet -.-> Cat1
    FinalSet -.-> Cat2
    FinalSet -.-> Cat3
