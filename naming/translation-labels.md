# Translation labels

## Write labels in US English

## Use hyphens as delimiters

When hyphens are not possible because of specific code language or framework use camelCase.

## Categorize labels with name of component, page or website module

- Make sure the name of the component or page is well thought before categorizing labels.
- Categorize component in 'components', page in 'pages' and website module in 'modules'.

Examples:

- components.notifications.idle-message-text -> Your session has expired because you were longer than %time% inactive. Please renew your selection.
- pages.login.password-label -> Your password
- modules.checkout.payment-method-title -> Payment Method

## Categorize labels used in different components, pages or modules in ‘global’ or brand name

- Category 'global' should result in a translation that is or can be used for different websites and brands.
- If a website or brand wants to overrule a global translation, but still wants to use this translation for different components, pages or modules, the brand name can be used as category.

Examples:

- global.edit-action -> Edit
- global.optional-lowercase -> optional
- aanzee.optional-lowercase -> optional

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

- page.login.login-title -> Login
- modules.checkout.payment-method-title -> Payment Method
- modules.checkout.payment-failed-title -> Payment was Unsuccessful

## Labels for longer texts end with ‘text’

Examples:

- modules.checkout.payment-failed-text -> Try again or change payment method.

## Labels for HTML content should end with 'content'

Examples:

- components.modal-window.error-content -> `<p>Something went wrong.</p>`

## Labels for form labels end with ‘label’

Short description of what is expected from the user to fill in. These labels do not only contain labels that can be found in front of input fields, they can also contain labels found after radio buttons and checkboxes or in segmented controls.

Examples:

- pages.personal-information.mister-short-label -> Mr.
- pages.personal-information.email-label -> Email

## Labels for ‘form helper texts’ end with ‘helper-text’

Helper text are always visible directly below an input field. It helps the user to know what is expected and why it is needed.

Examples:

- pages.personal-information.email-helper-text -> You will receive a confirmation by email.

## Labels for ‘form feedback texts’ end with ‘feedback-text’

Feedback text gives feedback about why the data within an input field is incorrect and how the user can solve this. Feedback text is only visible after the user gets an error when submitting a form.

Examples:

- pages.personal-information.email-empty-feedback-text -> Your email address is needed to finish your booking.

## Labels for file names end with ‘file-name’

File names should not include the format of the document. This should be added by the back-end.

Examples:

- aanzee.general-conditions-file-name -> general-conditions

## Labels for buttons, links or actions end with action

The labels for buttons often differ in style per language, for example Dutch labels are often written in ‘gebiedende wijs’.

Examples:

- global.close-action -> Close
