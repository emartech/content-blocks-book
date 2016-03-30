# Concept book
This document summarize:
- the main concepts which we agreed on to follow
- concepts which are under consideration so it could be moved up to the *Base concepts* in the future but it has a chance to be dropped as well
- the technical assumptions we used to define the concepts. If an assumption seems to be invalidated then we have to check the validity of the related concepts.

## Base technical concepts
**Custom HTML based:** the email editing is based upon the existing Custom HTML campaign type.

**New Campaign type:** the new editor comes with a new campaign type: *Block-based email campaigns*.

**Content type:** a new domain property is introduced in the Campaigns: the `content_type` with one of the following values per campaign:
  - `html`, as custom HTML campaigns editable by Content Editor
  - `template`, as VCMS campaigns
  - `block`, as higher level HTML campaigns editable by Content Blocks Editor
  
**Campaign is Template:** in the backend all templates are handled the same as the campaigns, the only difference is that a template won't have reference to a Suite campaign. The templates and campaigns will be differentiate mainly in the frontend.

**Base layout:** all campaign/template has a base layout which wraps the content part. It contains the doctype, the head and the style parts, and also a simple container for the contents. The base layout could be set per template.

**Blocks are rows:** an editable layout part of a campaign/template is a row - which means it could be organized vertically but never horizontally. It implicates that **the content of an email is a set of blocks in one, vertical dimension** (simply an array).

**Declarative editables:** the editable fields for Claire is defined in the block's HTML source by Bob. This fields could be defined as HTML tags or attributes with their local settings. The following editables are available:
  - *simple text:* plain text without any formatting. Used to force Claire to use the predefined the style of a title, etc.
  - *rich text:* customizable text with a WYSIWYG editor
  - *image:* the source could be set from the MediaDB or with a simple url. It supports mobile images by design.


## Concepts under consideration
**Claire uses HTML:** Claire should easily modify the HTML source of a block. It could be important if Claire can't customize the campaign enough to her needs using the tools we've provided.

**Auto inline CSS classes:** automatically inline all classes provided in `<style>` tags into the HTML tags. These CSS classes could be in the base layout.

**Encourage CSS classes:** CSS classes can be added to the block HTML tags and the class definitions can be added in template level *[?and in block level?]*. The styles will be automatically inlined into the HTML tags.

**Use SASS:** instead of CSS we accept SASS code - which enables variables and simplify creating complex styles. On the email/preview generation process all SASS code (from base layout, custom SASS, block level styling?) will be concatenated and then compiled - so a SASS variable could be used in all of the styles!

**High HTML:** provide high-level HTML tags to simplify the creation of complex and responsive layouts. These tags mean automatically added styles as well.

**Foundation:** use [ZURB's Foundation for Emails 2](http://foundation.zurb.com/emails.html) framework to get:
  - a well-defined and tested base layout
  - a base layout with responsive email support by design
  - pre-defined variables to modify the base attributes
  - a grid system
  - high-level HTML tags to simplify creating complex but mobile friendly layouts
  - support and "always" up-to-date email techniques
  - a good documentation and learning resources


## Technical assumptions
**Real-time previews:** all the previews (block and a whole campaign) could be rendered on-the-fly everywhere using iframes.

**CSS inline:** inlining CSS could be safely managed by a 3rd party library such as [inline-css](https://github.com/jonkemp/inline-css). It also keeps the final email clean of the unnecessary classes but preserves classes under media queries. It could remove the classes to spare some space - but again, it preserves the ones related to media queries.

**SASS:** we could compile SASS on-the-fly for the previews in the client side.

**Foundation:** stack could be used in all platform - so we have no problem on rendering the previews and the final HTML content in the browser and in NodeJS. We don't have to fork and modify the Foundation stack, it works as we and the users expect! We expect that this framework will be maintained in the future.
