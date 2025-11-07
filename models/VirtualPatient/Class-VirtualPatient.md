classDiagram
    direction LR
    class VirtualPatient {
        <<VirtualModel>>
        +patient_id: Integer (Key)
        +name: String
        +bind_code: Integer
        +gender: String (ChoiceMap)
        +birthday: DateTime
        +specialist_id: Integer
        +hospital_registration: String (null=True)
        +phone_number: String (null=True)
        +weight: Float (null=True)
        +height: Float (null=True)
        +accept_tcl: Boolean
        +smoke_frequency: String (ChoiceMap, null=True)
        +drink_frequency: String (ChoiceMap, null=True)
        +user_id: Integer (null=True)
        +updated_at: Date
    }

    class Person {
        <<OMOP Table>>
        +person_id: Integer (PK)
        +gender_concept_id: Integer (from gender)
        +birth_datetime: DateTime (from birthday)
        +year_of_birth: Integer (Constant: CID_NULL)
        +race_concept_id: Integer (Constant: CID_NULL)
        +ethnicity_concept_id: Integer (Constant: CID_NULL)
        +provider_id: Integer (from specialist_id)
        +person_care_site_registration: String (from hospital_registration)
        +person_user_id: Integer (from user_id)
    }

    class PatientNonClinicalInfos {
        <<Custom Table>>
        +person_id: Integer (PK, from patient_id)
        +name: String (from name)
        +phone_number: String (from phone_number)
        +accept_tcl: Boolean (from accept_tcl)
        +bind_code: Integer (from bind_code)
    }

    class Measurement {
        <<OMOP Table>>
        +person_id: Integer (PK, from patient_id)
        +value_as_number: Float (from height/weight)
        +measurement_concept_id: Integer (PK, Constant: CID_HEIGHT/CID_WEIGHT)
        +unit_concept_id: Integer (Constant: CID_CENTIMETER/CID_KILOGRAM)
        +measurement_date: Date (from updated_at)
        +measurement_type_concept_id: Integer (Constant: CID_NULL)
    }

    class Observation {
        <<OMOP Table>>
        +person_id: Integer (PK, from patient_id)
        +observation_concept_id: Integer (PK, Constant: CID_SMOKE_FREQUENCY/CID_DRINK_FREQUENCY)
        +value_as_concept_id: Integer (from smoke_frequency/drink_frequency)
        +observation_date: Date (from updated_at)
        +observation_type_concept_id: Integer (Constant: CID_NULL)
    }

    VirtualPatient --|> Person : binds(row_person)
    VirtualPatient --|> PatientNonClinicalInfos : binds(row_nonclinicalinfos)
    VirtualPatient --|> Measurement : binds(row_height)
    VirtualPatient --|> Measurement : binds(row_weight)
    VirtualPatient --|> Observation : binds(row_smoke_frequency)
    VirtualPatient --|> Observation : binds(row_drink_frequency)
