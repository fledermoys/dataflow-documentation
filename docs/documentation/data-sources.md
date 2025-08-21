# Data Sources
Dataflow allows you to use either local data files or Google Sheets data for reversioning and batch processing. The following will teach you how the data needs to be setup in order to work with Dataflow.

## Dataflow Columns
Dataflow Columns are predefined keys/column names that are reserved for use of main features of the tool. These are case sensitive and may result in errors if used as a dynamic data source instead of for its actual functionality.


| <div style="width:100px">Column / Key</div> | Function| <div style="width:200px">Notes</div> |
|----------|----------|----------|
|target| Specifies the target composition that will be rendered by Dataflow. Can be used to switch between compositions per job. | **Must be defined.**If no composition is defined, or the specified composition cant be found in the Project, Batch Rendering will be stopped. Agent will skip this row and mark it as "error". |
|aep| Dataflow allows you to switch between After Effects Projects on a per row basis. This opens up the possibility to batch render across unlimited amounts of projects using the same machine or data source.| **Values must be absolute file paths**. If undefined or not found, it will render the row from the current After Effects Project. |
|output| Setting output values for your Jobs, allows you to have dynamic filenames and destinations for your renders. | If not specified or empty, Dataflow will use the composition name, which may lead to overwrites. Its highly recommended to define individual output names in your data source. |
|render-settings| Allows you to select an After Effects Render Settings Template for your outputs via your data source.| **Case Sensitive.** Only use values that match installed Render Setting Templates on your machine. If no matching template is found, the row will be skipped. If left empty, will use After Effects Default Render Settings |
|output-module| Allows you to select an After Effects Output Module Template for your outputs via your data source.| **Case Sensitive.** Only use values that match installed Output Module Templates on your machine. If no matching template is found, the row will be skipped. If left empty, will use After Effects Default Module |
|**Agent**|||
|render-status| This column specifies the status of a render job, allowing the Agent to scan the data source for ready-to-render jobs. This enables new data to be dynamically processed by the Agent. Once a job is successfully rendered, the Agent will set the render-status value to **finished**. | Must exist when using Agent. See [Data Source for Agent Mode](#data-source-for-agent-mode) for more details. | 


## Sample Sheet
|<div style="width:100px">render-status</div> | Cat Names |<div style="width:100px">target</div>|aep|output|<div style="width:150px">render-settings</div>|<div style="width:300px">output-module</div>|
|-|-|-|-|-|-|-|
|finished|Daisy|CatsComp_9x16_10s|T:/Projects/2025_CatsCampaign/CatsDaisy.aep|Daisy_CatsCampaign_9x16_10s|Best Settings|H.264 - Match Render Settings - 15Mbps
|finished|Molly|CatsComp_1x1_6s|T:/Projects/2025_CatsCampaign/CatsMolly.aep|Molly_CatsCampaign_1x1_6s|Best Settings|Lossless
|rendering...|Luna|CatsComp_16x9_15s|T:/Projects/2025_CatsCampaign/CatsLuna.aep|Luna_CatsCampaign_16x9_15s|Best Settings|Lossless with Alpha
|ready|Poppy|CatsComp_4x5_8s|T:/Projects/2025_CatsCampaign/CatsPoppy.aep|Poppy_CatsCampaign_4x5_8s|Best Settings|Lossless
|ready|Lily|CatsComp_1x1_10s|T:/Projects/2025_CatsCampaign/CatsLily.aep|Lily_CatsCampaign_1x1_10s|Best Settings|H.264 - Match Render Settings - 15Mbps

## Sample JSON
```json title="DataflowSource.json"
[
  {
    "render-status": "finished",
    "Cat Names": "Daisy",
    "target": "CatsComp_9x16_10s",
    "aep": "T:/Projects/2025_CatsCampaign/CatsDaisy.aep",
    "output": "Daisy_CatsCampaign_9x16_10s",
    "render-settings": "Best Settings",
    "output-module": "H.264 - Match Render Settings - 15Mbps"
  },
  {
    "render-status": "finished",
    "Cat Names": "Molly",
    "target": "CatsComp_1x1_6s",
    "aep": "T:/Projects/2025_CatsCampaign/CatsMolly.aep",
    "output": "Molly_CatsCampaign_1x1_6s",
    "render-settings": "Best Settings",
    "output-module": "Lossless"
  },
  {
    "render-status": "rendering...",
    "Cat Names": "Luna",
    "target": "CatsComp_16x9_15s",
    "aep": "T:/Projects/2025_CatsCampaign/CatsLuna.aep",
    "output": "Luna_CatsCampaign_16x9_15s",
    "render-settings": "Best Settings",
    "output-module": "Lossless with Alpha"
  },
  {
    "render-status": "ready",
    "Cat Names": "Poppy",
    "target": "CatsComp_4x5_8s",
    "aep": "T:/Projects/2025_CatsCampaign/CatsPoppy.aep",
    "output": "Poppy_CatsCampaign_4x5_8s",
    "render-settings": "Best Settings",
    "output-module": "Lossless"
  },
  {
    "render-status": "ready",
    "Cat Names": "Lily",
    "target": "CatsComp_1x1_10s",
    "aep": "T:/Projects/2025_CatsCampaign/CatsLily.aep",
    "output": "Lily_CatsCampaign_1x1_10s",
    "render-settings": "Best Settings",
    "output-module": "H.264 - Match Render Settings - 15Mbps"
  }
]
```

## Data Source for Agent Mode

If you want to use agent mode to have a 24/7 renderbot which renders on demand, you need to add a collumn/key called **render-status** to your data soure.
This render-status has 4 states:

* **ready**: Asset is ready to render.
* **processing**: Asset is currently being rendered/processed.
* **error**: Asset rendering failed / missing data / skipped or aborted for other reasons.
* **finished**: Asset finished rendering!

This is needed so the Agent knows which Assets it is allowed to render.
!!! info "Info"
    When connecting multiple Sheets, the agent will scan the sheets in the order you selected them in the sheet selector.
    Therefore you need to select data soruces based on rendering priority.

