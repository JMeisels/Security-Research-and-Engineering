# Twill Typhoon-Informed Scheduled Task Persistence Hunt

KQL hunt logic by Jordan Meisels for reviewing a sequence of executable extraction, subsequent file creation at a different path, optional renaming, and scheduled task creation in Microsoft Defender endpoint telemetry.

This project shows how threat intelligence can be translated into behavior-based investigation logic. A result is an investigation candidate, not proof of malicious activity, successful execution, compromise, or actor attribution.

## Intelligence context and confidentiality

The hunt was developed from confidential threat intelligence concerning Twill Typhoon. The underlying intelligence report is confidential and is not reproduced, attached, or distributed in this repository. Only the author's hunt code and an explanation of its approach are shared here.

The supplied query retains the specific filename and folder indicators, including `RegExt.exe`, `CommonLib.dll`, and `MicrosoftEdgeServices`. These references provide hunt context; they do not independently establish attribution. `CommonLib.dll` appears in an analyst-review comment, not as an explicit final-result filter.

## Files

| File | Purpose |
| --- | --- |
| [scheduled-task-persistence.kql](scheduled-task-persistence.kql) | Main query with a configurable lookback window. |
| [original-hunt.kql](original-hunt.kql) | Original supplied query with its fixed example dates. |

The main query preserves the original correlation and filtering logic. Its only functional change is replacing the repeated fixed date ranges with shared `HuntStart` and `HuntEnd` variables. The default lookback is seven days.

## Telemetry and setup

The query expects `DeviceFileEvents` and `DeviceEvents`, with a `TimeGenerated` time column. Confirm that the tables and fields are available in your environment. Adapt the time-column references if your workspace uses a different schema.

Relevant fields include `DeviceName`, `FileName`, `FolderPath`, `SHA256`, `ActionType`, initiating-process details, and `AdditionalFields`. Task parsing assumes the `TaskContent` structure used in the original query. Validate that structure against your own events before relying on the extracted command, arguments, or repetition interval.

## How to use it

1. Open the main `.kql` file in your authorized hunting workspace.
2. Set `Lookback` to an appropriate review period, or set `HuntStart` and `HuntEnd` to explicit datetimes.
3. Review the filename indicators, writable-directory heuristics, and exclusion placeholders for relevance to your environment.
4. Run the query and inspect the returned task content and surrounding endpoint events.
5. Corroborate any finding with task-action paths, file hashes, process execution, user context, and other available evidence.

For a fixed investigation window, replace the window declarations with:

```kusto
let HuntStart = datetime(2026-08-31T00:00:00Z);
let HuntEnd = datetime(2026-09-02T04:00:00Z);
```

## Correlation stages

1. **Extraction candidates:** Find DLL or EXE creation initiated by common archive-handling programs.
2. **Subsequent file creation:** Match SHA256 and device name to a later creation at a different path, using writable-directory heuristics.
3. **Optional rename review:** Identify later file-renaming events for the matched hash.
4. **Candidate devices:** Find the earliest candidate file-behavior time per device.
5. **Scheduled tasks:** Review later `ScheduledTaskCreated` events on those devices, filtered for five-minute repetition or `RegExt.exe` in the event details.

The output includes task time, device name, first candidate time, task name, subject username, parsed action details, repetition intervals, and the original additional fields.

## Important implementation details

- Matching is at the device level for the final task join. The query does not prove that a task references or executes the earlier file.
- A later same-hash creation at another path is consistent with relocation or copying. It does not prove a filesystem move occurred.
- The rename branch is optional. Since all moved-file candidates are already included and renames occur later, unioning rename events does not change the candidate device set or earliest candidate time. Rename details are not returned in the final result. To inspect them, temporarily replace the final task query with `RenamedFileEvents`.
- The `SoftwareX`, `SoftwareY`, and `SoftwareZ` paths are exclusion placeholders from the supplied query. They require local review and tuning. They apply to the rename branch, not to all moved-file candidates.
- Campaign-related path and filename references are useful leads, not a complete behavior model. Most are scoped to particular stages or comments rather than mandatory conditions throughout the chain.

## Limitations and validation

Benign installers, updaters, and administrative tasks can produce similar activity. Sparse telemetry, missing hashes, schema differences, and task-content serialization can affect results. The time window bounds the overall search; there is no separate maximum delay between a candidate file event and task creation.

The repository has been reviewed for consistency with the supplied query. It has not been executed against a live KQL workspace as part of preparing this public version. No production deployment, detection accuracy, or measured operational impact is claimed.

## Portfolio

[Website case study](https://www.jordanmeisels.com/technical-work#scheduled-task-hunt) · [GitHub profile](https://github.com/JMeisels)
