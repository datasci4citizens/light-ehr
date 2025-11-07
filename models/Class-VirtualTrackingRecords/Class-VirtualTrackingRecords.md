classDiagram
    direction LR
    class VirtualTrackingRecords {
        <<VirtualModel>>
        +tracking_id: Integer (Key)
        +patient_id: Integer
        +specialist_id: Integer
        +track_date: Date
        +wound_id: Integer
        +length: Float (null=True)
        +width: Float (null=True)
        +exudate_amount: String (ChoiceMap, null=True)
        +exudate_type: String (ChoiceMap, null=True)
        +tissue_type: String (ChoiceMap, null=True)
        +wound_edges: String (ChoiceMap, null=True)
        +skin_around: String (ChoiceMap, null=True)
        +had_a_fever: Boolean (ChoiceMap)
        +pain_level: Integer (null=True)
        +dressing_changes_per_day: Integer (null=True)
        +image_id: Integer (null=True)
        +guidelines_to_patient: String
        +extra_notes: String
    }

    class ProcedureOccurrence {
        <<OMOP Table>>
        +procedure_occurrence_id: Integer (PK, from tracking_id)
        +person_id: Integer (from patient_id)
        +provider_id: Integer (from specialist_id)
        +procedure_concept_id: Integer (Constant: CID_WOUND_PHOTOGRAPHY)
        +procedure_date: Date (from track_date)
        +procedure_type_concept_id: Integer (Constant: CID_NULL)
    }

    class FactRelationship {
        <<OMOP Table>>
        +domain_concept_id_1_id: Integer (Constant: CID_PK_CONDITION_OCCURRENCE)
        +fact_id_1: Integer (from wound_id)
        +relationship_concept_id: Integer (PK, Constant: CID_CONDITION_RELEVANT_TO)
        +domain_concept_id_2_id: Integer (Constant: CID_PK_PROCEDURE_OCCURRENCE)
        +fact_id_2: Integer (PK, from tracking_id)
    }

    class Measurement {
        <<OMOP Table>>
        +person_id: Integer (PK, from patient_id)
        +measurement_date: Date (from track_date)
        +measurement_event_id: Integer (PK, from tracking_id)
        +meas_event_field_concept_id: Integer (Constant: CID_PK_PROCEDURE_OCCURRENCE)
        +measurement_type_concept_id: Integer (Constant: CID_NULL)
        +value_as_number: Float (from length, width, pain_level, dressing_changes_per_day)
        +value_as_concept_id: Integer (from exudate_amount, exudate_type, tissue_type, wound_edges, skin_around, had_a_fever)
        +measurement_concept_id: Integer (PK, Constant: CID_WOUND_LENGTH, CID_WOUND_WIDTH, CID_EXUDATE_AMOUNT, etc.)
        +unit_concept_id: Integer (Constant: CID_CENTIMETER, CID_NULL)
    }

    class TrackingRecordImage {
        <<Custom Table>>
        +image_id: Integer (from image_id)
        +tracking_record_id: Integer (PK, from tracking_id)
    }

    class Note {
        <<OMOP Table>>
        +person_id: Integer (from patient_id)
        +note_date: Date (from track_date)
        +note_class_concept_id: Integer (PK, Constant: CID_WOUND_MANAGEMENT_NOTE, CID_GENERIC_NOTE)
        +encoding_concept_id: Integer (Constant: CID_UTF8)
        +language_concept_id: Integer (Constant: CID_PORTUGUESE)
        +note_text: String (from guidelines_to_patient, extra_notes)
        +note_event_id: Integer (PK, from tracking_id)
        +note_event_field_concept_id: Integer (Constant: CID_PK_PROCEDURE_OCCURRENCE)
        +note_type_concept_id: Integer (Constant: CID_NULL)
    }

    VirtualTrackingRecords --|> ProcedureOccurrence : binds(row_procedure)
    VirtualTrackingRecords --|> FactRelationship : binds(row_fact_relation)
    VirtualTrackingRecords --|> Measurement : binds(row_length)
    VirtualTrackingRecords --|> Measurement : binds(row_width)
    VirtualTrackingRecords --|> Measurement : binds(row_exudate_amount)
    VirtualTrackingRecords --|> Measurement : binds(row_exudate_type)
    VirtualTrackingRecords --|> Measurement : binds(row_tissue_type)
    VirtualTrackingRecords --|> Measurement : binds(row_wound_edges)
    VirtualTrackingRecords --|> Measurement : binds(row_skin_around)
    VirtualTrackingRecords --|> Measurement : binds(row_had_a_fever)
    VirtualTrackingRecords --|> Measurement : binds(row_pain_level)
    VirtualTrackingRecords --|> Measurement : binds(row_dressing_changes_per_day)
    VirtualTrackingRecords --|> TrackingRecordImage : binds(row_image)
    VirtualTrackingRecords --|> Note : binds(row_guidelines_note)
    VirtualTrackingRecords --|> Note : binds(row_extra_notes)