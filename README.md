# wonky-file-input
A javascript enhancement for file input with multiple attribute.

# TODO list and checks

- Max file size helper and message if exceeds
- allowed filetypes helper and message if not complies
  - show what types are allowed?
 
 

## Core (use native if you can)

* [ ] **Use `<input type="file" multiple>`** (don’t replace it with a div).

  * WCAG: 4.1.2 Name/Role/Value, 1.3.1 Info & Relationships
* [ ] **Programmatic label** via `<label for>` with a clear purpose (“Upload files”).

  * WCAG: 2.5.3 Label in Name, 1.3.1, 3.3.2 Labels/Instructions
* [ ] **Instructions near the control** (types, size limits, count limits, confidentiality notes).

  * WCAG: 3.3.2
* [ ] **Required?** Use the `required` attribute (or `aria-required="true"` if truly custom) and explain what “required” means.

  * WCAG: 3.3.2, 3.3.1 Error Identification

## Keyboard & Focus

* [ ] **Fully operable with keyboard** (Tab to focus, Enter/Space opens picker, delete/remove actions reachable).

  * WCAG: 2.1.1 Keyboard, 2.1.2 No Keyboard Trap
* [ ] **Logical focus order** (label → control → list of selected files → action buttons).

  * WCAG: 2.4.3 Focus Order
* [ ] **Visible focus indicator** that’s easy to see. If following WCAG 2.2, meet Focus Appearance (Minimum).

  * WCAG: 2.4.7 Focus Visible; (2.2+) 2.4.11 Focus Appearance (Minimum)

## Multiple selection UX

* [ ] **Selected files are exposed in the UI** as a list/table that a screen reader can reach.

  * WCAG: 1.3.1, 4.1.2
* [ ] **Each file has an individual “Remove” button** with an accessible name that includes the filename (e.g., “Remove report.pdf”).

  * WCAG: 4.1.2, 2.5.3 Label in Name
* [ ] **Announce changes** when files are added/removed (polite live region or status text near the control).

  * WCAG: 4.1.3 Status Messages
* [ ] **Prevent surprise navigation**—actions like “Remove all” should not steal focus or reload pages.

  * WCAG: 3.2.2 On Input

## Errors, validation, and help

* [ ] **Reject disallowed files (type/size/count)** and show **specific** error messages (“.zip not allowed”, “Max 10 files”, “Image must be ≤ 5 MB”).

  * WCAG: 3.3.1 Error Identification, 3.3.3 Error Suggestion
* [ ] **Associate errors to the control** via `aria-describedby` or inline markup; don’t rely on color alone.

  * WCAG: 1.4.1 Use of Color, 3.3.1
* [ ] **Progress feedback** for long uploads (use a live region or `<progress>` with `aria-valuenow`).

  * WCAG: 4.1.3, 1.3.1

## Contrast & sizing

* [ ] **Text contrast**: normal text ≥ 4.5:1, large text ≥ 3:1; icons & borders (non-text) ≥ 3:1 against adjacent colors.

  * WCAG: 1.4.3 Contrast (Minimum), 1.4.11 Non-Text Contrast
* [ ] **Hit targets** (buttons like “Browse”, “Remove”) are at least \~24×24 CSS px if following WCAG 2.2 AA Target Size.

  * WCAG (2.2+): 2.5.8 Target Size (Minimum)

## Announcements & SR text

* [ ] Provide short **sr-only guidance** for multi-select (e.g., “You can select multiple files in the dialog”).

  * WCAG: 3.3.2 Labels/Instructions
* [ ] When the native picker returns a list, announce **how many files** were chosen (“3 files selected”).

  * WCAG: 4.1.3 Status Messages

## Drag-and-drop (if you add a dropzone)

* [ ] **Keyboard alternative** to drag (e.g., the standard “Browse” button) and/or click-to-select.

  * WCAG: 2.1.1 Keyboard, 2.5.1 Pointer Gestures
* [ ] **Dragging is not required**; provide a single-pointer alternative (click).

  * WCAG (2.2+): 2.5.7 Dragging Movements
* [ ] Dropzone has an informative label/role (e.g., group with a labelled heading); announce “Drop files to upload”.

  * WCAG: 1.3.1, 4.1.2
* [ ] **Focus styles** and **contrast** on the dropzone border/label meet the same rules as above.

  * WCAG: 1.4.11, 2.4.7/(2.4.11)

# Robustness & semantics (for custom widgets)

* [ ] If you wrap the native input with a custom button, **keep the real file input in the DOM**, visible to AT, and forward focus correctly.

  * WCAG: 4.1.2, 1.3.1
* [ ] Don’t **override the role** of the file input; avoid `role="button"` on it.

  * WCAG: 4.1.2
* [ ] Keep **state exposed** (e.g., number of files selected) either in the control’s value text or via a nearby live region that updates.

  * WCAG: 4.1.2, 4.1.3

## Nice-to-have (but helpful)

* [ ] **Preview list** shows filename and type/size; make previews optional and screen-reader friendly (alt text like “Preview of photo.jpg”).
* [ ] **Cancel/Retry** buttons for failed uploads, keyboard reachable, properly named.
* [ ] **Persisted constraints** (`accept`, server-side validation) match what you tell the user.

---

### Minimal accessible pattern (HTML skeleton)

```html
<label for="files">Upload files (PDF, JPG). Max 10 files, each ≤ 5 MB.</label>
<input id="files" name="files" type="file" multiple aria-describedby="files-help files-status" accept=".pdf,.jpg,.jpeg,image/jpeg,application/pdf" required>

<div id="files-help">You can select multiple files in the dialog.</div>

<ul id="selected-files" aria-live="polite" aria-relevant="additions removals">
  <!-- Inject <li>File name <button aria-label="Remove report.pdf">Remove</button></li> -->
</ul>

<div id="files-status" aria-live="polite"></div>
```

If you want, I can turn this into a printable checklist (or a tiny test page) that you can run your component against.
