Diagram Tool - Markup Syntax (Version 10)
This version adds task icons, task-to-context connections (Control/Mechanism), swimlane spacing, and actor position refinement.

Overall Structure:

diagram [Diagram Title] // Optional

// --- Swimlane Definitions ---
swimlane [ID] "[Label]" [actor] // 'actor' keyword is optional
  task [ID] "[Description]" [icon="ICON_NAME"] // 'icon' attribute is optional
  event [ID] "[Label]" [type="TYPE"] // 'type' is optional
  gateway [ID] ["Label"] [type="TYPE"] // Label and 'type' are optional
  syncbar [ID] [orientation="ORIENT"] // 'orientation' is optional
  ... // More elements
end // End of swimlane block

swimlane ...
  ...
end

// --- Context Box Definition (Optional) ---
context [ID] "[Label]"
  input "[ArrowLabel]" from=left
  output "[ArrowLabel]" to=right
  control "[ArrowLabel]" from=top
  mechanism "[ArrowLabel]" from=bottom
  ... // More I/O/C/M
endcontext

// --- Connection Definitions ---
connect [SourceID] -> [TargetID] ["Label"] [style="STYLE"] // Element to Element
connect [TaskID] -> context.top ["Label"] [style="STYLE"] // Task to Context Control
connect [TaskID] -> context.bottom ["Label"] [style="STYLE"] // Task to Context Mechanism
...

Keywords & Syntax Details:

diagram [Title]: (Optional) Overall diagram title.

// or #: Comments or blank lines (ignored).

swimlane [ID] "[Label]" [actor]: Defines a swimlane.

[ID]: Unique identifier.

"[Label]": Displayed label (in quotes).

actor: (Optional) Displays a stick figure icon in the header.

end: Closes a swimlane block.

Elements (Defined inside swimlane...end blocks):

task [ID] "[Description]" [icon="ICON_NAME"]: Task/activity rectangle.

[ID]: Unique identifier.

"[Description]": Text inside the rectangle.

icon="ICON_NAME": (Optional) Displays an icon. Supported ICON_NAMEs: "envelope", "user", "gear", "database", "clock".

event [ID] "[Label]" [type="TYPE"]: Event circle.

[ID]: Unique identifier.

"[Label]": Text below the circle (required).

type="TYPE": (Optional) Allowed: "start" (default), "end", "workflow-start", "workflow-end".

gateway [ID] ["Label"] [type="TYPE"]: Gateway diamond.

[ID]: Unique identifier.

["Label"]: (Optional) Text below the diamond.

type="TYPE": (Optional) Allowed: "exclusive" (default, 'X'), "parallel" ('+').

syncbar [ID] [orientation="ORIENT"]: Synchronization bar (black rectangle).

[ID]: Unique identifier.

orientation="ORIENT": (Optional) Allowed: "horizontal" (default), "vertical".

context [ID] "[Label]": Starts the IDEF0-style context box definition (max one per diagram).

endcontext: Ends the context block.

Context Arrows (Defined inside context...endcontext blocks):

input "[ArrowLabel]" from=left: Input arrow pointing to the left edge.

output "[ArrowLabel]" to=right: Output arrow pointing from the right edge.

control "[ArrowLabel]" from=top: Control arrow pointing to the top edge.

mechanism "[ArrowLabel]" from=bottom: Mechanism arrow pointing to the bottom edge.

connect [SourceID] -> [TargetID] ["Label"] [style="STYLE"]: Defines connections.

[SourceID]: ID of a task, event, gateway, or syncbar.

[TargetID]: ID of a target element OR context.top or context.bottom.

["Label"]: (Optional) Text near the connection midpoint.

style="STYLE": (Optional) Allowed: "solid" (default), "dashed".

Key Changes from v9:

Task Icons: Added optional icon attribute to task elements.

Task-to-Context Connections: Extended connect syntax to allow tasks as sources and context.top or context.bottom as targets. Implemented rendering and basic staggering for these connections.

Swimlane Spacing: Added visual vertical spacing between swimlanes.

Actor Position: Slightly adjusted the vertical position of the actor symbol in the swimlane header.

Current Limitations (v10):

Context box arrows (input, output) originating from the context box do not yet connect to specific tasks. Connections to context.left or context.right are not supported.

Connection routing is basic orthogonal and does not avoid collisions.

Limited number of supported task icons and event/gateway types.

Parser requires attributes to appear in a specific order.
Diagram Tool - Markup Syntax (Version 11)
This version adds task icons, task-to-context connections (Control/Mechanism), optional swimlane spacing, and actor position refinement.

Overall Structure:

diagram [Diagram Title] // Optional

