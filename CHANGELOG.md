# Changelog

All notable changes to this project are documented in this file.

---

## [1.6.0] – 2026-02-26
**Highlights:** Import system (SQL DDL, CSV/TSV files, mappings, catalog items, preset bundles), meta-only category tags, comprehensive shortcuts reference, mapping terminology

### Import system
- **SQL DDL import**: **Import → Import SQL/DDL…** parses `CREATE TABLE` statements from pasted SQL or uploaded `.sql` files. Each table becomes a column; each SQL column becomes a field. Auto-detects data types, PRIMARY KEY, NOT NULL, UNIQUE, FOREIGN KEY, AUTO_INCREMENT, and DEFAULT values. Creates or reuses a Data Type attribute, Nullable attribute, and standard tags (Primary Key, Foreign Key, Required, Unique). Supports MySQL, PostgreSQL, SQL Server, and Oracle syntax including quoted identifiers, schema prefixes, and IF NOT EXISTS
- **CSV/TSV file import**: **Import → Import CSV/TSV file…** uploads a file and shows an interactive column mapping UI. Each CSV column gets a role dropdown: Label, ID, Parent (nesting), Column (grouping), Note, Tag, Skip, or Custom attribute. Auto-detects common header names. Import into new columns or an existing column. Supports comma, tab, and semicolon separators with quoted field parsing
- **Import mappings**: **Import → Import mappings…** creates mappings between existing fields from pasted text or uploaded CSV/TSV files. Multi-strategy field resolution: exact ID, `column.label`, or unambiguous label. Supports cardinality, labels, notes, defaults, tags, transforms, and extra columns as custom attributes. Compatible with **Export CSV** output for round-tripping
- **Catalog import**: import tags, transforms, and attributes from pasted text or uploaded files. Supports plain lines and tab-separated formats with auto-detection. Match & merge: items matched by ID or label show **new** / **will update** / **exists — no changes** badges. TSV imports support `id` and `tag`/`tags` columns
- **Preset bundles**: four domain presets (Database, API/JSON, Data Governance, ETL/Integration) populate tags, attributes, and transforms in a single click. Per-catalog presets bar in individual import modals

### Import infrastructure
- **TSV parent column**: field and column TSV imports recognize a `parent` column for multi-level nested hierarchies
- **TSV column import**: Import Columns supports tab-separated format with `column`, `parent`, and extra columns for tags/attributes
- **Auto-create attributes**: unrecognized TSV columns automatically create custom attributes and values
- **Tab indentation**: all import textareas intercept Tab/Shift+Tab for 4-space indent/outdent
- **Import file upload**: all import modals include a file upload button (.csv/.tsv/.txt)

### Meta-only tags
- **Meta-only tags**: **Meta only** checkbox marks tags as category headers, hidden from node/mapping selectors. Dropdowns group items under labeled optgroup sections
- **Category assignment**: catalog items (tags, attributes, transforms) can only be tagged with meta-only category tags

### Shortcuts & UI
- **Keyboard & mouse shortcuts reference**: expanded from 6 to 11 sections — now covers click modifiers (Ctrl/Shift/Alt+click), edge click modifiers, marquee & lasso (with Shift/Ctrl/Alt combinations), and drag-and-drop modifiers (Move / Map / Copy / Copy+)
- **Mapping terminology**: all user-facing "arrow" and "edge" references updated to "mapping" — Graph menu headers (Show mappings, Mapping scope), button tooltips, filter editor labels, documentation, and quick-start guide
- **Mapping labels layout**: full-width row format with title above, matching other Graph menu sections
- **Preset bundle fix**: status message no longer shows "undefined"

---

## [1.5.0] – 2026-02-25
**Highlights:** Edge tags & attributes, emoji display mode, edge labels, bulk editing, attribute editor UX overhaul

### Edge metadata
- **Edge tags**: mappings now support tags from the shared tag catalog — same tags used on nodes. Add, remove, and manage tags directly in the mapping editor
- **Edge custom attributes**: assign custom attribute values to mappings using the shared attribute catalog. Supports single-select and multi-select attributes, plus inline creation of new attributes and values
- **Edge labels**: mappings now have a **Label** field — a short freeform text rendered directly on the edge line in the viewer at the curve midpoint. Togglable via **Edge labels** selector (Always / Highlight / Off) with icon buttons in the Graph menu. Label show/hide checkbox per mapping
- **Consolidated view**: tag and attribute chips displayed in consolidated and bidirectional edge cards for quick scanning. Tooltips and badge pills in node detail mapping lists

### Emoji system
- **Emoji fields**: tags, transforms, custom attributes, and attribute values now have an optional emoji field with a curated picker palette (😀▾ button)
- **Display mode toggle**: each catalog item has an explicit **Abbr / Emoji** toggle controlling which label is shown in node pills, detail panels, filter chips, and transform badges. Auto-switches when emoji is set or cleared

### Bulk editing
- **Bulk move** (**Alt+↑/↓**): move multiple contiguous siblings up or down as a block
- **Bulk indent/outdent** (**Alt+→/←**): indent or outdent multiple siblings at once
- **Copy & paste** (**Ctrl+C/V**): copy selected node subtrees with deep clone and mapping duplication. Cross-column paste supported
- **Duplicate** (**Ctrl+D**): duplicate selected siblings in-place with full subtree and mapping clone
- **Group selection** (**Ctrl+G**): wrap contiguous selected siblings into a new named group
- **Ungroup** (**Ctrl+Shift+G**): dissolve groups — moves children to parent level. Supports multi-selection (ungroups all selected groups at once)
- **Collapse/expand toggle** (**Space**): toggle on selected group(s), supports multi-selection

