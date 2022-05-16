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
I have a confusion regarding this question: does this command already not show the targeted weight:

```
primary: Put {{TargetWeight}} of Ice Tea into the flask and press print.

```

If the question is to visualize the taget value after pressing 'print' button, then we need to put an extra command in the behavior field of device 'Balance', we have to add a section after '-when: on_data_point'
```
behaviors:
          - when:
              on_manual:
                key: print
            do:
              send_command:
                device: Balance
                command: get_weight
          - when:
              on_data_point:
                device: Balance
                channel: weight
            do:
              - set_field:
                  field: StableWeight
                  value: data_point.qty
              - set_field:
                  field: TargetWeight
                  value: Targetweight
              - set_field:
                  field: Delta
                  value: (TargetWeight - data_point.qty)


```

# Q3. Regarding the screencast and line 146 of the template: What’s the value of the
“data_point.qty”in that specific example?

Ans. data_point.qty is the value of field StableWeight. In this particular case this is 9.69g.


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
