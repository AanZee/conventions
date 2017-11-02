# Label Conventions

## Write labels in US English

## Prefer hyphens as delimiters or use camelCase

When hyphens are not possible because of specific code language or framework use camelCase.

## Categorize labels with the name of the front-end component

Make sure the name of the front-end component is well thought before categorizing labels.

Examples:

- notifications.idle-message-text -> Your session has expired because you were longer than %time% inactive. Please renew your selection.
- login.password-label -> Your password

## Categorize labels used in different components in ‘global’

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

The labels for buttons often differ in style per language, for example Dutch labels are often written in ‘gebiedende wijs’.

Examples:

- global.close-action -> Close