### Attribute editor UX
- **Attribute editor redesign**: compact merged rows (Id+Abbr, Emoji+Display), collapsible emoji grid and color swatches behind 😀▾ and 🎨▾ dropdown buttons
- **Inline value creator**: replaced "Add value…" modal with inline input — type a label and press Enter. Auto-generates ID, abbreviation, and priority
- **Drag-and-drop value reordering**: grab the 6-dot handle to reorder values. Full-border blue highlight on drop target. Priority-based ordering
- **Catalog drag handles**: 6-dot grip icons on all catalog cards (filters, tags, attributes, views) indicating drag-to-reorder support

### Bug fixes & polish
- **Multi-select keyboard fix**: all shortcuts (duplicate, group, ungroup, move, indent, outdent, collapse) now work correctly with lasso/marquee multi-selections
- **Browser shortcut conflict fix**: Ctrl+D and Ctrl+G now always preventDefault when the app is focused, preventing browser bookmark and find-next dialogs
- **Auto-ID freeze**: clicking the `auto` badge freezes the ID — stops following label changes. Clearing re-enables auto-follow
- **Context menu expanded**: Copy, Paste, Group selection, and Ungroup actions with keyboard shortcut hints
- **View scope expanded**: views now capture and restore edge label display mode, tag pill visibility, and attribute pill visibility
- **Catalog naming consistency**: "Tag manager" → Tags catalog, "Transformation library" → Transforms catalog
- **Move button consistency**: disabled move arrows show dimmed instead of hidden across all catalogs

---

## [1.4.1] – 2026-02-24
**Highlights:** Top bar icon revamp, columns popover redesign, keyboard shortcut reorganization, platform-aware shortcut display, catalog SVG icon buttons, view auto-deactivation

- **Top bar icons**: New, Open, and Save buttons now show SVG icons with shortened labels. Bright/dark mode toggle uses proper sun/moon SVG icons
- **Editor mode button**: replaced the checkbox+label toggle with a clean button that lights up with golden glow when active
- **Columns popover redesign**: checkboxes replaced with eye/eye-off SVG toggle buttons, hidden columns shown at reduced opacity. Color dots, move arrows, and delete button use SVG icon buttons
- **Keyboard shortcuts reorganized**: all project shortcuts now use the **Alt+** prefix (**Alt+N** new, **Alt+O** open, **Alt+S** save, **Alt+E** editor mode). View shortcuts: **Ctrl+Alt+S** save view, **,** / **.** previous/next view, **Ctrl+Alt+0** reset view. Platform-aware display: Mac shows ⌘⌥⇧ symbols
- **Catalog move buttons**: all ↑↓ text arrow buttons are now SVG icon buttons with consistent sizing and hover states
- **View auto-deactivation**: changing any viewer state automatically deactivates the active view. Debounced 80ms drift check
- **Mac keyboard fix**: Alt+letter project shortcuts now use `e.code` instead of `e.key` — fixes Option+letter producing special characters on Mac
- **Platform-aware shortcut display**: keyboard shortcuts modal, command palette, context menu, and tooltips show Mac symbols on Mac and Ctrl/Alt/Shift on Windows/Linux
- **Transforms sorted alphabetically**: the Transforms catalog now displays entries sorted by label
- **Browser tab title**: changed from "Project — Dunnode" to "Dunnode — Project"
- **View nav edge behavior**: prev/next buttons greyed out instead of hidden at edges

---

## [1.4.0] – 2026-02-24
**Highlights:** Views catalog with inline editing, SVG icon system, context menu redesign, keyboard shortcuts, reset view, view pill indicator

