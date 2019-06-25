# Tasks

LittlevGL has a built-in task system. You can register a function to call them periodically. The tasks are handled and called in `lv_task_handler()` which needs to be called periodically in every few milliseconds. 
See [Porting](/porting/task-handler) for more information.

The tasks are non-preemptive which means a task can interrupt an other.

To create a new task use `lv_task_create(task_cb, period_ms, LV_TASK_PRIO_OFF/LOWEST/LOW/MID/HIGH/HIGHEST, user_data)`. It will create an `lv_task_t *` variable which can be used later to modify the parameters of the task.
`lv_task_create_basic()` also can be used to create a new task without specifying any parameters.

A task callback should have `void (*lv_task_cb_t)(lv_task_t *);` prototype.


## Ready and Reset

`lv_task_ready(task)` makes the task run on the next call of `lv_task_handler()`.

`lv_task_reset(task)` resets the period of a task. It will be called the defined period milliseconds later.


## Set parameters
You can modify some parameters of the tasks later:
- `lv_task_set_cb(task, new_cb)`
- `lv_task_set_period(task, new_period)`
- `lv_task_set_prio(task, new_priority)`

## One-shot tasks

You can make a task to run only once by calling`lv_task_once(task)`. The task will be automatically deleted when called fo the first time.


## Measure idle time

You can get the idle percentage time `lv_task_handler` with `lv_task_get_idle()`. Note that, it doesn't measure the idle time of the overall system, only `lv_task_handler`. 
It might be misleading if you use an operating system and call `lv_task_handler` in a task.

## API 

```eval_rst

.. doxygenfile:: lv_task.h
  :project: lvgl
        
```

