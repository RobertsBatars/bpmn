Test Cases for Diagram Tool (Increment 10 - Revised)
These tests verify task icons, task-to-context connections, swimlane spacing, and actor position. Run tests from previous versions as well.

1. Task Icon Cases

Test 1.1: Task with Envelope Icon

Input:

diagram TaskIconTest1
swimlane A "Lane"
  task T1 "Send Email" icon="envelope"
end

Expected Outcome: Renders task T1 with a small envelope icon in the top-left corner. Text is positioned correctly beside the icon. No errors.

Test 1.2: Task with User Icon

Input:

diagram TaskIconTest2
swimlane A "Lane"
  task T1 "Assign User" icon="user"
end

Expected Outcome: Renders task T1 with a small user icon. No errors.

Test 1.3: Task with Gear Icon

Input:

diagram TaskIconTest3
swimlane A "Lane"
  task T1 "Process Data" icon="gear"
end

Expected Outcome: Renders task T1 with a small gear icon. No errors.

Test 1.4: Task with Database Icon

Input:

diagram TaskIconTest4
swimlane A "Lane"
  task T1 "Update DB" icon="database"
end

Expected Outcome: Renders task T1 with a small database (cylinder) icon. No errors.

Test 1.5: Task with Clock Icon

Input:

diagram TaskIconTest5
swimlane A "Lane"
  task T1 "Wait for Event" icon="clock"
end

Expected Outcome: Renders task T1 with a small clock icon. No errors.

Test 1.6: Task without Icon

Input:

diagram TaskIconTest6
swimlane A "Lane"
  task T1 "Normal Task" // No icon attribute
end

Expected Outcome: Renders task T1 normally without any icon. Text fills the available space. No errors.

Test 1.7: Task with Invalid Icon Name

Input:

diagram TaskIconTest7
swimlane A "Lane"
  task T1 "Bad Icon" icon="rocket" // Invalid icon name
end

Expected Outcome: Error message like "Invalid icon name: 'rocket'. Allowed: envelope, user, ..." pointing to the task line.

2. Task-to-Context Connection Cases

Test 2.1: Task to Context Top (Control)

Input:

diagram TaskToContext1
swimlane A "Sub Process"
  task T1 "Provide Rules"
end
context C0 "Main Process" // Context ID is C0
  control "Rules" from=top
endcontext
connect T1 -> C0.top "Rule Input" style="dashed" // Corrected target

Expected Outcome: Renders swimlane A with T1, and the context box C0 below. A dashed orthogonal arrow goes from T1 to the top edge of C0, labeled "Rule Input". No errors.

Test 2.2: Task to Context Bottom (Mechanism)

Input:

diagram TaskToContext2
swimlane B "Resource Lane"
  task T2 "Resource Provider" icon="gear"
end
context C0 "Main Process" // Context ID is C0
  mechanism "Resource Used" from=bottom
endcontext
connect T2 -> C0.bottom "Resource Link" // Corrected target

Expected Outcome: Renders swimlane B with T2, and the context box C0 below. A solid orthogonal arrow goes from T2 to the bottom edge of C0, labeled "Resource Link". No errors.

Test 2.3: Multiple Tasks to Context Top (Staggering)

Input:

diagram TaskToContext3
swimlane A "Controls"
  task Ctr1 "Rule Set 1"
  task Ctr2 "Rule Set 2"
end
context C0 "Main Process" // Context ID is C0
  control "Control Input 1" from=top
  control "Control Input 2" from=top
endcontext
connect Ctr1 -> C0.top "From Ctr1" // Corrected target
connect Ctr2 -> C0.top "From Ctr2" // Corrected target

Expected Outcome: Renders swimlanes and context box. Two orthogonal arrows connect Ctr1 and Ctr2 to the top edge of C0. The attachment points on the C0 top edge should be staggered horizontally. Labels render correctly. No errors.

Test 2.4: Connecting Non-Task to Context (Error)

Input:

diagram BadContextConnect1
swimlane A "Lane"
  event E1 "Start"
end
context C0 "Process" // Context ID is C0
endcontext
connect E1 -> C0.top // Invalid source type

Expected Outcome: Error message indicating that the source for a context connection must be a task.

Test 2.5: Connecting Task to Invalid Context Side (Error)

Input:

diagram BadContextConnect2
swimlane A "Lane"
  task T1 "Task"
end
context C0 "Process" // Context ID is C0
endcontext
connect T1 -> C0.left // Invalid target side for task connection

Expected Outcome: Error message indicating invalid target context side (only top/bottom allowed from tasks).

3. Layout Cases (Visual Inspection)

Test 3.1: Swimlane Spacing (Optional)

Input:

diagram LaneSpacing
swimlane A "Lane 1" spacing=5 // Small gap
  task T1 "T1"
end
swimlane B "Lane 2" spacing=30 // Large gap
  task T2 "T2"
end
swimlane C "Lane 3" // Default gap
  task T3 "T3"
end
swimlane D "Lane 4" spacing=0 // No gap
    task T4 "T4"
end

Expected Outcome: Visually inspect the rendered diagram. There should be different vertical gaps below Lane 1 (small), Lane 2 (large), Lane 3 (default), and Lane 4 (none).

Test 3.2: Actor Vertical Position

Input:

diagram ActorPosCheck
swimlane Manager "Manager Role" actor
    task T1 "Task"
end

Expected Outcome: Visually inspect the actor symbol. It should appear slightly higher than the exact vertical midpoint of the swimlane header area.

Run these tests to verify task icons, task-to-context connections, optional swimlane spacing, and actor positioning.