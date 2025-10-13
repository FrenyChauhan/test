# FRA Atlas User Workflows

This document contains the Mermaid workflow diagrams for all user types in the FRA Atlas system. It also highlights how different users collaborate and utilize the DSS for scheme planning and FRA implementation.

---

## Table of Contents

1. [Website Overview: FRA Atlas & DSS System](#fra-atlas--dss-system-website-workflow)
2. [Central Government (Ministry of Tribal Affairs)](#1-central-government-ministry-of-tribal-affairs)
3. [District-Level Tribal Welfare Departments & Line Departments of DAJGUA](#2-district-level-tribal-welfare-departments--line-departments-of-dajgua)
4. [Field Investigation Officer (FIO)](#3-field-investigation-officer-fio)
5. [NGOs Working with Tribal Communities](#4-ngos-working-with-tribal-communities)
6. [Planning & Development Authorities](#5-planning--development-authorities)


---

## FRA ATLAS & DSS SYSTEM WEBSITE WORKFLOW

```mermaid
flowchart TD
    %% PDA & DSS Portal Workflow
    A[🔑 Login to PDA Portal / DSS Dashboard] --> B[🗺️ Access verified FRA Atlas & village-level asset data]
    B --> C[📊 Analyze DSS recommendations: schemes, priorities, resource gaps]
    C --> D[🔍 Filter villages by need, FRA type, and existing interventions]
    D --> E[🎯 Select priority villages for scheme planning]
    E --> F[📝 Formulate development action plans using DSS insights]
    F --> G[🤝 Coordinate with District & Line Departments for approvals & resource allocation]
    G --> H[🏷️ Assign schemes to villages / tag parcels on FRA Atlas]
    H --> I[📈 Monitor scheme implementation and fund utilization]
    I --> J[📊 Compare DSS recommendations vs actual outcomes]
    J --> K[📑 Generate analytics, reports, & feedback to DSS]
    K --> L[🔒 Logout / End session]

    %% Central Govt
    CG[🏛️ Central Govt] -->|📡 Monitor progress| D[🏢 District Officials]
    CG -->|📤 Receive DSS reports| PDA[🏛️ Planning & Development Authorities]

    %% District Officials
    D1[🔑 Login to portal] --> D2[📂 Upload FRA docs: claims & title certificates]
    D2 --> D3[📝 Run OCR + NER to extract claimant & land data]
    D3 --> D4{❓ Low-confidence fields?}
    D4 -- Yes --> D5[✏️ Manual correction]
    D4 -- No --> D6[🗺️ Preliminary FRA Atlas mapping - yellow]
    D6 --> D7[📤 Assign claims to FIOs]
    D7 --> D8[📊 Monitor FIO progress & receive verification updates]

    %% Field Investigation Officers
    FIO1[🔑 FIO Login & view assigned claims] --> FIO2[📍 On-site verification]
    FIO2 --> FIO3[📸 Collect geotagged photos, shapefiles, evidence]
    FIO3 --> FIO4{✅ Claim valid?}
    FIO4 -- Yes --> FIO5[🟢 Approve mapping - Green in FRA Atlas]
    FIO4 -- No --> FIO6[🔴 Reject / mark conflict - Red]
    FIO5 & FIO6 --> FIO7[📝 Upload field notes & feedback]

    %% DSS & Planning Authorities
    PDA1[🔑 PDA Login & access verified FRA Atlas] --> PDA2[📊 Consult DSS recommendations]
    PDA2 --> PDA3[🎯 Prioritize villages & plan interventions]
    PDA3 --> PDA4[🤝 Coordinate with districts for approvals & resource allocation]
    PDA4 --> PDA5[📈 Monitor implementation & compare DSS vs actual outcomes]
    PDA5 --> PDA6[📑 Feedback to DSS & generate reports]
    PDA6 --> CG

    %% NGOs
    NGO1[🔑 NGO Login & access FRA Atlas + DSS] --> NGO2[🔍 Identify high-need villages]
    NGO2 --> NGO3[👐 Assist communities: awareness, documentation, scheme support]
    NGO3 --> NGO4[📤 Provide feedback & geotagged observations]
    NGO4 --> PDA2

    %% Connections
    D8 --> FIO1
    FIO7 --> PDA2
    FIO7 --> NGO1



```
## 1. Central Government (Ministry of Tribal Affairs)

```mermaid
flowchart TD
    A[🔑 Login with MFA credentials]
    B[📊 View dashboard: 4 states overview, FRA stats, claim status, assets, DSS recommendations]
    C[🗺️ Drill down to state → district → village]
    D[🔍 Review DSS recommendations and filter by FRA type, resources, schemes]
    E[📑 View scheme details: actions, target villages, benefits, priority]
    F[📈 Check implementation status and uploaded evidence]
    G{❓ Are all DSS recommendations implemented?}
    H[⚖️ Compare DSS recommendations vs actual action and identify gaps]
    I[📝 Provide oversight/feedback to DSS or departments]
    J[📊 Generate analytics & reports]
    K[📤 Export reports for policy decisions/meetings]
    L[💬 Query DSS Chatbot for specific questions]
    M[🔒 Logout / End session]

    %% Main flow
    A --> B --> C --> D --> E --> F --> G
    G -- ✅ Yes --> J --> K --> M
    G -- ❌ No --> H --> I --> D

    %% Optional chatbot queries
    D -.-> L
    E -.-> L
    F -.-> L
    L -.-> D


```
## 2.District-Level Tribal Welfare Departments & Line Departments of DAJGUA

```mermaid
flowchart TD
    A[🔑 Login to district/state portal]
    B[📄 Upload scanned FRA documents: IFR, CR, CFR, Title Certificates]
    C[📝 Upload metadata: claim date, Gram Sabha, claimant details, village]
    D[🤖 Run OCR + NER to extract claimant info and land details]
    E{❓ Any low-confidence fields?}
    F[✏️ Manual verification & correction by district officer]
    G[🟨 Preliminary Mapping in FRA Atlas - Yellow polygons]
    H[📎 Attach document references and claimant details]
    I[👷 Assign claims to Field Investigation Officers -FIOs]
    J[🗺️ FIO conducts on-site verification: geotagged shapefiles, photos, field notes]
    K[📤 Receive FIO updates: Approved ✅ / Rejected ❌ / Conflicts ⚠️]
    L[📊 Monitor verification progress & alert discrepancies]
    M[🔍 Check preliminary DSS recommendations for claims]
    N[📈 Generate district-level FRA implementation reports]
    O[📢 Notify FIOs or Gram Sabha officials of pending verifications or missing evidence]
    P[🔒 Logout / End session]

    %% Main flow with parallelism and loops
    A --> B --> C --> D --> E
    E -- ✅ Yes --> F --> G
    E -- ❌ No --> G
    G --> H
    H --> I
    I --> J
    J --> K
    K --> L
    L --> M
    L --> O
    K -->|⚠️ Conflicts detected| FIO_Conflict[Assign back for FIO review]
    FIO_Conflict --> J
    M --> N
    N --> P

    %% Optional parallel checks
    D -->|🔎 Check DSS rules & scheme eligibility| M
    G -->|✅ Verify attached documents & metadata| L

```
## 3️. Field Investigation Officer (FIO)
```mermaid
flowchart TD
    A[🔑 Login to FIO portal]
    B[🗂️ View assigned villages/claims]
    C[🟨 Review preliminary yellow polygons & claim documents]
    D[🗺️ On-site verification: boundaries, land use, forest cover, water bodies, homesteads]
    E[📸 Collect geotagged evidence: photos, shapefiles, community signatures, witness statements]
    F[🤝 Collaborate with NGOs for local insights & verification]
    G{❓ Mapping approved?}
    H[✅ Update FRA Atlas: Green = Verified, Red = Rejected/Conflict]
    I[📝 Document feedback/discrepancies for district review]
    J[📊 Feed verified polygons & asset layers into DSS]
    K[🔒 Logout; activity logged]

    %% Flow
    A --> B --> C
    C --> D
    D --> E
    E --> F
    F --> G
    G -- Yes --> H
    G -- No --> H
    H --> I --> J --> K

    %% Optional/parallel actions
    C -.-> F
    D -.-> F
    E -.-> J
    F -.-> J


```
## 4. NGOs Working with Tribal Communities
```mermaid
flowchart TD
    A[🔑 Login to NGO Portal]
    B[📊 View DSS Dashboard: recommended schemes & priority villages]
    C[🔍 Analyze DSS insights: resource gaps, FRA claim coverage, potential benefits]
    D[🎯 Select target villages for community support]
    E[👐 Conduct awareness drives & assist claimants in documentation]
    F[📤 Upload supporting data: feedback, resource status, local needs]
    G[📈 Monitor DSS recommendation implementation & village progress]
    H[💡 Provide feedback to DSS for policy improvement]
    I[📑 Generate NGO impact & community engagement reports]
    J[🔒 Logout / End session]

    A --> B --> C --> D --> E --> F --> G --> H --> I --> J
    C -.-> F
    D -.-> G
    F -.-> H


```
## 5. Planning & Development Authorities
```mermaid
flowchart TD
    A[🔑 Login to PDA/DSS Dashboard]
    B[📊 Access FRA Atlas & village-level asset data]
    C[📝 Consult DSS recommendations per village]
    D{High-priority villages identified by DSS?}
    D -- Yes --> E[📌 Analyze resources & scheme feasibility]
    D -- No --> F[⚠️ Flag for DSS review / wait for updates]
    E --> G[📝 Draft intervention plans & coordinate approvals]
    G --> H[🏷️ Assign/tag schemes on FRA Atlas per village/parcel]
    H --> I{Overlapping/conflicting schemes?}
    I -- Yes --> J[🔄 Resolve conflicts using DSS guidance]
    I -- No --> K[🚀 Implement schemes]
    K --> L[📈 Monitor execution & fund utilization]
    L --> M[📊 Compare DSS recommendations vs actual outcomes]
    M --> N{Outcomes aligned with DSS targets?}
    N -- Yes --> O[📑 Generate reports & analytics]
    N -- No --> P[🔄 Provide feedback to DSS]
    O --> Q[🔒 Logout / End session]
    P --> Q[🔒 Logout / End session]

    B -.-> C
    E -.-> H
    H -.-> L
    M -.-> P

    I -.-> M
    N -.-> Q


```
---
