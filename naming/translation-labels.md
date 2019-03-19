# Translation labels

## Write labels in US English

## Prefer hyphens as delimiters or use camelCase

When hyphens are not possible because of specific code language or framework use camelCase.

## Categorize labels with name of component or page

- Make sure the name of the component or page is well thought before categorizing labels.
- Categorize component in 'components' and page in 'pages'.

Examples:

- components.notifications.idle-message-text -> Your session has expired because you were longer than %time% inactive. Please renew your selection.
- pages.login.password-label -> Your password

## Categorize labels used in different components or pages in ‘global’

Examples:

- global.edit-action -> Edit
- global.optional-lowercase -> optional

## Labels containing ‘exact translations’ should contain only the exact words and end with the type of capitalization

The descriptions for capitalization is borrowed from CSS’s text-transform. Although CSS text-transform does not follow language-specific casing, this should of course be the case in the translations.

Examples:

- global.monday-capitalize -> Monday
- global.monday-lowercase -> monday
- global.monday-uppercase -> MONDAY

## Labels which are a abbreviations end with ‘short’

Capitalization type is added after the term ‘short’.

Examples:

- global.friday-short-capitalize -> Fr.

## Labels for a title end with ‘title’

The term ‘title’ gives important information about its context and how it should be translated. It is also language-specific, for example: in Dutch, only the first character is capitalized; in English, all the main words are capitalized.

Examples:

- login.login-title -> Login
- checkout.payment-method-title -> Payment Method
- checkout.payment-failed-title -> Payment was Unsuccessful

## Labels for longer texts end with ‘text’

Examples:

- checkout.payment-failed-text -> Try again or change payment method.

## Labels for HTML content should end with 'content'

Examples:

- modal-window.error-content -> `<p>Something went wrong.</p>`

## Labels for form labels end with ‘label’

Short description of what is expected from the user to fill in. These labels do not only contain labels that can be found in front of input fields, they can also contain labels found after radio buttons and checkboxes or in segmented controls.

Examples:

- personal-information.mister-short-label -> Mr.
- personal-information.email-label -> Email

## Labels for ‘form helper texts’ end with ‘helper’

Helper text are always visible directly below an input field. It helps the user to know what is expected and why it is needed.

Examples:

- personal-information.email-helper -> You will receive a confirmation by email.

## Labels for ‘form feedback texts’ end with ‘feedback’

Feedback text gives feedback about why the data within an input field is incorrect and how the user can solve this. Feedback text is only visible after the user gets an error when submitting a form.

Examples:

- personal-information.email-empty-feedback -> Your email address is needed to finish your booking.

## Labels for file names end with ‘file-name’

File names should not include the format of the document. This should be added by the back-end.

Examples:
- global.general-conditions-file-name -> general-conditions

## Labels for buttons, links or actions end with action

Examples:
- global.close-action -> Close

### Use imperative for direct actions
The label in a button that directly performs the desired action must be written imperative. So 'Save' instead of 'To save'. In English, this is often done correctly, but for instance in Dutch these are often mixed up. In Dutch write 'Bewaar' instead of 'Bewaren'.

### Use infinitive or imperative for indirect actions depending on language
A button or link that refers to a page or form in which the action can be performed, must be written:
- Infinitive in Dutch: write 'Reserveren' instead of 'Reserveer' for the reference to the reservation form. Titles of a form must also be written infinitive, so the title of the login form has the title 'Inloggen' and not 'Log in'.
- Imperative in English: the same as direct actions.

### Use ellipsis for changes on the page or view
A button or link that does not refer to another page, but for example opens a popover or a modal window or brings up a new section, ends with an ellipse. However, as soon as this button or link has a directional icon (e.g. chevron, arrow) or visually sufficiently communicates the consequences, the ellipse should not be added. An ellipse will not be part of the label that can be entered by the content manager. It will have to be added by a developer to the codebase immediately after the label variable. This gives flexibility to replace an ellipse with, for example, a chevron without having to change the content or label type.