- **Views catalog**: save and restore viewer state snapshots — filters, selection, arrows, collapse state, hidden columns, edge color scheme, node color mode, and more. **Views** toolbar button for one-click apply. **Save current view** (**Alt+S**) captures current state. **Previous view / Next view** (**Alt+,** / **Alt+.**) navigate between saved views. Full catalog management with inline editing, emoji picker, drag-and-drop reordering, and update snapshot. Click an active view to deactivate (toggle off). Tooltips show view notes on hover. Four sample views in the example project
- **View pill indicator**: when a view is active, a compact pill appears in the viewer header showing the emoji + label with ‹/› navigation buttons, an × to deactivate, and a dropdown overlay for quick switching
- **Reset view** (**Alt+0**): clears all filters, search, selection, hidden columns, collapsed groups, arrows, edge colors, node colors, and dim mode — returns to clean-slate state. Available in the Views menu, as an icon button in the viewer toolbar, and in the command palette
- **Project keyboard shortcuts**: **Ctrl+N** new project, **Ctrl+O** open project, **Ctrl+S** save project, **Ctrl+E** toggle editor mode. All shown in tooltips, command palette, and keyboard shortcuts modal
- **SVG icon system**: new shared `ICONS` object with 20+ monochrome SVG icons at consistent stroke weight. Replaces all Unicode text glyphs in context menus, toolbar buttons, dropdown menus, and the multi-select details panel. New `nodeIcon()` helper provides unified diamond (field) and rect-with-header (group) icons across the app
- **Context menu redesign**: tighter layout with section labels (Add, Insert, Arrange), keyboard shortcut hints, transparent backgrounds with hover fills, and SVG icons for every action. Delete uses colored text instead of colored background. Column and node menus both restructured
- **Toolbar menu revamp**: all toolbar buttons (Graph, Layout, Selection, Catalogs, Views, Export, Help) now use SVG icons instead of text glyphs. All dropdown menus now use the `selActionBtn` pattern with SVG icons — matching the Selection menu style established in v1.3.8
- **Viewer controls redesign**: icon buttons above the viewer are now grouped into logical capsules — View actions (pan, clear, reset) and History (undo, redo). All buttons use consistent SVG icons with hover/active states. History group shows/hides with editor mode
- **Layout wrap toggle**: the bare checkbox for "Wrap columns" is now a styled button matching the rest of the Layout menu, with an ON/OFF indicator
- **Keyboard shortcuts**: ↑/↓ arrow navigation, Shift+↑/↓ multi-select, Ctrl+↓/↑ quick-create field below/above with inline rename, Ctrl+Alt+↓/↑ for groups, Ctrl+→ add child, Alt+↑/↓ move node, Tab/Shift+Tab indent/outdent, Enter to focus editor, Delete to remove node
- **Inline rename**: new nodes created via keyboard start with an inline label editor. Type a name and press Enter to commit, Escape to cancel (removes the node), or Ctrl+↓ to commit and create the next field — enabling rapid-fire schema building
- **Field ↔ group conversion**: right-click context menu and command palette entries to convert fields to groups and vice versa (groups must be empty to convert to fields)
- **Cancel button fix**: Cancel in catalog editors now closes immediately without triggering the unsaved changes guard
- **Edit field/group fix**: the context menu "Edit field" / "Edit group" action no longer clears the selection — it directly focuses the node without toggle behavior
- **Opacity popover fix**: the floating panel's opacity slider now renders below the icon row when there is not enough space above (e.g. when the panel is at the top of the screen)
- **About dialog**: new tagline — *"Dunno where your data goes?"* above the DUNNODE wordmark
- **Filter selection clearing**: when filter mode is Hide and selected nodes become hidden, selection is automatically cleared
- **Enter/Escape in all dialogs**: Enter confirms and Escape cancels in all custom alert, confirm, and prompt dialogs
- **Column-level keyboard shortcuts**: when a column header is selected, Ctrl+↓/↑ adds fields to the top/bottom of the column. Arrow keys from column header jump to the first node
- **Browser tab title sync**: the browser tab title now reflects the project title
- **Edge hiding fix**: Direct and Selected highlight modes now correctly hide non-highlighted edges when arrow mode is set to Selected

---

## [1.3.9] – 2026-02-23
**Highlights:** Unified color editor UX, nested create modals, required field indicators, undo improvements

- **Unified color editor**: all color pickers now include a hex input field, preset swatches, and an **Apply** checkbox — across catalog managers (tags, transforms, attributes), create modals, and details panels. Typing a hex code auto-checks Apply and updates the picker
- **Create modal color support**: the create modal for transforms and custom attributes now includes the full color editor (swatches + picker + hex input + Apply checkbox). Tags always have color applied; other types start with Apply unchecked
- **Nested create modals**: selecting "+ New tag…", "+ New attribute…", or "+ New value…" from the node create modal now opens a nested create modal instead of the full catalog manager. The node create modal's state is saved and restored after committing or cancelling. New items are automatically added to the node being created
- **Required field indicators**: Label fields in all editors and create modals now show a red **\*** asterisk. The Save button remains disabled until a label is provided — replaces the previous alert-based validation
- **Highlight colors undoable**: saving or deleting custom highlight colors now creates an undo snapshot. Ctrl+Z properly reverts highlight color changes
- **Undo catalog sync**: undo and redo now re-render all open catalog modals (tags, transforms, attributes, filters) and restore highlight CSS variables. Fixes ghost entries that appeared after undoing a catalog "Add" operation
- **Dim Off parent highlighting**: when Dim unselected is set to Off, connected parent groups now show the blue highlight — matching the behavior of Parents mode. Previously, parent groups were not highlighted in Off mode
- **Highlight colors preview labels**: the demo nodes in the highlight colors modal now read "Source" and "Target" instead of "source_id" and "target_id"
- **Dropdown reset on cancel**: selecting "+ New value…" in the node editor attribute dropdown now resets the dropdown immediately, so cancelling the create modal leaves it at the default "Value…" placeholder
- **Guard prompt labels**: dirty discard prompts for create modals now show friendly names ("custom attribute", "custom attribute value") instead of internal kind codes

---

## [1.3.8] – 2026-02-23
**Highlights:** Selection menu redesign, highlight mode, enhanced dimming, branding & licensing, Unicode transliteration