// --- Swimlane Definitions ---
swimlane [ID] "[Label]" [actor] [spacing=VALUE] // 'actor' & 'spacing' optional
  task [ID] "[Description]" [icon="ICON_NAME"] // 'icon' attribute is optional
  event [ID] "[Label]" [type="TYPE"] // 'type' is optional
  gateway [ID] ["Label"] [type="TYPE"] // Label and 'type' are optional
  syncbar [ID] [orientation="ORIENT"] // 'orientation' is optional
  ... // More elements
end // End of swimlane block

swimlane ...
  ...
end

// --- Context Box Definition (Optional) ---
context [ID] "[Label]"
  input "[ArrowLabel]" from=left
  output "[ArrowLabel]" to=right
  control "[ArrowLabel]" from=top
  mechanism "[ArrowLabel]" from=bottom
  ... // More I/O/C/M
endcontext

// --- Connection Definitions ---
connect [SourceID] -> [TargetID] ["Label"] [style="STYLE"] // Element to Element
connect [TaskID] -> [ContextID].top ["Label"] [style="STYLE"] // Task to Context Control
connect [TaskID] -> [ContextID].bottom ["Label"] [style="STYLE"] // Task to Context Mechanism
...

Keywords & Syntax Details:

diagram [Title]: (Optional) Overall diagram title.

// or #: Comments or blank lines (ignored).

swimlane [ID] "[Label]" [actor] [spacing=VALUE]: Defines a swimlane.

[ID]: Unique identifier.

"[Label]": Displayed label (in quotes).

actor: (Optional) Displays a stick figure icon in the header.

spacing=VALUE: (Optional) Specifies the vertical space (in pixels) below this swimlane. VALUE must be a non-negative integer. Defaults to 15 if omitted.

end: Closes a swimlane block.

Elements (Defined inside swimlane...end blocks):

task [ID] "[Description]" [icon="ICON_NAME"]: Task/activity rectangle.

[ID]: Unique identifier.

"[Description]": Text inside the rectangle.

icon="ICON_NAME": (Optional) Displays an icon. Supported ICON_NAMEs: "envelope", "user", "gear", "database", "clock".

event [ID] "[Label]" [type="TYPE"]: Event circle.

[ID]: Unique identifier.

"[Label]": Text below the circle (required).

type="TYPE": (Optional) Allowed: "start" (default), "end", "workflow-start", "workflow-end". (Intermediate/Inclusive planned).

gateway [ID] ["Label"] [type="TYPE"]: Gateway diamond.

[ID]: Unique identifier.

["Label"]: (Optional) Text below the diamond.

type="TYPE": (Optional) Allowed: "exclusive" (default, 'X'), "parallel" ('+'). (Inclusive planned).

syncbar [ID] [orientation="ORIENT"]: Synchronization bar (black rectangle).

[ID]: Unique identifier.

orientation="ORIENT": (Optional) Allowed: "horizontal" (default), "vertical".

context [ID] "[Label]": Starts the context box definition.

endcontext: Ends the context block.

Context Arrows (Defined inside context...endcontext blocks):

input "[ArrowLabel]" from=left: Input arrow to left edge.

output "[ArrowLabel]" to=right: Output arrow from right edge.

control "[ArrowLabel]" from=top: Control arrow to top edge.

mechanism "[ArrowLabel]" from=bottom: Mechanism arrow to bottom edge.

connect [SourceID] -> [TargetID] ["Label"] [style="STYLE"]: Defines connections.

[SourceID]: ID of a task, event, gateway, or syncbar.

[TargetID]: ID of a target element OR [ContextID].top or [ContextID].bottom. Source must be a task if target is context.top or context.bottom.

["Label"]: (Optional) Text near the connection midpoint.

style="STYLE": (Optional) Allowed: "solid" (default), "dashed".

Key Changes from v9:

Task Icons: Added optional icon attribute to task elements and rendering support.

Task-to-Context Connections: Extended connect syntax to allow tasks as sources and [ContextID].top or [ContextID].bottom as targets. Implemented rendering and basic staggering for these connections.

Optional Swimlane Spacing: Added spacing=VALUE attribute to swimlane definition. Renderer now uses this value (or a default) instead of a fixed spacing.

Actor Position: Slightly adjusted the vertical position of the actor symbol.

Parser Fixes: Corrected regex and validation logic for task-to-context connections.

Current Limitations (v11):

Context box arrows (input, output) originating from the context box do not yet connect to specific tasks. Connections to context.left or context.right are not supported.

Connection routing is basic orthogonal and does not avoid collisions.

Limited number of supported task icons and event/gateway types.

Parser requires attributes to appear in a specific order.