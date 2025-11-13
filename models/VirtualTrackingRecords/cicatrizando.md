---
layout: mermaid
title: VirtualTrackingRecords/Cicatrizando
permalink: /models/VirtualTrackingRecords/cicatrizando/
---
~~~mermaid
graph LR
    %% Virtual Model
    VTR[VirtualTrackingRecords]
    
    %% Virtual Fields
    VTR --> tracking_id[tracking_id]
    VTR --> patient_id[patient_id]
    VTR --> specialist_id[specialist_id]
    VTR --> track_date[track_date]
    VTR --> wound_id[wound_id]
    VTR --> length[length]
    VTR --> width[width]
    VTR --> exudate_amount[exudate_amount]
    VTR --> exudate_type[exudate_type]
    VTR --> tissue_type[tissue_type]
    VTR --> wound_edges[wound_edges]
    VTR --> skin_around[skin_around]
    VTR --> had_a_fever[had_a_fever]
    VTR --> pain_level[pain_level]
    VTR --> dressing_changes[dressing_changes_per_day]
    VTR --> image_id[image_id]
    VTR --> guidelines[guidelines_to_patient]
    VTR --> extra_notes[extra_notes]
    
    %% OMOP Tables
    PO[ProcedureOccurrence]
    FR[FactRelationship]
    ML[Measurement - Length]
    MW[Measurement - Width]
    MEA[Measurement - Exudate Amount]
    MET[Measurement - Exudate Type]
    MTT[Measurement - Tissue Type]
    MWE[Measurement - Wound Edges]
    MSA[Measurement - Skin Around]
    MF[Measurement - Fever]
    MPL[Measurement - Pain Level]
    MDC[Measurement - Dressing Changes]
    TRI[TrackingRecordImage]
    NG[Note - Guidelines]
    NE[Note - Extra Notes]
    
    %% Mappings to ProcedureOccurrence
    tracking_id --> |procedure_occurrence_id| PO
    patient_id --> |person_id| PO
    specialist_id --> |provider_id| PO
    track_date --> |procedure_date| PO
    
    %% Mappings to FactRelationship
    wound_id --> |fact_id_1| FR
    tracking_id --> |fact_id_2| FR
    
    %% Mappings to Measurements
    length --> |value_as_number| ML
    width --> |value_as_number| MW
    exudate_amount --> |value_as_concept_id| MEA
    exudate_type --> |value_as_concept_id| MET
    tissue_type --> |value_as_concept_id| MTT
    wound_edges --> |value_as_concept_id| MWE
    skin_around --> |value_as_concept_id| MSA
    had_a_fever --> |value_as_concept_id| MF
    pain_level --> |value_as_number| MPL
    dressing_changes --> |value_as_number| MDC
    
    %% Mappings to TrackingRecordImage
    image_id --> |image_id| TRI
    tracking_id --> |tracking_record_id| TRI
    
    %% Mappings to Notes
    guidelines --> |note_text| NG
    patient_id --> |person_id| NG
    track_date --> |note_date| NG
    tracking_id --> |note_event_id| NG
    
    extra_notes --> |note_text| NE
    patient_id --> |person_id| NE
    track_date --> |note_date| NE
    tracking_id --> |note_event_id| NE
    
    %% Styling
    classDef virtualModel fill:#e1f5ff,stroke:#01579b,stroke-width:3px
    classDef virtualField fill:#fff9c4,stroke:#f57f17,stroke-width:2px
    classDef omopTable fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
    
    class VTR virtualModel
    class tracking_id,patient_id,specialist_id,track_date,wound_id,length,width,exudate_amount,exudate_type,tissue_type,wound_edges,skin_around,had_a_fever,pain_level,dressing_changes,image_id,guidelines,extra_notes virtualField
    class PO,FR,ML,MW,MEA,MET,MTT,MWE,MSA,MF,MPL,MDC,TRI,NG,NE omopTable
~~~