- **Selection menu redesign**: action buttons now have SVG icons and are reordered — Select all → Invert selection → Clear selection → Expand all → Collapse all. Cleaner visual hierarchy with grouped sections
- **Highlight mode (3-way)**: merged the old "Selection arrows" toggle and "Selected only" checkbox into a single **Chain** / **Direct** / **Selected** selector. **Chain** follows the full mapping chain, **Direct** shows only immediate neighbors, **Selected** highlights only the selection with no connected fields
- **Highlight parents removed**: the standalone "Highlight parents" toggle has been retired — its behavior is now baked into the **Parents** dim mode, which highlights ancestor groups with a subtle blue tint
- **Dim "All" fix**: expanded parent groups now correctly stay dimmed in All mode. Previously, parent highlighting was un-dimming them regardless
- **Selected group highlighting**: selecting a group now properly un-dims the group node itself and all its descendant subgroups
- **Selected mode edge hiding**: in Selected highlight mode, non-highlighted edges are fully hidden instead of dimmed
- **Enhanced dimming contrast**: dimmed elements are now more transparent — dark mode 0.30 → 0.22, bright mode 0.50 → 0.40
- **Column selection fix**: clicking a column header while in multi-select mode now properly clears the multi-selection
- **Unicode transliteration**: auto-generated IDs now convert accented characters to ASCII equivalents (á→a, é→e, ű→u, ñ→n, ö→o) instead of stripping them. Applied across all ID generation paths
- **Favicon**: inline SVG and PNG fallback — the Dunnode diamond icon appears in browser tabs
- **Branding headers**: Quick Start Guide and Documentation modals now open with the Dunnode logo, tagline, and description
- **MIT License**: full license text added to Documentation. Footer updated with clickable license link. About modal shows "MIT Licensed"
- **Privacy & Data Handling**: new Documentation section confirming Dunnode runs entirely client-side
- **About modal**: now includes dunnode.com link and "Runs entirely in your browser" notice
- **Version format**: standardized to "v1.3.8" (lowercase v prefix) across footer, About modal, docs, and release notes

---

## [1.3.7] – 2026-02-23
**Highlights:** Arrow controls redesign, filter bar polish, mapping color hierarchy, command palette docs search, terminology sweep

- **Arrow mode selector**: the three arrow checkboxes (Arrows, All arrows, Adjacent-only) are replaced by a clean 3-way selector in the Graph menu — **Selected** (only hovered/selected), **All** (every arrow), or **Off**. Matches the "Dim unselected" and "Details panel" dock selector pattern
- **Arrow scope toggles**: new **Same-column** and **Distant** checkboxes in the Graph menu replace the old Adjacent-only toggle. Independently hide arrows within the same column or across non-adjacent columns — adjacent-column arrows are always shown when arrows are on
- **Mapping color priority**: revised hierarchy is now Selection highlight → Filter color → Color-by scheme → Per-mapping manual color (lowest). "Color mappings by" now takes priority over individual mapping colors, matching the node color inheritance philosophy
- **Mapping dimming fix**: colored mappings (scheme, filter, or manual) now properly dim when a selection is active. Previously, inline opacity overrode the CSS dimming class
- **Filter bar redesign**: the right section of the filter bar now uses segmented selectors — **Hide / Dim / Highlight** mode selector, **AND / OR** logic selector, and a pill-style **Only mapped** toggle. Replaces the old checkboxes and cycle button with a cleaner, more discoverable layout
- **Column header toning**: colored column headers now show a 2px accent line (down from 3px) and neutral-colored text — removes the doubled-up effect of colored text plus thick colored border
- **Command palette docs search**: typing 3+ characters now also searches the full Documentation — matching sections appear under a "Documentation" category with a snippet preview. Selecting a result opens the docs modal and scrolls to the relevant section. The Help category now includes a Documentation command alongside Quick Start, Release Notes, and About
- **Adjacent highlight removed**: the "Adjacent highlight" toggle in the Selection menu has been retired. Its functionality is now better served by the arrow scope toggles (Same-column / Distant) which control both drawing and visibility in a more intuitive way
- **Terminology sweep**: all user-facing text now consistently uses "mapping" instead of "edge" — detail panel headers, status bar counts, tooltips, export filenames, documentation, and changelog. Code internals retain "edge" as the correct graph theory term
- **Sample data refresh**: all five columns now have colors (Lab → emerald, Archive DB → slate, Obs → amber). New group-level colors on lab.personnel (pink), arch.fact_telemetry (sky blue), and arch.dim_crew (indigo). Seven mappings now have custom colors to showcase the color priority hierarchy
- **Select all / Invert selection**: previously hidden in the command palette, now surfaced as buttons in the Selection menu and as keyboard shortcuts — **Ctrl+A** (Cmd+A) selects all visible nodes, **Ctrl+Shift+I** (Cmd+Shift+I) inverts the current selection

---

## [1.3.6] – 2026-02-22
**Highlights:** Column viewer, node color mode toggle, column header tint, bug fixes

- **Column viewer**: clicking a column header now shows a proper Column view in the details panel (label, ID, note, color, field/group/mapping counts) instead of incorrectly showing the root group node. Works in both viewer and editor mode
- **Column selection persistence**: toggling between viewer and editor mode no longer loses the column selection — the column stays selected and the details panel switches between column viewer and column editor automatically
- **Node color mode**: new "Node colors" section in the Layout popover with four modes — **All** (full inheritance), **Groups** (column + group colors only, no field overrides), **Column** (column colors only), **Off** (no background tinting). Styled with icon buttons matching the Dim unselected pattern
- **Column header tint**: column headers now display a subtle background tint in addition to the colored name and bottom border, making the column color more visible in the viewer

---

## [1.3.5] – 2026-02-22
**Highlights:** Group color inheritance, updated sample data, documentation refresh

- **Group color inheritance**: groups with an applied color now cascade to all descendants. The full hierarchy is: Node color (applied) → nearest ancestor group color (applied) → Column color → none. This means a single color on a group can tint hundreds of children, and any child can override it with its own applied color
- **Sample data refresh**: the built-in Mars Mission example showcases color hierarchy — Mission Control (blue column), Crew group (red, overrides column), CommanderName field (amber, overrides group), Spacecraft Telemetry (purple column), Navigation subgroup (orange), Observatory Validation group (yellow). Attribute values include `colorEnabled` flags to demonstrate inheritance
- **Documentation updated**: Quick Start Guide, full Documentation, and JSON schema reference all updated to cover column colors, group color inheritance, attribute-level color, value Apply checkboxes, and the label→ID auto-fill additions

