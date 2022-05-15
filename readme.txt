# Q1.  If I wanted to change the workflow by adding an extra step after the stirring step, but
before the summary, what would I have to do?

Ans. The step has to be added under the 'steps:' nesting, before 'summary' but after 'stirring' subsections.
Asuuming the new task is called 'newtask', it will have indentations matching that of weighing, srirring
and summary. Also the flow section should mention this:

```
flow:
  - weighing
  - stirring
  - newstep
  - summary
```



# Q2. When adding the iced tea mix to the flask, we also want to show the user the target
weight, as defined at the beginning of the workflow. How would you accomplish this?

Ans.

# Q3. Regarding the screencast and line 146 of the template: What’s the value of the
“data_point.qty”in that specific example?

Ans.


# Q4. Please explain what happens when the timer runs out on its own vs. when the user stops
the timer manually.

Ans. This is the code block for timer manual or auto completion:

```
 - when:
              - on_timer_stop
              - on_timer_complete
            do:
              - send_command:
                  device: Stirrer
                  command: set_stirrer_status
                  data: 0
              - complete_substep

```
For both manual stopping and normal completion
