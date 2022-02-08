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

Note, supporting the concepts found in CDC Race & Ethnicity v1.2 is relevant to the terminological alignment that is happening in the OMOP+FHIR workgroup, as this vocabulary also serves as the base vocabulary for the current US Core IG (4.0.0) and proposed update (4.1.0) race and ethnicity extensions.

 - All codes will have `vocabulary_id = 'CDC Race and Ethnicity'` instead of `Race` or `Ethnicity`
 - Codes `1000-9` "Race" and `2133-7` "Ethnicity" will be marked as Classification Concepts, all others will be marked as Standard concepts.
 - The CDC v1.2 concepts that already exist in the current 'Race' and 'Ethnicity' vocabularies will retain their `concept_id`s from the current Race and Ethnicity Vocabulary concepts
 - `concept_code`s will be updated to reflect the concept codes in CDC v1.2, not the heirarchical codes (for example `1002-5` for 'American Indian or Alaska Native' instead of `1`)

Fixes
 - [no standard concept for German](https://forums.ohdsi.org/t/question-on-mapping-race/15759)


### 2. Add or "make standard" additional concepts not covered by CDC v1.2

- "Asian or Pacific Islander"

    This is an old OMB term that can often be found in source data in the US.

    SNOMED 413581001, `concept_id 4184984` will be marked as Standard, and as subsuming CDCv1.2 2028-9 "Asian" `concept_id 8515` and CDCv1.2 2076-8 "Native Hawaiian or Other Pacific Islander" `concept_id 8557`
- ...
- multi
- MENA

### 3. Merge the Race and Ethnicity Domains

### 4. One "Standard" Race, one "Standard" Ethnicity Observation

### 5. Update convention

- Ethnicity recommended for all, not only US data sources
- Race and Ethnicity in person table reflects most recent observation
- Race and ethnicity also have dated rows in the observation table. If multiple concepts apply, multiple rows with the same `observation_start_date` exist in the observation table.

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