---

## [1.3.4] – 2026-02-22
**Highlights:** Color hierarchy: column colors, attribute colors, value colorEnabled, label→ID auto-fill everywhere

- **Column colors**: columns now have an optional color with Apply checkbox. When applied, the column header is tinted and all child nodes without their own color inherit the column color as a subtle background
- **Attribute-level color**: attributes can now have their own color with swatch picker and Apply checkbox. When enabled, attribute values that don’t have their own color applied will inherit the attribute’s color for node pills
- **Attribute value Apply checkbox**: each value’s color now has an explicit Apply toggle. Unchecked = color is stored but not used, inherits from attribute instead. For "Color mappings by", disabled value colors fall back to the default palette
- **Color hierarchy**: node background tint follows Node color (applied) → nearest ancestor color (applied) → Column color → none. A group with color applied cascades to all descendants until overridden by a child with its own applied color. Attribute value pill color follows Value color (applied) → Attribute color (applied) → none
- **Label→ID auto-fill**: typing a label now auto-generates the ID (and abbreviation where applicable) in the column editor, node editor, and attribute value rows — matching the existing tag/transform pattern. "auto" badges show when values are auto-synced
- **Dirty detection fixes**: attribute value field edits (label, id, abbr, note), attribute color changes, and filter color changes now correctly activate the Save button

---

## [1.3.3] – 2026-02-21
**Highlights:** Node attribute pills, transform colors, attribute ordering & display controls

- **Multi-select drag-and-drop**: when multiple nodes are selected, dragging any selected node performs the operation on all selected nodes at once. Same modifier keys apply: no modifier = Move, Alt = Map, Ctrl/Cmd = Copy, Ctrl/Cmd+Alt = Copy+
- **Multi MAP (Alt+drag)**: Alt-drag any selected node onto a non-selected field to create mappings from all selected fields to that target. Selection switches to the target field afterward
- **Multi MOVE**: drag selected nodes to reposition them together. Nodes maintain their original relative order. Automatic deduplication: children of selected groups are excluded since they move implicitly with their parent
- **Multi COPY / COPY+**: Ctrl-drag to duplicate all selected nodes at the drop location. Ctrl+Alt duplicates with mappings. Same deduplication and ordering rules as Move
- **Multi bin delete**: drag selected nodes to the 🗑 Delete zone to bulk-delete with confirmation. Shows affected mapping count
- **Transform custom color**: transforms now have an optional color field with swatch picker and hex input. Used by "Color mappings by → Transform" to override the default palette
- **Custom attribute ordering**: attributes and their values now have priority-based ordering with drag-and-drop reorder and ↑/↓ buttons, matching the tag catalog pattern
- **Attribute "Display on node"**: per-attribute checkbox controls whether its values appear as pills on tree nodes. Pill order: Tags first → Attributes by priority → Values by priority within each attribute
- **Value abbreviation**: each custom attribute value now has an optional abbreviation field. When set, the abbreviation is shown instead of the full label in node pills
- **Layout display toggles**: two new checkboxes in the Layout menu — "Display tags" and "Display attributes" — control visibility of tag and attribute pills on all nodes
- **Copy self-drop refinement**: copying a node before/after itself is allowed (duplicate in place), but copying into itself is blocked to prevent recursive nesting

---

## [1.3.1] – 2026-02-21
**Highlights:** Unified editor UX: inline creation, smart auto-ID/abbr, dirty guards everywhere, "auto" indicators

- **Inline catalog creation**: adding a new tag, transform, or attribute opens an inline editor card at the top of the catalog list instead of a popup modal. Empty fields, auto-focused label, no Delete button for unsaved items
- **Unified Save/Cancel/Delete pattern**: all editors (catalog, filters, create modal, bulk modals) now follow the same pattern — Save (disabled until dirty), Cancel, and Delete (only for existing items). The old "Create X" buttons are replaced by a consistent "Save" button
- **Smart auto-ID from label**: typing a label auto-generates the ID in real time. Manually editing the ID stops the sync. Clearing the ID field re-derives it from the current label and resumes syncing. Works for all catalog items, filters, create modals, and transform param rows
- **Smart auto-abbreviation**: same sync logic applied to abbreviation fields — auto-fills from label, stops on manual edit, resumes on clear
- **Auto indicator badges**: a subtle blue **auto** pill appears next to ID and abbreviation fields when they are linked to the label. Disappears when manually overridden, reappears when cleared
- **Label validation**: all save handlers require a non-empty label — shows an alert and focuses the field if empty. Applies to tags, transforms, attributes, and filters
- **Dirty guards for new items**: cancelling or navigating away from an unsaved new item prompts "Discard new [kind]?" if the form has content, then removes the placeholder entry
- **Create modal dirty guards**: closing, cancelling, or clicking outside the create modal prompts if the form has content. Save button highlights when dirty
- **Bulk modal dirty tracking**: Apply buttons in bulk tag and bulk attribute modals now start inactive and highlight only when a change is made
- **Filter inline creation**: new filters start with an empty label and auto-generated ID, with the same Save/Cancel pattern and dirty guards as catalog items
- **ID regeneration on save**: saving any item with an empty ID field auto-generates the ID from the current label, whether the item is new or existing

