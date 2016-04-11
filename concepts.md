# Concept book
This document summarize:

- the main concepts which we agreed on to follow
- concepts which are under consideration so it could be moved up to the *Base concepts* in the future but it has a chance to be dropped as well
- the technical assumptions we used to define the concepts. If an assumption seems to be invalidated then we have to check the validity of the related concepts.

## Personas
There are two personas according to the two important use-cases of the editor:

**Bob, the builder:** who creates the templates and the base parts of it, the layouts and the blocks. He is expert in HTML and want to use his code snippets from other editors as well. 

**Claire, the editor:** who creates and send campaigns. She only knows basic HTML and want to use visual tools to fill up the content.


## Base technical concepts
**Custom HTML based:** the email editing is based upon the existing Custom HTML campaign type.

**New Campaign type:** the new editor comes with a new campaign type: *Block-based email campaigns*.

**Content type:** a new domain property is introduced in the Campaigns: the `content_type` with one of the following values per campaign:

  - `html`, as custom HTML campaigns editable by Content Editor
  - `template`, as VCMS campaigns
  - `block`, as higher level HTML campaigns editable by Visual Content Editor
  
**Campaign is Template:** in the backend all templates are handled the same as the campaigns, the only difference is that a template won't have reference to a Suite campaign. The templates and campaigns will be differentiate mainly in the UI.

**Base layout:** all campaign/template has a base layout which wraps the content part. It contains the doctype, the head and the style parts, and also a simple container for the contents. The base layout could be set per template.

**Blocks are rows:** the smallest editable layout part of a campaign/template is a row called Block - which means it could be organized vertically but never horizontally. It implicates that **the content of an email is a set of blocks in one, vertical dimension** (simply an array).

**Free positioning:** all of the blocks can be moved after placing. It implicates that it doesn't need to create the same block groups in all possible permutation for the layout - it only needs to create a block type once.
 
**Declarative editables:** the editable fields for Claire is defined in the block's HTML source by Bob. This fields could be defined as HTML tags or attributes with their local settings. The following editables are available:

  - *simple text:* plain text without any formatting. Used to force Claire to use the predefined the style of a title, etc.
  - *rich text:* customizable text with a WYSIWYG editor
  - *image:* the source could be set from the MediaDB or with a simple url. It supports mobile images by design.

**Inline editables:** all of the editable fields will be changed with inline editors in the preview.

**Customizable attributes:** variables with different types (eg. number, url, etc.) can be defined in the HTML source of a block. It means that Bob can mark an editable number such as *width* and an input will be automatically created in the UI to allow Claire to set its value.

**Emarsys blocks:** there are basic Emarsys blocks which are available for all users. These are protected and the users couldn't change them but they can fork to create new blocks.
 
**Block variations:** a block could have different variations, eg. with different HTML and styles.

**Permission control:** the customer could set the permissions for creating templates and/or campaigns per user.


## Concepts under consideration
**Auto inline CSS classes:** automatically inline all classes provided in `<style>` tags into the HTML tags. These CSS classes could be in the base layout.

**Encourage CSS classes:** CSS classes can be added to the HTML tags of a block and the class definitions can be added in template level *[?and in block level?]*. The styles should be automatically inlined into the HTML tags.

**Use SASS:** instead of CSS we accept SASS code - which enables variables and simplify creating complex styles. On the email/preview generation process all SASS code (from base layout, custom SASS, block level styling?) will be concatenated and then compiled - so a SASS variable could be used in all of the styles! The styles should be automatically inlined into the HTML tags.

**High HTML:** provide high-level HTML tags (eg. `<column>`, `<row>`, `<container>`, etc.) and attributes (eg. `<column size="2">`, etc.) to simplify the creation of complex and responsive layouts. These tags mean automatically added styles as well.

**Foundation:** use [ZURB's Foundation for Emails 2](http://foundation.zurb.com/emails.html) framework to get:

  - a well-defined and tested base layout
  - a base layout with responsive email support by design
  - pre-defined variables to modify the base attributes
  - a grid system
  - support of hiding images, content, etc. on mobile or desktop
  - high-level HTML tags to simplify creating complex but mobile friendly layouts
  - support and "always" up-to-date email techniques
  - a good documentation and learning resources


## Technical assumptions
**Real-time previews:** all the previews (block and a whole campaign) could be rendered on-the-fly everywhere using iframes.

**Row based campaigns:** all campaigns could be rendered as vertically arranged blocks.

**CSS inline:** inlining CSS could be safely managed by a 3rd party library such as [inline-css](https://github.com/jonkemp/inline-css). It also keeps the final email clean of the unnecessary classes but preserves classes under media queries. It could remove the classes to spare some space - but again, it preserves the ones related to media queries.

**SASS:** we could compile SASS on-the-fly for the previews in the client side.

**Foundation:** stack could be used in all platform - so we have no problem on rendering the previews and the final HTML content in the browser and in NodeJS. We don't have to fork and modify the Foundation stack, it works as we and the users expect! We expect that this framework will be maintained in the future.
