# Relative Recurring Tasks for Task Warrior

(c) 2014 [Jens Erat] <email@jenserat.de>, MIT License

This is a small hack providing [relative recurring tasks][TW-150] with due date some period after completing the current task. [Taskwarrior] will not learn such a feature before ["the Great Recurrence rewrite", which has already been delayed for many years][Recurrence RFC], so this had to be dealt with.

## Requirements

This hook requires a Task Warrior 2.4.2 build not older than 2015-02-22.

It works with both Python 2 and 3.

## Installation

Link the python script into `~/.task/hooks`, creating this folder if needed. Then add two [user defined attributes] for recurring tasks:

    task config uda.relativeRecurDue.type duration
    task config uda.relativeRecurDue.label 'Rel. Rec. Due'
    task config uda.relativeRecurScheduled.type duration
    task config uda.relativeRecurScheduled.label 'Rel. Rec. Scheduled'
    task config uda.relativeRecurWait.type duration
    task config uda.relativeRecurWait.label 'Rel. Rec. Wait'

## Usage

Create a task and set the `relativeRecurDue`, `relativeRecurScheduled`, and/or `relativeRecurWait` attributes. Some examples:

- You shouldn't mow your lawn more than once a week, but want to keep it short, so shouldn't wait for more than two weeks:

        task add 'Mow the Lawn' relativeRecurWait:1weeks relativeRecurDue:2weeks

- Ate enough fruit? Eat at least daily, but eating another one straight after won't hurt you:

        task add 'Eat a Fruit!' relativeRecurDue:1day

- Is it vacation time yet? Don't go to often, otherwise your taskwarrior log will overfill:

        task add 'Go on vacation' relativeRecurWait:2months relativeRecurScheduled:2months

After completion of any of them, follow-up tasks will automatically be created.

You can also complete waiting tasks. For example, you could water your plants just before departing for vacation.

## Caveats

For the initial tasks, no due date is automatically set. You might add one manually, or just complete the task anyway (and mark it as done, so the follow-up task with correct wait and/or due dates are set).

Be aware that this only happens when the hook triggers on completion, for example if completing a task on another host (like a phone running Mirakel) will complete without creating the follow-up task nor telling you so. A cleanup-job would be very similar to the script and easy to write, but nobody needed it hard enough yet to code it.

[Jens Erat]: http://www.jenserat.de
[Taskwarrior]: http://taskwarrior.org
[user defined attributes]: http://taskwarrior.org/docs/udas.html
[Recurrence RFC]: https://taskwarrior.org/docs/design/recurrence.html
[TW-150]: https://github.com/GothenburgBitFactory/taskwarrior/issues/203