---

## [1.3.0] – 2026-02-20
**Highlights:** Multi-select with Ctrl+click, Shift+click range, bulk actions, and chain/direct arrow modes

- **Multi-select (Ctrl/Cmd+click)**: hold Ctrl (Cmd on Mac) and click nodes to add or remove them from a multi-selection. Works across columns
- **Shift+click range select**: hold Shift and click to select a range of visible nodes within the same column (from last clicked to current)
- **Alt+click chain select**: if the clicked node is connected to the current selection, adds it plus the entire path in between. If already selected or unconnected, adds the clicked node’s full mapping chain
- **Directional chain select**: **Alt+Shift+click** selects upstream only (all sources), **Alt+Ctrl/Cmd+click** selects downstream only (all targets)
- **Marquee & lasso select**: drag on empty viewer background to draw a selection rectangle. Hold Alt while dragging for freeform lasso. All nodes within the shape are selected. Hold Shift to add to existing selection, Ctrl/Cmd to subtract
- **Combined highlighting**: all selected nodes highlight their mapping chains simultaneously. Dimming, arrows, and chain-following work across the combined set
- **Highlight mode**: toggle between **Chain** (follow full mapping chain, default), **Direct** (show only immediate mappings), and **Selected** (highlight only the selection) in the Selection popover
- **Details panel summary**: when multiple nodes are selected, the details panel shows a count breakdown by type and column, mapping stats, and a scrollable node list
- **Bulk delete**: delete all selected nodes and their mappings with one click (undo supported)
- **Bulk tag assign**: add or remove tags across all selected nodes at once — checkboxes show current state (checked, unchecked, or indeterminate for partial)
- **Bulk set attribute**: set or clear a custom attribute value on all selected nodes
- **Bulk map to…**: create mappings from all selected fields to a single target field — search by name or ID
- **Select all / Invert selection**: command palette commands to select all visible nodes or invert the current selection
- **Parameterized transforms**: transforms now support per-instance parameters. Catalog entries define a params schema (e.g. precision, fallback value, lookup table); each instance on a mapping can override the defaults. The same transform can be applied multiple times in a chain with different parameters
- **Transform params UI**: click a parameterized transform chip in the mapping editor to edit its parameters. Catalog editor now includes a params section to define parameter schemas (id, label, type, default)
- **Mapping color legend hover preview**: hovering any "Color mappings by" button temporarily shows its legend
- **Consistent context menu icons**: indent/outdent now use ← / → (matching filter conditions), column move uses ⇤ / ⇥

---

## [1.2.5] – 2026-02-20
**Highlights:** Mapping dimming, visual adjacency, toolbar quick-actions, legend hover preview

- **Mapping dimming**: unrelated mappings now dim to match node dimming when a selection is active. Respects the 3-state dim mode (All / Parents / Off)
- **Active mapping z-ordering**: hovered or selected mappings always render on top of other mappings, fixing visual overlap in dense graphs
- **Visual column adjacency**: hidden columns are now skipped when calculating adjacency — two columns displayed side-by-side count as adjacent even if hidden columns exist between them
- **Node colors when dimmed**: custom node colors are now preserved (at reduced opacity) when dimmed instead of being stripped
- **Pan toggle button**: ⊞ four-way arrow icon in the toolbar for quick pan mode toggle
- **Clear selection button**: ⊘ icon in the toolbar to deselect — same as pressing Escape
- **Add column in Columns popover**: "Add column left/right" buttons moved into the Columns… popover footer (editor mode)
- **Command palette background**: dark mode palette now uses a solid background matching other modals
- **Safari known limitation**: documented that drag-and-drop is not supported in Safari

---

## [1.2.4] – 2026-02-20
**Highlights:** Command palette with fuzzy search for commands and nodes

- **Command palette**: press **Ctrl+K** (Cmd+K on Mac) or click the ⌘ button in the header to open a spotlight-style command bar
- **Fuzzy search**: type to filter all available commands (open catalogs, toggle modes, change panel layout, undo/redo, etc.) with match highlighting
- **Node search**: the palette also searches all nodes and fields by name or ID. Selecting a node expands parent groups, highlights it, and scrolls it into view
- **Keyboard navigation**: ↑↓ to move, Enter to execute, Escape to close. Results grouped by Commands and Nodes & Fields
- **Shortcut hints**: commands show their keyboard shortcut when one exists (e.g. ?, D, Ctrl+Z)

---

## [1.2.3] – 2026-02-20
**Highlights:** Custom attribute value colors with swatches, catalog overview color dots, create modal color picker

- **Attribute value color dots**: the Attributes catalog overview now shows a tiny colored dot next to each value that has a custom color assigned
- **Value editor color swatches**: 🎨 toggle button on each value row reveals a preset swatch panel (10 colors) for quick color selection — same pattern as the filter editor palette
- **Value color reset**: ↺ icon next to each value’s color picker clears the custom color and reverts to the uncolored default state
- **Create value modal color picker**: adding a new attribute value now includes the full color picker with swatches and hex input, auto-visible without a toggle. ↺ reset icon included
- **Edge coloring priority**: "Color mappings by" attribute modes use the value’s custom color when set, falling back to the 20-color palette for uncolored values

---

## [1.2.2] – 2026-02-20
**Highlights:** Highlight colors modal redesign with live preview, project JSON persistence, editor/viewer modes

