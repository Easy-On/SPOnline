# AGENTS.md

Guidance for AI agents creating and editing lab guides: Markdown repositories with labs, practices, and reusable instructions for training courses. Repository-specific facts (course name, scenario, machines, accounts, paths, scripts) belong in a `## Repository specifics` section at the end of this file.

## Language

All repository content is written in English (US): Markdown, file and folder names, scripts, comments, commit messages. Reply to the user in their language, but never write another language into repository files.

## Content types

| Type | Purpose | Duration | File name |
| ---- | ------- | -------- | --------- |
| Practice | Instructor demonstrates, participants follow along | 5-10 minutes | Imperative: `Configure-sharing-settings.md` |
| Lab | Participants work independently | 15 minutes or more | Imperative: `Manage-permissions.md` |
| General instruction | Reusable how-to, linked from labs and practices | | Gerund: `Creating-a-list.md` |

* Default folders: `Instructions/Labs/`, `Instructions/Practices/`, `Instructions/General/`, `Instructor/` (instructor notes), `images/` (screenshots, `lowercase-with-hyphens`). Follow the existing structure if it differs.
* File names: words separated by hyphens, first word capitalized, product names keep their capitalization. The H1 equals the file name with spaces instead of hyphens, prefixed with `Practice: ` or `Lab: ` for practices and labs.
* At most one lab per course module; a lab belongs to exactly one module.
* No redundancy: before creating or revising a practice or lab, check that no other one covers the same tasks.
* Minimize dependencies: each practice or lab must be completable on its own. Prefer objects that already exist over objects created by earlier practices or labs. Name an unavoidable dependency in Setup; do not add new ones.
* If the repository provides skills for writing practices or labs, use them.

## Structure

* **Lab:** `# Lab: <Title>`, `## Setup` (machine, sign-in, catch-up steps for skipped labs), `## Introduction` (scenario: what and why), `## Exercises` (linked list), then one `## Exercise n: <Title>` per exercise. Exercises contain numbered steps directly or an overview list linking to `### Task n: <Title>` sections. Tasks are self-contained: they start with opening the tool, navigating, and signing in. Alternative methods in a task use `####` headings.
* **Practice:** `# Practice: <Title>`, optional `## Setup` and `## Introduction`, `## Task` (short goal, often a requirements list), `## Instructions` (starts with the sentence naming the machine or portal, then the steps).
* **General instruction:** Gerund H1, generic steps with placeholders (`\<Group name\>`) instead of concrete values, either numbered steps directly or one `##` per method, and a final `## References` (plural) with one link per paragraph; link text = page title of the target.

## Methods

* If a task can be done in several ways (desktop, web portal, PowerShell, admin tool), give instructions for all of them. With only one way, use no method heading; start directly with the sentence naming the machine or portal.
* Method headings are exactly one level below their parent. Each PowerShell module is a separate method at the same level (`### Microsoft Graph PowerShell`, `### Microsoft Entra PowerShell`), not grouped under a general `PowerShell` heading. With only one PowerShell method, the heading is `### PowerShell`.
* Each method starts with the sentence naming the machine or portal.

## Step wording

