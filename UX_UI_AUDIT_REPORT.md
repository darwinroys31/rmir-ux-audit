# RMIR System — Comprehensive UX/UI Audit Report

**Date:** 2026-04-10
**System:** Supplier RMIR (Request for Material Information Record)
**Modules Reviewed:** RMIR Field Management, RMIR Form Creation
**User Flow:** Admin creates fields → builds template → sends to supplier → supplier submits data

---

## Table of Contents

1. [Screen-by-Screen Analysis](#screen-by-screen-analysis)
2. [Overall UX Gaps](#overall-ux-gaps)
3. [Suggested Improved Flow](#suggested-improved-flow)
4. [Priority Matrix](#priority-matrix)

---

## Screen-by-Screen Analysis

---

### Screen 1: RMIR Field Management — Main View

**Description:** The primary screen for managing fields within RMIR sections. Shows a left sidebar navigation (RMIR Form Creation, RMIR Field Management), a main content area with an "EDITED SECTION" card (subtitle: TESTING), and a table of available fields with columns: Field Name, Field Description, Mandatory, Actions. Buttons include "Add Section", "+ Add group", and "+ Add Field".

#### UX Issues
| # | Issue | Severity |
|---|-------|----------|
| 1 | **No clear onboarding or empty-state guidance** — A new admin landing here has no help text, tooltip, or wizard explaining the workflow (create section → add fields → build form). | High |
| 2 | **Section naming is confusing** — "EDITED SECTION / TESTING" appears to be test data, but there is no clear indication of section status (draft, active, published). Admins cannot tell what state a section is in. | High |
| 3 | **No drag-and-drop reordering** — Fields inside a section cannot be reordered visually. The admin must rely on implicit ordering with no control. | Medium |
| 4 | **"Available Items" label is ambiguous** — Does it mean fields available to add, or fields already in the section? The label doesn't clarify. | Medium |
| 5 | **No search or filter** for fields within a section — If sections grow large, finding a specific field is tedious. | Medium |
| 6 | **Cognitive overload from flat hierarchy** — Sections, groups, and fields all appear at the same level. There is no visual nesting to convey the hierarchy (Section → Group → Field). | High |

#### UI Issues
| # | Issue | Severity |
|---|-------|----------|
| 1 | **Inconsistent button styles** — "Add Section" is a filled primary button (top-right), "+ Add group" is an outlined button, and "+ Add Field" is a filled button. Three different visual treatments for similar-level actions creates confusion about hierarchy. | Medium |
| 2 | **Icon-only action buttons** (edit ✏️, delete 🗑️, collapse ∧) lack labels or tooltips — Violates accessibility standards; icons alone are ambiguous. | High |
| 3 | **Table column alignment** — "Mandatory" column shows "No" as plain text; a toggle or visual indicator (✓/✗ icon) would be more scannable. | Low |
| 4 | **Left sidebar navigation** — Active state ("RMIR Field Management") uses a subtle blue highlight that may not be accessible for color-blind users. Needs stronger contrast or an active indicator (bold, underline, or icon). | Medium |
| 5 | **Section card has excessive whitespace** between the header and the table content below. | Low |
| 6 | **Breadcrumb** ("RMIR Form > RMIR Field Management") uses a ">" character instead of a proper chevron icon, appearing inconsistent with modern UI patterns. | Low |

#### Improvements
- Add a **stepper/wizard indicator** at the top showing "1. Create Sections → 2. Add Fields → 3. Build Form → 4. Send to Supplier"
- Add **section status badges** (Draft, Active, Archived)
- Replace icon-only action buttons with **icon + label** buttons or add persistent tooltips
- Implement **drag-and-drop reordering** for fields and sections
- Add an **inline search/filter bar** above the fields table
- Use **visual nesting** (indentation, tree lines, or cards-within-cards) to show Section → Group → Field hierarchy
- Standardize all "Add" actions to use a consistent button style

---

### Screen 2: Add Field Modal

**Description:** A modal/side-panel for adding a new field to a section. Contains: Field Type (dropdown, required), Field Label (text input, max 50 chars, required), a live Preview panel showing a rendered RMIR Form preview, Field Description (optional textarea), and a Mandatory toggle.

#### UX Issues
| # | Issue | Severity |
|---|-------|----------|
| 1 | **No field type visible by default** — The "Field Type" dropdown appears empty. The user must guess what types are available before selecting. A default selection or type gallery would reduce friction. | High |
| 2 | **No validation rules configuration** — There is no way to set min/max length, regex patterns, numeric ranges, or file size limits. Admins can only set "Mandatory" — all other validation must be handled elsewhere or not at all. | High |
| 3 | **Character counter placement** — "Enter label (max 50 chars)" is inside the placeholder. Once the user starts typing, this guidance disappears. Should be a persistent helper text below the input. | Medium |
| 4 | **Preview panel is static** — The preview shows a generic "Enter your answer" placeholder. It doesn't dynamically reflect the field type selected (e.g., showing a dropdown, checkbox, date picker, file upload). | Medium |
| 5 | **No "Save and Add Another" option** — Admin must close the modal and reopen it for each field, adding repetitive clicks when building forms with many fields. | Medium |
| 6 | **Mandatory toggle has no explanation** — No helper text explaining what happens when a field is mandatory (e.g., supplier cannot submit without filling it). | Low |

#### UI Issues
| # | Issue | Severity |
|---|-------|----------|
| 1 | **Modal width is narrow** — The preview panel and form fields compete for horizontal space, making both feel cramped. | Medium |
| 2 | **"Discard" button placement** — There is a "Discard" text/button that appears detached from the modal, creating confusion about what it discards (the field? the entire section?). | High |
| 3 | **Preview section header** says "RMIR Form" generically — It should say "Field Preview" or "Live Preview" to be clear. | Low |
| 4 | **No clear visual separation** between the form inputs and the preview panel — They blend together. | Medium |
| 5 | **Missing Cancel/Save buttons** in a prominent, consistent location — The action buttons are not clearly visible at the bottom of the modal. | Medium |

#### Improvements
- Add a **field type gallery** (visual grid of type icons: Text, Number, Dropdown, Date, File Upload, etc.) instead of a plain dropdown
- Add **validation rules configuration** section: min/max length, pattern, allowed file types, numeric range
- Make the preview **dynamic** — reflect the actual field type in real-time
- Add **"Save & Add Another"** button alongside "Save"
- Move character counter to **persistent helper text** below inputs
- Add a clear, consistent **button bar** at the modal footer (Cancel | Save | Save & Add Another)
- Add helper text to the Mandatory toggle: "When enabled, suppliers must complete this field before submission"

---

### Screen 3: Add New Group Modal

**Description:** A modal for creating a new group within a section. Contains: Group Name (text input, required, 0/50 char counter), Group Description (optional textarea).

#### UX Issues
| # | Issue | Severity |
|---|-------|----------|
| 1 | **No explanation of what a "group" is** — New admins won't understand the difference between a section and a group. There is no contextual help, tooltip, or info icon. | High |
| 2 | **No visual preview** of how the group will appear in the final form — Unlike the Add Field modal which has a preview panel, this modal has none. | Medium |
| 3 | **No option to add fields directly during group creation** — Admin must create the group, close the modal, then separately add fields to it. This breaks the mental model of "group = collection of fields." | Medium |

#### UI Issues
| # | Issue | Severity |
|---|-------|----------|
| 1 | **Character counter format** — Shows "0/50" which is fine, but the placement varies from the Add Field modal's approach (placeholder text vs. counter). Inconsistent pattern. | Low |
| 2 | **Modal is very sparse** — Only two fields with lots of empty space. Feels unfinished. | Low |
| 3 | **Missing action buttons or they're below the visible area** — Cancel/Save buttons aren't clearly visible. | Medium |

#### Improvements
- Add an **info tooltip/popover** next to "Group" explaining: "Groups organize related fields together within a section. Suppliers will see grouped fields under a shared heading."
- Add a **preview panel** consistent with the Add Field modal
- Allow **adding fields inline** during group creation (optional)
- Ensure **consistent character counter** styling across all modals

---

### Screen 4: Allow Multiple Entries Toggle

**Description:** A section of the group configuration showing an "Allow Multiple Entries" toggle with an info (?) icon, and a toggle switch (currently off).

#### UX Issues
| # | Issue | Severity |
|---|-------|----------|
| 1 | **Toggle context is unclear** — "Allow Multiple Entries" is shown in isolation. It's not obvious what "entries" refers to (multiple values per field? multiple rows of the group? multiple submissions?). | High |
| 2 | **Info icon (?) requires hover/click** — Critical configuration like this should have inline explanation, not hidden behind an icon. | Medium |
| 3 | **No preview of multiple-entry behavior** — Admin can't visualize what the supplier will see when this is enabled. | Medium |

#### UI Issues
| # | Issue | Severity |
|---|-------|----------|
| 1 | **Toggle is visually disconnected** from the group modal — It appears as a standalone element rather than part of a cohesive form. | Medium |
| 2 | **Minimal vertical spacing** — The toggle feels cramped against surrounding elements. | Low |

#### Improvements
- Add **inline description**: "When enabled, suppliers can add multiple rows of data for this group (e.g., multiple ingredients, multiple certifications)."
- Show a **mini-preview** illustrating single-entry vs. multiple-entry behavior
- Ensure toggle is visually grouped within the parent Group modal

---

### Screen 5: RMIR Form Creation — Form List

**Description:** The main form list view showing existing RMIR form templates. Includes a left sidebar navigation, a search bar, a "Create RMIR Form" button, and a table with columns: Form Name, Form Description, Created On, Template (with "Preview Form" links), and an actions column. Shows sample data including "Laundry & Homecare", "Beauty Product", "AutomationRMIR", "Demo purpose". Pagination at bottom: "Items per page 10, Page 1 of 32, Total Items: 311".

#### UX Issues
| # | Issue | Severity |
|---|-------|----------|
| 1 | **No form status column** — Cannot tell if a form is Draft, Active, Sent to Supplier, or Archived. This is critical for workflow management. | High |
| 2 | **No bulk actions** — With 311 forms, there's no way to bulk delete, archive, or duplicate forms. | Medium |
| 3 | **No sorting indicators are active** — Column headers have sort icons (↑↓) but no indication of current sort order. | Medium |
| 4 | **"Preview Form" is the only action** — No Edit, Duplicate, Delete, or Send options visible in the table row. Admin must navigate elsewhere for these actions. | High |
| 5 | **Search is basic** — No advanced filters (by date range, by status, by creator). With 311 forms, finding a specific one requires knowing its name. | Medium |
| 6 | **Truncated form names** — "Laundry & Homecare - H..." and "AutomationRMIR_1773639..." are cut off with no way to see the full name without clicking. | Medium |
| 7 | **No "Last Modified" or "Last Sent" date** — Only "Created On" is shown. For ongoing form management, knowing when a form was last updated is essential. | Medium |

#### UI Issues
| # | Issue | Severity |
|---|-------|----------|
| 1 | **Table is visually dense** — Rows lack sufficient vertical padding, making it hard to scan. | Medium |
| 2 | **Pagination controls** are small and use plain text links — Could benefit from more prominent, touch-friendly buttons. | Low |
| 3 | **No hover state** visible on table rows — No visual feedback when the user mouses over a row. | Low |
| 4 | **"Create RMIR Form" button** is positioned next to the search bar — Could be confused with a search action. Should be more prominently positioned or styled differently. | Low |
| 5 | **Template column** only shows "Preview Form" as a text link — Inconsistent with other buttons in the system. | Low |

#### Improvements
- Add a **Status column** with badges: Draft (gray), Active (green), Sent (blue), Archived (yellow)
- Add **row-level actions** menu (⋮): Edit, Duplicate, Archive, Delete, Send to Supplier
- Add **bulk selection** with checkboxes and bulk action bar
- Add **advanced filters**: date range picker, status filter, creator filter
- Show full form names on **hover tooltip** or expand row
- Add **"Last Modified"** column
- Increase table row height and add **alternating row colors** or subtle dividers for scannability

---

### Screen 6: Create RMIR Form — Form Builder

**Description:** The form creation screen where an admin names a new RMIR form. Contains: Name field (required, 0/50 char counter), Description field (required, 0/100 char counter), and a "Fields to Display" section showing expandable sections (e.g., "EDITED SECTION") with checkboxes to select fields.

#### UX Issues
| # | Issue | Severity |
|---|-------|----------|
| 1 | **"Fields to Display" is confusing** — It shows sections from Field Management but the interaction model is unclear. Are you selecting individual fields? Entire sections? How are groups handled? | High |
| 2 | **No preview of the final form** during creation — Admin is building blind; they can't see what the supplier will experience until after saving. | High |
| 3 | **Name limit of 50 characters may be too short** — For descriptive form names like "Laundry & Homecare - Home Cleaning Products - Q4 2026", 50 characters will frequently be exceeded. | Medium |
| 4 | **Description limit of 100 characters is very restrictive** — Descriptions often need more space to explain purpose, deadline, or instructions. | Medium |
| 5 | **No template/duplication option** — Admin must build each form from scratch. No "duplicate existing form" or "start from template." | High |
| 6 | **No save-as-draft** — It's unclear if partial progress can be saved. | Medium |

#### UI Issues
| # | Issue | Severity |
|---|-------|----------|
| 1 | **Large empty space** below the form fields — The screen feels unfinished. | Low |
| 2 | **Section checkboxes** use accordion-style collapse but the expand/collapse affordance is subtle. | Medium |
| 3 | **No clear submit/save button visible** — The primary action button is not prominent in the viewport. | Medium |
| 4 | **Breadcrumb** ("sophie > RMIR Form > Create RMIR Form") includes the username "sophie" — This is inconsistent and potentially confusing. The breadcrumb should show navigation path, not the logged-in user. | Medium |

#### Improvements
- Add a **live form preview** panel (split-screen or toggle) showing the supplier view
- Implement **"Duplicate Form"** action from the form list
- Increase character limits: Name to 100, Description to 500
- Add **drag-and-drop** for reordering selected sections/fields
- Add a **"Select All / Deselect All"** option for field selection
- Make the save/submit button **sticky at the bottom** of the viewport
- Fix breadcrumb to show **navigation path only**, not username

---

### Screen 7: Form Field Selection & Preview — Detailed View

**Description:** The lower portion of the form creation screen showing the expanded sections and their fields. Shows sections like "TESTING" with fields (Product name, Concentration), a multi-line text area field with sample text, a "333 sample" group with "No fields in this group" message, and an "EIGHT / EIGHT FOR TESTING" section with "Selected Fields: 0". Various field types are visible including text inputs and text areas.

#### UX Issues
| # | Issue | Severity |
|---|-------|----------|
| 1 | **"No fields in this group" is a dead end** — There's no inline action to add fields from here. Admin must navigate back to Field Management. | High |
| 2 | **"Selected Fields: 0" provides no guidance** — When a section has no selected fields, there should be a CTA or explanation of how to populate it. | Medium |
| 3 | **Test/dummy data visible** — Names like "333 sample", "qq", "dwasq", "EIGHT" suggest either test data pollution or no naming validation. This hurts credibility and usability. | Medium |
| 4 | **Multi-line text preview** shows a long test string with no formatting — It's unclear if rich text or markdown is supported. | Low |
| 5 | **No field-level configuration override** — Admin can't customize field labels or make fields mandatory at the form level (only at the field management level). | Medium |

#### UI Issues
| # | Issue | Severity |
|---|-------|----------|
| 1 | **Inconsistent section card styling** — Some sections show as expanded cards with content, others show collapsed with just "Selected Fields: 0". The visual treatment differs. | Medium |
| 2 | **Dense layout** — Field previews are stacked tightly with minimal spacing between them. | Low |
| 3 | **Checkbox alignment** varies across sections. | Low |
| 4 | **Section expand/collapse** iconography is inconsistent with other parts of the UI. | Low |

#### Improvements
- Add **inline "Go to Field Management"** link when a section/group has no fields
- Add **field count summary** per section: "3 of 5 fields selected"
- Allow **form-level overrides**: rename fields, change mandatory status, add conditional logic
- Add **field type icons** next to each field name for quick identification
- Implement **consistent card styling** across all sections regardless of content

---

## Overall UX Gaps

### 1. **No End-to-End Flow Visibility** — Priority: 🔴 High
The system lacks a clear, visible workflow showing where the admin is in the process. There is no stepper, progress bar, or status tracker. The relationship between Field Management → Form Creation → Supplier Submission is implicit and never visualized.

### 2. **Disconnected Modules** — Priority: 🔴 High
RMIR Field Management and RMIR Form Creation operate as separate, siloed screens. Changes in one aren't immediately reflected in the other. There's no cross-linking (e.g., from a form back to its field definitions, or from a field to all forms using it).

### 3. **No Supplier-Side Preview** — Priority: 🔴 High
At no point can the admin see exactly what the supplier will experience. The "Preview Form" link in the form list is the closest feature, but it's not available during form creation when it's most needed.

### 4. **Missing Form Lifecycle Management** — Priority: 🔴 High
There is no concept of form status (Draft → Active → Sent → Completed → Archived). Admins cannot track which forms have been sent, to whom, or what the completion rate is.

### 5. **No Validation Framework** — Priority: 🔴 High
Fields can only be marked as "Mandatory." There are no other validation types: numeric ranges, date ranges, regex patterns, file type restrictions, conditional required fields, or cross-field validation.

### 6. **No Collaboration Features** — Priority: 🟡 Medium
No audit trail of who created/edited what, no commenting system, no approval workflow for form templates, no version history.

### 7. **No Data Import/Export** — Priority: 🟡 Medium
No ability to import field definitions from spreadsheets or export form templates. This is critical for organizations managing hundreds of forms.

### 8. **No Conditional Logic** — Priority: 🟡 Medium
No show/hide logic for fields based on other field values. Example: "If product type = Chemical, show Hazard Classification field."

### 9. **Accessibility Deficits** — Priority: 🟡 Medium
- Icon-only buttons without labels or ARIA attributes
- Color-only state indicators
- No visible focus indicators
- Small touch targets on pagination and action icons
- No keyboard navigation support visible

### 10. **No Help System** — Priority: 🟡 Medium
No contextual help, tooltips on complex features, onboarding flow, or documentation links.

---

## Suggested Improved Flow

### Current Flow (As-Is)
```
Admin opens Field Management
  → Creates a Section (no guidance)
  → Adds Fields one-by-one (no bulk)
  → Switches to Form Creation
  → Creates a Form
  → Selects fields blindly
  → Previews (only from list, post-creation)
  → Sends to supplier (mechanism unclear)
```

### Recommended Flow (To-Be)
```
1. DASHBOARD (New)
   ├── Quick stats: Forms sent, Pending responses, Completion rate
   ├── Recent activity feed
   └── Quick actions: "Create New Form", "Manage Fields"

2. FORM BUILDER (Redesigned — Unified)
   ├── Step 1: Basic Info
   │     ├── Form Name, Description, Category
   │     └── Option: "Start from Template" / "Duplicate Existing"
   ├── Step 2: Build Structure
   │     ├── Add/Reorder Sections (drag-and-drop)
   │     ├── Add/Reorder Groups within Sections
   │     └── Add/Configure Fields within Groups
   │           ├── Field Type (visual gallery)
   │           ├── Validation Rules
   │           ├── Conditional Logic
   │           └── Live Preview (split-screen)
   ├── Step 3: Review & Preview
   │     ├── Full supplier-view preview
   │     ├── Validation summary
   │     └── Field count & completeness check
   └── Step 4: Publish & Send
         ├── Select suppliers
         ├── Set deadline
         ├── Add instructions/message
         └── Send (with confirmation)

3. FIELD LIBRARY (Refined)
   ├── Reusable field definitions with categories
   ├── Search, filter, tag fields
   ├── See which forms use each field
   └── Bulk import/export

4. FORM TRACKING (New)
   ├── Status per supplier: Not Started → In Progress → Submitted → Reviewed
   ├── Reminders & notifications
   ├── Completion analytics
   └── Export collected data
```

---

## Priority Matrix

### 🔴 High Priority (Address Immediately)

| # | Item | Screen(s) | Impact |
|---|------|-----------|--------|
| 1 | Add form status/lifecycle management (Draft, Active, Sent, Archived) | Form List, Form Builder | Without this, admins cannot manage form workflow |
| 2 | Add supplier-side live preview during form creation | Create RMIR Form | Admins build forms blind; high error rate |
| 3 | Add field validation rules (beyond Mandatory) | Add Field Modal | Data quality from suppliers will be poor |
| 4 | Add row-level actions in form list (Edit, Duplicate, Delete, Send) | Form List | Currently only "Preview" is available; crippled management |
| 5 | Add workflow stepper/progress indicator | All screens | Users don't understand the end-to-end process |
| 6 | Fix Section → Group → Field hierarchy visualization | Field Management | Flat hierarchy causes confusion |
| 7 | Add accessible labels to icon-only buttons | Field Management | Accessibility compliance failure |
| 8 | Add "Duplicate Form" capability | Form List / Create Form | With 311 forms, building from scratch each time is unacceptable |
| 9 | Add inline guidance for empty states ("No fields in this group") | Form Field Selection | Dead-end states block user progress |
| 10 | Clarify "Discard" button scope and placement | Add Field Modal | Risk of accidental data loss |

### 🟡 Medium Priority (Next Sprint)

| # | Item | Screen(s) | Impact |
|---|------|-----------|--------|
| 1 | Add advanced search and filters (date, status, creator) | Form List | 311 forms is unmanageable with basic search |
| 2 | Add "Save & Add Another" for field creation | Add Field Modal | Reduces repetitive clicks during bulk creation |
| 3 | Add drag-and-drop reordering for fields and sections | Field Management, Form Builder | No reordering = rigid form structure |
| 4 | Standardize button styles across all modals and screens | All screens | Visual inconsistency hurts trust |
| 5 | Add contextual help/tooltips for Groups and Multiple Entries | Add Group Modal, Toggle | Concepts are not self-explanatory |
| 6 | Add "Last Modified" column to form list | Form List | "Created On" alone is insufficient |
| 7 | Increase character limits (Name: 100, Description: 500) | Create RMIR Form | Current limits are too restrictive |
| 8 | Add bulk field selection ("Select All / Deselect All") | Form Field Selection | Tedious for large sections |
| 9 | Fix breadcrumb to exclude username | Create RMIR Form | Breadcrumb shows "sophie" which is confusing |
| 10 | Add field type icons in field selection view | Form Field Selection | No visual differentiation between field types |

### 🟢 Low Priority (Backlog)

| # | Item | Screen(s) | Impact |
|---|------|-----------|--------|
| 1 | Add alternating row colors in tables | Form List, Field Management | Minor readability improvement |
| 2 | Replace ">" breadcrumb separator with chevron icon | All screens | Minor visual polish |
| 3 | Add hover tooltips for truncated form names | Form List | Nice-to-have for long names |
| 4 | Add rich text support for field descriptions | Add Field Modal | Low-frequency need |
| 5 | Add form creation analytics dashboard | New screen | Valuable but not blocking |
| 6 | Add conditional logic for fields | Form Builder | Complex feature, high value but high effort |
| 7 | Add data import/export for field definitions | Field Library | Batch operations optimization |
| 8 | Add version history for forms | Form Builder | Audit trail enhancement |
| 9 | Add collaboration features (comments, approvals) | All screens | Team workflow enhancement |
| 10 | Improve pagination controls with touch-friendly buttons | Form List | Minor usability improvement |

---

## Summary Statistics

| Category | Count |
|----------|-------|
| Total Screens Analyzed | 7 |
| UX Issues Identified | 32 |
| UI Issues Identified | 24 |
| High Priority Items | 10 |
| Medium Priority Items | 10 |
| Low Priority Items | 10 |
| Missing Features | 12 |

---

*Report generated from analysis of RMIR Screens.pdf and provided screen images.*