- **Highlight colors modal redesign**: full editor workflow with Save / Cancel / Delete buttons matching the tag editor pattern. Close button in header with unsaved-changes guard
- **Project JSON persistence**: highlight colors saved as `_highlightColors` in project data — colors travel with the file. Omitted when defaults are active (clean JSON)
- **Live preview tester**: interactive source → target preview in the modal. Hover or click nodes and arrow to see exactly how chosen colors render for connected vs selected states
- **Editor / Viewer mode**: color pickers and swatches are read-only in Viewer mode with a hint to switch to Editor. Save/Cancel/Delete only appear in Editor mode
- **Delete with confirmation**: removes custom colors from project data and reverts to defaults with a confirm dialog
- **Per-row ↺ reset**: inline reset icon per color row, sitting alongside swatches for quick default restore
- **Standard button styling**: Save uses `btnSave`/`btnDirty` classes (yellow highlight when dirty), Delete uses the standard pink border pattern

---

## [1.2.1] – 2026-02-20
**Highlights:** Zoom slider, selection controls, highlight color customization, same-column arrow improvements

- **Zoom / density slider**: new Zoom control (50–150%) in the Layout popover scales the entire viewer for fitting more or less content on screen. Persisted to localStorage with inline ↺ reset
- **Dim mode selector**: "Dim others" replaced with a 3-mode icon selector: **All** (dim everything unselected), **Parents** (keep parent groups visible), **Off** (no dimming)
- **Dim unselected: Parents mode**: expanded parent groups of connected fields get a subtle blue highlight and remain visible. In All mode, only direct connections are shown. Collapsed groups are always highlighted regardless
- **Highlight mode: Selected**: limits highlighting to the directly selected node — suppresses the full mapping chain highlight and restricts which arrows are drawn
- **Adjacent highlight**: moved from Graph to Selection popover where it logically belongs
- **Highlight colors modal**: customize Connected (chain) and Selected (active) highlight colors via color picker and 10-color swatches
- **Mapping color scheme selector**: "Color mappings by" dropdown replaced with icon buttons matching the dock selector pattern — Off, Cardinality, Transform, Source tag, Target tag
- **Same-column arrows (rightmost)**: arrows in the rightmost column now loop to the left instead of right, preventing overflow clipping
- **Same-column sample mappings**: sample dataset now includes within-column mappings in Observatory and Science Lab
- **Collapse recalculates highlights**: toggling a group collapsed/expanded now recalculates highlight state correctly
- **CSS dim inheritance fix**: changed `.dimmed .row` to `.dimmed > .row` so dimmed parents no longer cascade to connected children
- Viewer right padding added for consistent spacing on the rightmost column border
- Arrow zoom compensation: coordinates divide by CSS zoom factor for correct alignment at any zoom level
- Documentation footer updated to match Quick Start Guide style with version number

---

## [1.2.0] – 2026-02-20
**Highlights:** Dunnode rebrand, float panel overhaul, color picker UX, scroll/resize fixes

- **Rebrand to Dunnode**: new name, all-caps wordmark with tracking, tagline "Done. Now."
- **About modal**: new Help → About with branding, creator info, and contact
- **App footer**: persistent footer with copyright and version, visible in all panel dock modes
- **_app metadata**: JSON format changed from string to `{ name, version, schema }` object. Old files auto-migrated on load
- **Float panel overhaul**: top/left CSS anchoring (resize grows down-right naturally), custom corner resize handle with ╝ indicator
- **6-dot drag grip**: float panel header shows a standard 2×3 dot grip icon instead of invisible drag bar
- **Pan mode (P key)**: toggle pan mode with P, cross-arrow cursor, drag to scroll viewport. Press P or Esc to exit
- **Resize handles**: thicker (14px), blue glow on hover, groove line indicator, follow cursor during drag
- **Color preset swatches**: inline row of 10 color swatches in node and mapping editors alongside the picker and Apply checkbox
- **Color persistence**: picker value preserved as `_pendingColor` when Apply is unchecked — survives save/reload
- **Tag manager color picker**: native `<input type="color">` added alongside hex input and swatches, all bidirectionally synced
- **Filter mapping highlighting**: collapsed group arrows now inherit filter colors from constituent mappings
- **Live arrow redraw**: arrows update in real-time during bottom and side panel resize, not just on mouse-up
- **Scroll area fix**: SVG overlay no longer inflates scroll dimensions; ResizeObserver triggers redraw on any container resize
- **Details panel min-width**: increased to 360px to prevent UI collapse at narrow widths
- **Nested group support**: sample dataset includes SAMPLE_ANALYSIS nested group inside EXPERIMENT
- **Quick Start Guide**: updated with welcome message and closing tagline
- **Documentation**: updated JSON schema reference with new `_app` object format
- Sample project author changed to "Mars Systems Integration Team"
- Dirty detection now tracks color picker value independently of Apply checkbox state
- Project title input made smaller (14px) to give more visual weight to the app name

---

## [1.1.1] – 2026-02-19
**Highlights:** Editor polish, new metadata fields, bug fixes

