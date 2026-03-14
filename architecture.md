# Genflow Ad Studio Architecture

## High-Level Workflow (Conceptual)

This diagram shows the simplified user journey and the primary orchestration blocks.

```mermaid
graph LR
    User(["User (Input)"]) -->|URL + Persona| Discovery["Brand Discovery"]
    Discovery --> Creative["Creative Studio"]
    Creative --> Synthesis["Video Synthesis"]
    Synthesis --> Certification["Multi-Agent QC"]
    Certification -->|Verified Ad| User
```

---

## Detailed Systems Architecture

This diagram illustrates the end-to-end technical workflow, highlighting the "Pomelli-lite" brand integration and the Agentic Debate systems.

```mermaid
graph TD
    subgraph Frontend ["Frontend (Vite + React)"]
        UI["Product Form UI"]
        Log["Agentic Log Console"]
        Gallery["Video Gallery"]
    end

    subgraph Backend ["Backend (FastAPI)"]
        API["Pipeline Router"]
        
        subgraph Services ["Core Orchestration"]
            Pipe["Pipeline Service"]
            
            subgraph Phase1 ["Phase 1: Brand Discovery"]
                Scrape["Scraper Service"]
                DNA["Gemini 3 Flash (DNA Extract)"]
            end
            
            subgraph Phase2 ["Phase 2: Asset Prep"]
                Enhance["Image Service"]
                Nano["Nano Banana 2 (Enhancement)"]
            end
            
            subgraph Phase3 ["Phase 3: Creative"]
                Script["Script Service"]
                Story["Storyboard Service"]
                GeminiPro["Gemini 3 Pro"]
                
                subgraph StoryQC ["Storyboard War Room (Debate)"]
                    SDIR["Director QC"]
                    SBRN["Brand QC"]
                    SORC["Orchestrator"]
                end
            end
            
            subgraph Phase4 ["Phase 4: Synthesis"]
                Veo["Veo Service"]
                VideoGen["Veo (Video Synthesis)"]
                
                subgraph VideoQC ["Video Quality Control (Debate)"]
                    VDIR["Director QC"]
                    VBRN["Brand QC"]
                    VORC["Orchestrator"]
                end
            end
        end
        
        DB[("SQLite (Genflow.db)")]
        GCS[("GCS Bucket")]
    end

    %% Flow
    UI -->|URL + Image| API
    API --> Pipe
    
    Pipe --> Scrape --> DNA -->|BrandDNA| Pipe
    Pipe --> Enhance --> Nano -->|Enhanced Prod| Pipe
    Pipe --> Script --> GeminiPro -->|Script| Pipe
    
    Pipe --> Story --> GeminiPro
    GeminiPro <--> StoryQC
    StoryQC -->|Aligned Storyboard| Pipe
    
    Pipe --> Veo --> VideoGen
    VideoGen <--> VideoQC
    VideoQC -->|Certified Video| Pipe
    
    Pipe --> DB
    Pipe --> GCS
    Pipe -->|Events| Log
    Pipe --> Gallery
```

## Component Breakdown

1.  **Brand Discovery**: Extracts `tone_of_voice` and `target_demographic` from a provided URL to steer the entire creative process.
2.  **Asset Prep**: Uses **Nano Banana 2** (Gemini 3 Flash Image) to upscale and enhance raw product photos into studio-quality background plates.
3.  **Storyboard War Room**: A multi-agent debate loop where separate "Director" and "Brand" agents critique storyboard frames for brand alignment before finalization.
4.  **Video Quality Control**: A final agentic feedback loop overseeing Veo video synthesis, ensuring zero hallucinations and strict adherence to the brand's DNA.
