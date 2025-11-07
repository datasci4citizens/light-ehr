classDiagram
    direction LR
    class VirtualWound {
        <<VirtualModel>>
        +wound_id: Integer (Key)
        +region: String (ChoiceMap)
        +wound_type: String (ChoiceMap)
        +start_date: Date
        +end_date: Date (null=True)
        +is_active: Boolean (ChoiceMap)
        +image_id: Integer (null=True)
        +patient_id: Integer
        +specialist_id: Integer
        +updated_at: Date
    }

    class ConditionOccurrence {
        <<OMOP Table>>
        +condition_occurrence_id: Integer (PK, from wound_id)
        +person_id: Integer (from patient_id)
        +provider_id: Integer (from specialist_id)
        +condition_concept_id: Integer (from wound_type)
        +condition_start_date: Date (from start_date)
        +condition_end_date: Date (from end_date)
        +condition_status_concept_id: Integer (from is_active)
        +condition_type_concept_id: Integer (Constant: CID_NULL)
    }

    class Observation {
        <<OMOP Table>>
        +person_id: Integer (PK, from patient_id)
        +observation_concept_id: Integer (PK, Constant: CID_WOUND_LOCATION)
        +observation_date: Date (from updated_at)
        +value_as_concept_id: Integer (from region)
        +observation_event_id: Integer (PK, from wound_id)
        +obs_event_field_concept_id: Integer (Constant: CID_PK_CONDITION_OCCURRENCE)
        +observation_type_concept_id: Integer (Constant: CID_NULL)
    }

    class WoundImage {
        <<Custom Table>>
        +image_id: Integer (from image_id)
        +wound_id: Integer (PK, from wound_id)
    }

    VirtualWound --|> ConditionOccurrence : binds(row_condition)
    VirtualWound --|> Observation : binds(row_region)
    VirtualWound --|> WoundImage : binds(row_image)