* One imperative action per step, location context first: `In SharePoint admin center, click **Active sites**.`
* Start a step with `In <page/panel/dialog>,` only when the location differs from the previous step. After switching tabs, the first step starts with `On the tab <Name>,`. Never start with `On the page`.
* A step that opens a new page, panel, or dialog is followed by a step starting with `In <that page/panel/dialog>,`. If an action significantly changes the view (e.g. sorting a table), the next action is a separate step.
* After signing in, state where the user is: `After signing in, you are in the **Microsoft Entra admin center**, on the home page.`
* Verbs: *click*, *type*, *select*, *activate*/*deactivate* (checkboxes, switches), *clear* (checkboxes), *find and click* (people pickers, search fields), *navigate to*, *execute* (scripts), *sign in as*, *sign out*.
* Several clicks in a path: `click **Sites**, **Active sites**`.
* Icons without text: `click the *Settings* icon (the gear icon)`.
* Window, dialog, page, and tab names in the location part are not bold. Message boxes are quoted verbatim without quotation marks: `In the message box Remove user?, click **Remove**.`
* Verifications and expected results are never separate steps; they are indented paragraphs below the step: `Verify that the user is listed.`
* Notes are paragraphs (indented inside a step) with an italic label: `*Note:* ...` or `*Important:* ...`. No GitHub admonitions.

## Formatting

* **Bold** everything the user clicks, types, selects, or must recognize exactly: interacted UI elements, values to enter, names of users, groups, sites, and files, app names, machine names, accounts, URLs, file paths. UI elements that are only read are not bold.
* Numbered lists always use `1.` for every item. Bullets use `*`, not `-`.
* Nested content (sub-lists, code, tables, notes, links, figures) is indented by 4 spaces and separated from the step by blank lines.
* Placeholders in angle brackets with backslashes: `**admin@\<your tenant\>.onmicrosoft.com**`. Escape asterisks in running text: `**Word Template (\*.dotx)**`.
* Pipe tables with a header row, padded for alignment, for values to enter (names, groups, settings, expected results).
* In running text, write `lab` and `practice` in lowercase (`If you skipped lab [...]`). Capitalize them only in the H1 prefix (`Lab:`, `Practice:`) and when starting a sentence.
* One H1 per file, then `##`, `###`, `####`. Blank line before and after headings, paragraphs, lists, tables, and code blocks. The file ends with a single newline.

### Links and figures

* All links to other files in the repository use relative paths, never absolute paths starting with `/`: `../General/Managing-site-groups.md` from a lab or practice, `./Other-lab.md` or just `Other-lab.md` within the same folder, `../../images/<file>.png` for images.
* Always include the `.md` extension and the exact capitalization of the file name.
* Link text is the H1 of the target without the `Lab:` or `Practice:` prefix: `[Managing site groups](../General/Managing-site-groups.md)`.
* Links to general instructions go in an indented paragraph below the step.
* Links to other labs or practices, for example in Setup, use the same relative form: `[Get started](./Get-started.md)`.
* Anchors are GitHub style: lowercase, spaces to hyphens, punctuation removed (`#task-2-create-groups`). Link only to headings in files of this repository, and re-check all anchors when renaming a heading.
* External links point to the stable page without tracking parameters or session-specific parts and use one locale consistently (for example `en-us`). Link text is the page title of the target.
* After renaming or moving files, search the repository for the old file name and fix all links. Where possible, run a link checker (for example `lychee` or `markdown-link-check`) locally or in CI.
* Figures are reference-style with descriptive alt text: `![<Alt text>][figure 1]`, referenced in text as `like in [figure 1]`. Figure captions are written in italics on the line directly below the image, in the form `*Figure 1: <Caption>*`, everywhere without exception. Definitions at the end of the file, lowercase `figure`, relative paths: `[figure 1]: ../../images/<file>.png`.

### Scripts and code

* Code blocks use four backticks with a language identifier, indented by 4 spaces inside steps. Longer explanations use block comments (`<# ... #>` in PowerShell).
* Values the user must enter stay empty with a comment: `$tenantName = '' # Between the quotes insert your tenant name`.
* Long commands use line continuation, one parameter per line; in PowerShell backticks and `-Parameter:$value` syntax.
* End PowerShell procedures that open a session with a disconnect step (e.g. `Disconnect-MgGraph`, `Disconnect-PnPOnline`).

## Repository specifics

* Course: Implementing and administering SharePoint Online and OneDrive for Business.
* Scenario company: **Contoso**. Standard users: Lynne Robbins (`LynneR`), Debra Berger, Irvin Sayers, Adele Vance, Patti Fernandez.
* Lab machine: **WIN1**. Practices start with `Sign in to **WIN1** as **Administrator**.`
* Catch-up sentence for skipped labs (use verbatim): `If you skipped lab [Get started with SharePoint administration](Get-started-with-SharePoint-administration.md), in **PowerShell** or **Windows PowerShell**, execute **C:\LabResources\Solutions\Start-SharePointAndTeamsConfiguration.ps1**. If you are asked to sign in, use the global administrator credentials of your tenant.`
* Scripts used in setup steps live under `C:\LabResources\Solutions\`.
* Link check: `lychee --config lychee.toml '**/*.md'` (also runs in GitHub Actions, see `.github/workflows/link-check.yml`). Run it after renaming or moving files.