- **_app identity**: JSON files now include `_app: "Mapping Studio"` to identify the source application
- **Project properties**: added Contact and URL fields (URL renders as clickable link in details pane)
- **Filter ID field**: filter editor now has an editable ID field with conflict detection, matching tag/transform/attribute behavior. ID shown in viewer cards
- **Condition editor buttons**: ↑ ↓ → ← action buttons on each condition row and group header for move up, move down, indent into group, and outdent from group
- **Edge color scheme palette**: extended from 10 to 20 distinct colors for better differentiation with many values
- **Catalog buttons hidden in viewer**: "Add tag/transform/attribute/filter" buttons are hidden in Viewer mode instead of showing an error
- **Toggle hover effect**: all toggle/checkbox controls now have hover highlighting in both dark and bright themes
- **Save button states**: Save buttons start greyed out (disabled appearance) when no changes are pending, including the Project Properties save button
- Mapping editor no longer shows false dirty state on open (undefined vs empty string normalization)
- Node and mapping color picker changes now correctly trigger dirty state on Save buttons
- New project / Load example / Open file now clears stale edit sessions, preventing phantom abandon-guard prompts
- Release notes now render HTML formatting (bold tags) correctly

---

## [1.1.0] – 2026-02-19
**Highlights:** Filtering overhaul, unsaved-changes protection, UX polish

- **Filter system**: rule-based filters with recursive condition groups (AND/OR), priority ordering, and rich highlight styles (background, stripe, mapping color, frame, bold, emoji)
- **Filter catalog**: create, edit, reorder, delete filters with live preview. Priority-based evaluation with drag-and-drop and ▲▼ button reordering
- **Filter bar**: toolbar toggle (🔎) with search input, Only mapped, display mode cycle, Filters AND/OR, Clear all, and active filter chips
- **Display mode cycle**: Hide → Dim → Highlight only. "Highlight only" keeps all nodes visible and just applies color styles to matches
- **Color palette**: 🎨 button in filter editor shows preset color swatches — click to apply to all enabled channels, or drag onto individual swatches
- **Unsaved-changes guard**: navigating away from edited nodes, columns, mappings, or catalog items prompts "Abandon unsaved changes?" Only fires when actual changes detected
- **Yellow Save buttons**: Save buttons turn gold when the form has pending changes vs. the snapshot. Reverts when user manually restores original values
- **Greyed-out catalog items**: while editing a tag/transform/attribute/filter, other items are dimmed and unclickable to prevent accidental switching
- **Details panel enhancements**: groups show rich Children cards with type, summary, tags, and attributes. Inbound/Outbound/Children sections are collapsible (▾ caret)
- **Undo/Redo guards**: Ctrl+Z/Y prompts if there are unsaved edits in the active editor before reverting state
- **Editor↔Viewer mode guard**: switching to Viewer mode prompts if node or mapping edits are unsaved
- **Node ID dirty check**: changing a node or column ID field is now properly detected as a pending change
- **Node colors**: optional per-node color applied as subtle background tint on the viewer row. Shown in details pane. Overridden by filter/selection highlights
- **Mapping colors**: optional per-mapping color applied to arrow strokes. Filter mapping colors take priority, then custom mapping colors, then default
- **Color mappings by**: automatic arrow coloring by cardinality, first transform, source/target tag, or source/target custom attribute. Select in Graph popover; legend auto-generated
- **Selection dim toggle**: "Dim others" checkbox in Selection popover — uncheck to keep all nodes at full opacity when something is selected
- **Color palette**: 🎨 button in filter editor shows 10 preset swatches with drag-to-swatch and click-to-apply-all-channels
- **Condition DnD**: drag ⠿ handles in the filter condition editor to reorder conditions, move between groups, or indent into a group
- Rephrased "new project" and "load example" confirmation prompts to be clearer
- Filter AND/OR toggle relabeled to "Filters: AND" to clarify it only affects filters (search is always ANDed)
- Context menu toggle fix for column and node ⫶ buttons
- Escape key now cancels column edits and mapping drafts (previously only handled node edits)
- Indent/outdent now correctly preserves mappings by passing state.data to replaceIdsInMappings
- Filter badge (Escape) correctly resets to 0

---

## [1.0.0] – 2026-02-18
**Highlights:** Initial release

- Multi-column schema viewer with nested tree structure and collapsible groups
- Bezier curve arrows across adjacent and non-adjacent columns with virtual edge discovery
- Full inline editor: create, edit, delete, move, indent/outdent nodes and columns
- Drag-and-drop support for nodes and columns
- Mapping editor with cardinality, default values, notes, and ordered transforms
- Tag catalog with color-coded chips, abbreviations, notes, and drag-to-reorder priority
- Transform catalog with abbreviations and notes
- Custom attribute catalog with multi/single-value modes and per-value notes
- All entity IDs independently editable with cascading rename across the full data model
- Hierarchical node IDs with auto-calculated path prefix and editable local segment
- Undo/redo with snapshot-based dirty tracking (save button reflects true state)
- Project properties modal: title, subtitle, author, organization, contact, URL, version, date, description
- App version and save timestamp stamped into JSON on every save
- Bright/dark mode with comprehensive theme coverage
- Column visibility controls, reordering, wrap mode for screenshots
- Arrow display modes: all, adjacent-only, highlight-only; plus adjacent-only highlight mode
- Details panel showing node metadata, mapping details, and project summary
- Tooltips on hover for nodes, mappings, and virtual mappings through hidden columns
- Context menus for columns and nodes with full action set
- CSV export of visible edges and HTML report export with embedded JSON
- Search/filter by text, filter by unmapped fields
- Inline Quick help, comprehensive Documentation page, and Release notes
- Sample dataset: Mars mission data pipeline across 5 systems (31 mappings, 3 tags, 8 transforms, 2 custom attributes)
- Keyboard shortcuts: Escape to deselect, ? for help, Ctrl+Z/Y for undo/redo