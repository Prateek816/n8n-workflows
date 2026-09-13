'''Mermaid
flowchart LR

%% ============================================================
%% SAMparkX — AI LEAD GENERATION SYSTEM
%% n8n WORKFLOW REPRESENTATION
%% ============================================================


%% ============================================================
%% TRIGGER + BUSINESS PROFILE
%% ============================================================

ST["⚡ Schedule Trigger"]

GBP["📊 Get Enhanced<br/>Business Profile"]

ST -->|"1 item"| GBP


%% ============================================================
%% STRATEGIC SUBREDDIT SELECTOR
%% ============================================================

SSS["🧠 Strategic<br/>Subreddit Selector"]

SSM["🔵 Google Gemini Chat<br/>Model"]

SSP["⚙️ Subreddit Output<br/>Parser"]

GBP -->|"2 items"| SSS

SSM -.->|"Model"| SSS
SSP -.->|"Output Parser"| SSS


%% ============================================================
%% MULTI QUERY GENERATOR
%% ============================================================

MQG["🧠 Multi-Query<br/>Generator"]

QGM["🔵 Query Generator<br/>Model"]

MQP["⚙️ Multi-Query Output<br/>Parser"]

SSS -->|"2 items"| MQG

QGM -.->|"Model"| MQG
MQP -.->|"Output Parser"| MQG


%% ============================================================
%% JAVASCRIPT PROCESSING
%% ============================================================

JS["{} Code in<br/>JavaScript"]

MQG -->|"2 items"| JS


%% ============================================================
%% SPLIT QUERY BATCHES
%% ============================================================

SQB["🔀 Split Query<br/>Batches"]

JS -->|"2 items"| SQB


%% ============================================================
%% REDDIT SEARCH ENGINE
%% ============================================================

RSE["🔴 Reddit Search<br/>Engine"]

SQB -.->|"Search Query"| RSE


%% ============================================================
%% CURRENT HTTP REQUEST / AYRSHARE
%% ============================================================

HTTP["🌐 HTTP Request<br/><small>POST: https://app.ayrshare.com/api/post</small>"]

SQB -->|"Query Batch"| HTTP


%% ============================================================
%% AI LEAD CLASSIFIER
%% ============================================================

ALC["🏷️ AI Lead<br/>Classifier"]

LCM["🔵 Lead Classifier<br/>Model"]

SQB -->|"Query / Candidate Items"| ALC

LCM -.->|"Model"| ALC


%% ============================================================
%% CLASSIFIER OUTPUTS
%% ============================================================

HIGH["HIGH_POTENTIAL"]

MEDIUM["MEDIUM_POTENTIAL"]

LOW["LOW_POTENTIAL"]

NONE["NO_POTENTIAL"]

ALC -->|"High Potential"| HIGH
ALC -->|"Medium Potential"| MEDIUM
ALC -->|"Low Potential"| LOW
ALC -->|"No Potential"| NONE


%% ============================================================
%% LOOP OVER ITEMS
%% ============================================================

LOOP["🔁 Loop Over Items"]

HIGH --> LOOP
MEDIUM --> LOOP
LOW --> LOOP
NONE --> LOOP


%% ============================================================
%% SERVICE OPPORTUNITY ANALYSIS
%% ============================================================

SO["💼 Service<br/>Opportunity Analysis"]

SOM["🔵 Service Opportunity<br/>Model"]

SOAP["⚙️ Service Analysis<br/>Parser"]

LOOP -->|"loop"| SO

SOM -.->|"Model"| SO
SOAP -.->|"Output Parser"| SO


%% ============================================================
%% HIGH VALUE FILTER
%% ============================================================

HVF["🔎 High Value<br/>Filter"]

SO -->|"Qualified Service Opportunity"| HVF


%% ============================================================
%% SAVE HIGH VALUE LEADS
%% ============================================================

SAVE["📊 Save High-Value Leads<br/><small>appendOrUpdate: Sheet</small>"]

HVF -->|"High-Value Lead"| SAVE


%% ============================================================
%% LOOP BACK
%% ============================================================

SAVE -->|"Next Item"| LOOP


%% ============================================================
%% LOOP DONE OUTPUT
%% ============================================================

DONE["✓ Done"]

LOOP -->|"done"| DONE


%% ============================================================
%% MANUAL EXECUTION TRIGGER
%% ============================================================

MANUAL["▶️ When clicking<br/>'Execute workflow'"]

MANUAL -.->|"Manual execution"| LOOP


%% ============================================================
%% NODE STYLING
%% ============================================================

classDef trigger fill:#111827,stroke:#22c55e,color:#ffffff,stroke-width:2px;
classDef sheets fill:#14532d,stroke:#22c55e,color:#ffffff,stroke-width:2px;
classDef ai fill:#111827,stroke:#22c55e,color:#ffffff,stroke-width:2px;
classDef model fill:#111827,stroke:#22c55e,color:#ffffff,stroke-width:2px;
classDef parser fill:#111827,stroke:#a3a3a3,color:#ffffff,stroke-width:1px;
classDef process fill:#111827,stroke:#9ca3af,color:#ffffff,stroke-width:1px;
classDef reddit fill:#7f1d1d,stroke:#f97316,color:#ffffff,stroke-width:2px;
classDef http fill:#111827,stroke:#ef4444,color:#ffffff,stroke-width:2px;
classDef decision fill:#111827,stroke:#f59e0b,color:#ffffff,stroke-width:2px;
classDef output fill:#14532d,stroke:#22c55e,color:#ffffff,stroke-width:2px;
classDef branch fill:#111827,stroke:#6366f1,color:#ffffff,stroke-width:1px;


%% ============================================================
%% APPLY STYLES
%% ============================================================

class ST,MANUAL trigger;

class GBP,SAVE sheets;

class SSS,MQG,ALC,SO ai;

class SSM,QGM,LCM,SOM model;

class SSP,MQP,SOAP parser;

class JS,SQB,LOOP,DONE process;

class RSE reddit;

class HTTP http;

class HVF decision;

class HIGH,MEDIUM,LOW,NONE branch;
'''