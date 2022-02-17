- Start Date: 2022-07-02
- RFC Number:

# OMOP Race and Ethnicity

## Summary

> One paragraph explanation of the change.

## Motivation

> Why are we doing this? What use cases does it support? What is the expected
outcome?

## Design Detail

### 1. Update Race and Ethnicity Vocabularies with [CDC Race & Ethnicity v1.2](https://phinvads.cdc.gov/vads/DownloadHotTopicDetailFile.action?filename=29DF7191-76CC-E611-8E51-0017A477041A)

The current OMOP 'Race' and 'Ethnicity' vocabularies are not explicit about their origin, but appear to come from a prior version of the "CDC Race & Ethnicity" vocabulary. These vocabularies will be updated to the most current version (v1.2) and this origin will be explicitly stated.

The vocabulary and its internal mapping can be found [here @ phinvads.cdc.gov](https://phinvads.cdc.gov/vads/DownloadHotTopicDetailFile.action?filename=29DF7191-76CC-E611-8E51-0017A477041A)

See updated concepts [here](https://gist.github.com/Jake-Gillberg/c00bae772a1339c12344749704c6363a).

- All codes will have `vocabulary_id = 'CDC Race and Ethnicity'` instead of `Race` or `Ethnicity`
- Codes `1000-9` "Race" and `2133-7` "Ethnicity" will be marked as Classification Concepts, all others will be marked as Standard concepts, excepting `2131-1` "Other Race" which has already been marked as Non-Standard: Deleted and will stay the same (should be mapped to concept 0).
- The CDC v1.2 concepts that already exist in the current 'Race' and 'Ethnicity' vocabularies will retain their `concept_id`s from the current Race and Ethnicity Vocabulary concepts
- `concept_code`s will be updated to reflect the concept codes in CDC v1.2, not the heirarchical codes (for example `1002-5` for 'American Indian or Alaska Native' instead of `1`)

Fixes
 - [no standard concept for German](https://forums.ohdsi.org/t/question-on-mapping-race/15759)
 - [no standard concept for Afghanistani](https://github.com/OHDSI/Vocabulary-v5.0/issues/534)
 
 > Note, supporting the concepts found in CDC Race & Ethnicity v1.2 is relevant to the terminological alignment that is happening in the OMOP+FHIR workgroup, as this vocabulary also serves as the base vocabulary for the current US Core IG (4.0.0) and proposed update (4.1.0) race and ethnicity extensions.

### 2. Add or "make standard" additional concepts not covered by CDC v1.2

#### 2.1

- "Asian or Pacific Islander"

  This is an old OMB term that can often be found in source data in the US.

    SNOMED 413581001, `concept_id 4184984` will be marked as Standard, and as subsuming CDCv1.2 `2028-9` "Asian" `concept_id 8515` and CDCv1.2 `2076-8` "Native Hawaiian or Other Pacific Islander" `concept_id 8557`

#### 2.2

- "Multiple"
    
    New "OMOP Extension" concept, marked as Standard
    Synonyms: Multiracial, Multiethnic, Mixed, Mixed Race, Mixed Ethnicity - new OMOP Vocabulary Concept with domain "Race/Ethnicity"

    Fixes

  - (when combined with [4](#4-standard-observation-concepts-for-race-and-ethnicity), and [5](#5-update-conventions)) -  [No standard concepts for EHDEN mixed race categories](https://github.com/OHDSI/Vocabulary-v5.0/issues/454)

#### 2.3

- All other SNOMED [`415229000` Racial Group](https://browser.ihtsdotools.org/?perspective=full&conceptId1=415229000&edition=MAIN/2022-01-31&release=&languages=en) and [`372148003` Ethnic Group](https://browser.ihtsdotools.org/?perspective=full&conceptId1=372148003&edition=MAIN/2022-01-31&release=&languages=en) concepts that do not map to standard concepts (or flavors of null) should be marked as Standard.

    Fixes

    - [No standard concept for Punjabi](https://github.com/OHDSI/Vocabulary-v5.0/issues/534)

#### 2.4

- All LOINC answers to LOINC race or ethnicity observations marked non-standard in [4.1](#41) that do not map to standard concepts (or flavors of null) should be marked as Standard... (and put in the race/ethnicity domain)

#### 2.5

- PPI

### 3. Merge the Race and Ethnicity Domains

- All concepts in the which have the Domain "Race" or the Domain "Ethnicity" will be marked as Domain "Race/Ethnicity"

### 4. Standard Observation Concepts for Race and Ethnicity

#### 4.1

- "Race" concept_id 4013886 (SNOMED 103579009) stays standard.
- "Ethnic group" concept_id 4271761 (SNOMED 364699009) stays standard.
- All other standard race and ethnicity observations are mapped to the above and marked as non-standard. Their accepted values / answers are mapped to standard race/ethnicity domain values (see [2](#2-add-or-%22make-standard%22-additional-concepts-not-covered-by-cdc-v12)).

  - concept_id 1586138 (PPI TheBasics_Race)
  - concept_id 3046853 (LOINC 32624-9 Race)
  - concept_id 40759212 (LOINC 56091-2 Race [PhenX])
  - concept_id 43055686 (LOINC 72826-1 Race OMB.1997)
  - concept_id 44816591 (LOINC 74693-3 Race [AHRQ])
  - concept_id 3040025 (LOINC 54134-2 Race [USSG-FHT])
  - concept_id 3051279 (LOINC 53720-9 Race NAPIIA)
  - concept_id 21494232 (LOINC 80977-2 Tabulated race [CDC])
  - concept_id 3050381 (LOINC 46463-6 Race or ethnicity)
  - concept_id 40762453 (LOINC 59362-4 Race or ethnicity OMB.1997)
  - concept_id 42868352 (LOINC 69855-5 Race [HHS.ACA Section 4302])
  - ... ethnicity


### 5. Update conventions

- Any concept is that is in the race/ethnicity domain is valid for all - person.race_concept_id, person.ethnicity_concept_id, and observation_value_concept_id for all [(4.) race and ethnicity observation concepts](#4-standard-observation-concepts-for-race-and-ethnicity)
- Ethnicity recommended for all, not only US data sources
- Race and ethnicity in person table reflects most recent observation
- Race and ethnicity also have dated rows in the observation table.
- Multiple race / ethnicity concepts recorded - If multiple concepts apply at once, multiple rows with the same `observation_start_date` exist in the observation table, and person table contains the standard concept for "Multiple".
- In the case where recorded values are ambiguous as to whether a recorded value was an observation of race or ethnicity (for example, "check all races and ethnicities that apply" without the categories being clear from context that they are racial or ethnic), values should be stored as both race observations and ethnicity observations and in both person table columns.
- In the case where recorded values are NOT ambiguous as to whether a recorded value was on observation of race or ethnicity, values should be stored in their respective observations/columns, regardless of external judgement on whether or not the category is a valid race or ethnicity. (For example, "Hispanic or Latino" recorded as an answer to "Select all racial groups you identifiy with" should be entered as an observation of race.)

### 6. Mapping non-standard codes to standard



## Drawbacks

> Why should we *not* do this? Please consider the impact on users,
on the integration of this change with other existing and planned features etc.

> There are tradeoffs to choosing any path, please attempt to identify them here.

## Rationale and Alternatives

> Why is this design the best in the space of possible designs?

> What other designs have been considered and what is the rationale for not choosing them?

> What is the impact of not doing this?


## Prior Art

Discuss prior art, both the good and the bad, in relation to this proposal. A few examples of what this can include are:

> How other services / infrastructures in the same domain have solved this problem.

> Are there any published papers or great posts that discuss this? If you have some relevant papers to refer to, this can serve as a more detailed theoretical background.

This section is intended to encourage you as an author to think about the lessons from other organisations, provide readers of your RFC with a fuller picture. If there is no prior art, that is fine - your ideas are interesting whether they are brand new or if it is an adaptation from other services.

## Unresolved questions

### 1. Hiding, but keeping available for use, heirarchical mappings from standard concepts which do not make sense outside of a US context

### 2. Mapping and marking as "non-standard"
> What parts of the design do you expect to resolve through the RFC process before this gets merged?

> What parts of the design do you expect to resolve through the implementation of this feature before stabilisation?

> What related issues do you consider out of scope for this RFC that could be addressed in the future independently of the solution that comes out of this RFC?
