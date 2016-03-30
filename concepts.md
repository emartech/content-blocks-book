# Concept book
This document summarize:
- the main concepts which we agreed on to follow
- concepts which are under consideration so it could be moved up to the *Base concepts* in the future but it has a chance to be dropped as well
- the technical assumptions we used to define the concepts. If an assumption seems to be invalidated then we have to check the validity of the related concepts.

## Base technical concepts
**Custom HTML based:** the email editing is based upon the existing Custom HTML campaign type

**New Campaign type:** the new editor comes with a new campaign type: *Block-based email campaigns*

**Content type:** a new domain property is introduced in the Campaigns: the `content_type` with one of the following values per campaign:
  - `html`, as custom HTML campaigns editable by Content Editor
  - `template`, as VCMS campaigns
  - `block`, as higher level HTML campaigns editable by Content Blocks Editor
  
**Campaign is Template:** in the backend all templates are handled the same as the campaigns, the only difference is that a template won't have reference to a Suite campaign. The templates and campaigns will be differentiate mainly in the frontend.

**Blocks are rows:** an editable layout part of a campaign/template is a row - which means it could be organized vertically but never horizontally. It implicates that **the content of an email is a set of blocks in one, vertical dimension** (simply an array).


## Concepts under consideration
**Claire uses HTML:** Claire should easily modify the HTML source of a block

## Technical assumptions
**Real-time previews:** all the previews (block and a whole campaign) could be rendered realtime everywhere using iframes.
