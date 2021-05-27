---
title: Tracking Experiments and Visualizing Results
---

While an experiment is running, and any time after it finishes, track it and visualize the results in the **ClearML Web UI**,
including:

* [Execution details](#execution-details) - Code, the base Docker image used for **ClearML Agent**, output destination for artifacts, and the logging level.
* [Configuration](#configuration) - Hyperparameters, user properties, and configuration objects.
* [Artifacts](#artifacts) - Input model, output model, model snapshot locations, other artifacts.
* [General information](#general-information) - Information about the experiment, for example: the experiment start, create, and last update times and dates, user creating the experiment, and its description.
* [Console](#console) - stdout, stderr, output to the console from libraries, and **ClearML** explicit reporting.
* [Scalars](#scalars) - Metric plots.
* [Plots](#other-plots) - Other plots and data, for example: Matplotlib, Plotly, and **ClearML** explicit reporting.
* [Debug samples](#debug-samples) - Images, audio, video, and HTML.

## Viewing modes

The **ClearML Web UI** provides two viewing modes for experiment details:

* The info panel

* Full screen details mode.

Both modes contain all experiment details. When either view is open, switch to the other mode by clicking <img src="/docs/latest/icons/ico-info-min.svg" className="icon size-md space-sm" />
(**View in experiments table / full screen**), or clicking <img src="/docs/latest/icons/ico-bars-menu.svg" alt="Bars menu" className="icon size-sm space-sm" /> (**menu**) > **View in experiments
table / full screen**.


### Info panel

The info panel keeps the experiment table in view so that [experiment actions](webapp_exp_table#clearml-actions-from-the-experiments-table)
can be performed from the table (as well as the menu in the info panel).

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_40.png)

</div>
</details>

### Full screen details view

The full screen details view allows for easier viewing and working with experiment tracking and results. The experiments
table is not visible when the full screen details view is open. Perform experiment actions from the menu.

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_33.png)

</div>
</details>


## Execution details
In the EXECUTION tab of an experiment's detail page, there are records of:
* Source code
* **ClearML Agent** configuration
* Output details
* Uncommitted changes
* Installed Python packages


### Source code, ClearML Agent configuration, and output details

The source code details of the EXECUTION tab of an experiment include:
* The experiment's repository
* Commit ID
* Script path
* Working directory

Additionally, there is information about the **ClearML Agent** configuration.  The **ClearML Agent** base image is a pre-configured Docker
that **ClearML Agent** will use to remotely execute this experiment (see [Building Docker containers](../clearml_agent.md#building-docker-containers)).

The output details include:
* The output destination used for storing model checkpoints (snapshots) and artifacts (see also, [default_output_uri](../configs/clearml_conf#config_default_output_uri)
  in the configuration file, and [output_uri](../references/sdk/task.md#taskinit)
  in `Task.init` parameters).

* The logging level for the experiment, which uses the standard Python [logging levels](https://docs.python.org/3/howto/logging.html#logging-levels).


<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_18.png)

</div>
</details>


### Uncommitted changes

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_19.png)

</div>
</details>


### Installed Python packages and their versions
<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_20.png)

</div>
</details>

## Configuration

All parameters and configuration objects appear in the **CONFIGURATION** tab.


### Hyperparameters

:::important
In older versions of **ClearML Server**, the **CONFIGURATION** tab was named **HYPER PARAMETERS**, and it contained all parameters. The renamed tab contains a **HYPER PARAMETER** section, and subsections for hyperparameter groups.
:::

Hyperparameters are grouped by their type and appear in **CONFIGURATION** **>** **HYPER PARAMETERS**.

#### Command line arguments

The **Args** section shows automatically logged `argparse` arguments, and all older experiments parameters, except TensorFlow Definitions. Hover over a parameter, and the type, description, and default value appear, if they were provided.

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_22.png)

</div>
</details>


#### Environment variables

If the `CLEARML_LOG_ENVIRONMENT` variable was set, the **Environment** section will show environment variables (see [this FAQ](../faq#track-env-vars)).

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_23.png)

</div>
</details>


#### Custom parameter groups

Custom sections shows parameter dictionaries, if the parameters were connected to the Task, using the `Task.connect` method,
with a `name` argument provided.

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_25.png)

</div>
</details>

#### TensorFlow Definitions

The **TF_DEFINE** sections shows automatic TensorFlow logging.

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_26.png)

</div>
</details>

Once an experiment is run and stored in **ClearML Server**, any of these hyperparameters can be [modified](webapp_exp_tuning.md#modifying-experiments).

### User properties

User properties allow to store any descriptive information in a key-value pair format. They are editable in any experiment,
except experiments whose status is *Published* (read-only).

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_21.png)

</div>
</details>


### Configuration objects

**ClearML** tracks experiment (Task) model configuration objects, which appear in **Configuration Objects** **>** **General**.
These objects include those that are automatically tracked, and those connected to a Task in code (see [Task.connect_configuration](../references/sdk/task.md#connect_configuration)).
**ClearML** supports providing a name for a Task model configuration (see the [name](../references/sdk/task.md#connect_configuration)
parameter in `Task.connect_configuration`.

:::important
In older versions of **ClearML Server**, the Task model configuration appeared in the **ARTIFACTS** tab, **MODEL CONFIGURATION** section. Task model configurations now appear in the **Configuration Objects** section, in the **CONFIGURATION** tab.
:::

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot - Configuration objects </summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_24.png)

</div>
</details>
<br/>

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot - Custom configuration object</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_28.png)

</div>
</details>




## Artifacts

Artifacts tracked in an experiment appear in the **ARTIFACTS** tab, and include models and other artifacts.

Copy the location of models and artifacts stored in local files (`file://`) to the clipboard. Download models and artifacts in remote storage (for example `https://` or `s3`).

### Models

The input and output models appear in the **ARTIFACTS** tab. Models are associated with the experiment, but to see further model details,
including design, label enumeration, and general information, go to the **MODELS** tab, by clicking the model name, which is a hyperlink to those details.

**To retrieve a model:**

1. In the **ARTIFACTS** tab **>** **MODELS** **>** **Input Model** or **Output Model**, click the model name hyperlink.
1. In the model details **>** **GENERAL** tab **>** **MODEL URL**, either:

    * Download the model<img src="/docs/latest/icons/ico-download.svg" className="icon size-md space-sm" />, if it is stored in remote storage.
    * Copy its location to the clipboard <img src="/docs/latest/icons/ico-clipboard.svg" alt="Copy Clipboard" className="icon size-md space-sm" />,
      if it is in a local file.


<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_exp_artifacts_01.png)

</div>
</details>


### Other artifacts

**To retrieve another artifact:**

1. In the **ARTIFACTS** tab **>** **DATA AUDIT** or **OTHER** **>** Select an artifact **>** Either:

    * Download the artifact <img src="/docs/latest/icons/ico-download.svg" className="icon size-md space-sm" />, if it is stored in remote storage.
    * Copy its location to the clipboard <img src="/docs/latest/icons/ico-clipboard.svg" alt="Copy Clipboard" className="icon size-md space-sm" />,
      if it is in a local file.

#### Data audit

Artifacts which are uploaded and dynamically tracked by **ClearML** appear in the **DATA AUDIT** section. They include the file path, file size, hash, and metadata stored with the artifact.


<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_29.png)

</div>
</details>

#### Other

Other artifacts, which are uploaded but not dynamically tracked after the upload, appear in the **OTHER** section. They include the file path, file size, and hash.

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_30.png)

</div>
</details>




## General information

General experiment details appear in the **INFO** tab. This includes information describing the stored experiment:
* The parent experiment
* Project name
* Creation, start, and last update dates and times
* User who created the experiment
* Experiment state (status)
* Whether the experiment is archived

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_31.png)

</div>
</details>




## Experiment results




### Console

The complete experiment log containing everything printed to stdout and strerr appears in the **CONSOLE** tab. The full log
is downloadable. To view the end of the log, click **Jump to end**.

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_32.png)

</div>
</details>



### Scalars

All scalars that **ClearML** automatically logs, as well as those explicitly reported in code, appear in **RESULTS** **>** **SCALARS**.

#### Scalar plot tools

Use the scalar tools to improve analysis of scalar metrics. In the info panel, click <img src="/docs/latest/icons/ico-settings.svg" className="icon size-md space-sm" /> to use the tools. In the full screen details view, the tools
are on the left side of the window. The tools include:
* **Group by** - select one of the following:
  * **Metric** - all variants for a metric on the same plot

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_33.png)

</div>
</details>

* **None** - Group by metric-variant combination (individual metric-variant plots).

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_34.png)

</div>
</details>

* Show / hide plots - Click **HIDE ALL**, and then click <img src="/docs/latest/icons/ico-show.svg" alt="Eye Show All" className="icon size-md space-sm" />
  on those you want to see.
* **Horizontal axis** modes (scalars, only) - Select one of the following:
  * **ITERATIONS**
  * **RELATIVE** - time since experiment began
  * **WALL** - local clock time
* Curve smoothing (scalars, only) - In **Smoothing** **>** Move the slider or type a smoothing factor between **0** and **0.999**.


#### Plot controls

Each plot supports plot controls allowing you better analyze the results. The table below lists the plot controls which may be available for any plot. Hover over a plot, and the controls appear.

|Icon|Description|
|---|---|
| ![image](../img/svg/download-png.svg) | Download plots as PNG files. |
| ![image](../img/svg/pan.svg) | Pan around plot. Click ![image](../img/svg/pan.svg), click the plot, and then drag. |
| ![image](../img/svg/dotted-box.svg) | To examine an area, draw a dotted box around it. Click ![image](../img/svg/dotted-box.svg) and then drag. |
| ![image](../img/svg/dotted-lasso.svg) | To examine an area, draw a dotted lasso around it. Click ![image](../img/svg/dotted-lasso.svg) and then drag. |
| ![image](../img/svg/zoom.svg) | Zoom into a section of a plot. Zoom in - Click ![image](../img/svg/zoom.svg) and drag over a section of the plot. Reset to original scale - Click ![image](../img/svg/reset-scale.svg). |
| ![image](../img/svg/zoom-in.svg) | Zoom in. |
| ![image](../img/svg/zoom-out.svg) | Zoom out. |
| ![image](../img/svg/reset-autoscale.svg) | Reset to autoscale after zooming ( ![image](../img/svg/zoom.svg), ![image](../img/svg/zoom-in.svg), or ![image](../img/svg/zoom-out.svg) ). |
| ![image](../img/svg/reset-axes.svg) | Reset axes after a zoom.
| ![image](../img/svg/spike-lines.svg) | Show / hide spike lines. |
| ![image](../img/svg/show-closest.svg) | Show the closest data point on hover, including horizontal and vertical axes values. Click ![image](../img/svg/show-closest.svg) and then hover over a series on the plot. |
| ![image](../img/svg/compare-data.svg) | Compare data on hover. Click ![image](../img/svg/compare-data.svg) and then hover over the plot. |
| ![image](../img/svg/logarithmic-view.svg) | Switch to logarithmic view. |
| ![image](../img/svg/legend.svg) | Hide / show the legend. |
| ![image](../img/svg/download-json.svg) | To get metric data for further analysis, download plot data to JSON file. |


### Other plots

Other plots include data reported by libraries, visualization tools, and **ClearML** explicit reporting. These may include
2D and 3D plots, tables (Pandas and CSV files), and Plotly plots. Other plots appear in **RESULTS** **>** **PLOTS**.
Individual plots can be shown / hidden or filtered by title.

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_35.png)

</div>
</details>








### Debug samples

View debug samples by metric at any iteration. The most recent iteration appears first. Use the viewer / player to inspect images, audio, video samples and do any of the following:

* Move to the same sample in a different iteration (move the iteration slider).
* Show the next or previous iteration's sample.
* Download the file <img src="/docs/latest/icons/ico-download.svg" className="icon size-md space-sm" />.
* Zoom.
* View the sample's iteration number, width, height, and coordinates.


<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot - Debug samples</summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_43.png)

</div>
</details>

<br/>

<details className="cml-expansion-panel screenshot">
<summary className="cml-expansion-panel-summary">View a screenshot - Viewer </summary>
<div className="cml-expansion-panel-content">

![image](../img/webapp_tracking_44.png)

</div>
</details>
<br/>

**To view debug samples:**

1. Click the **DEBUG SAMPLES** tab. The most recent iteration appears at the top.
1. Locate debug samples by doing the following:

    * Filter by metric. In the **Metric** list, choose a metric.
    * Show other iterations. Click <img src="/docs/latest/icons/ico-circle-older.svg" className="icon size-md space-sm" /> (Older images), <img src="/docs/latest/icons/ico-circle-newer.svg" className="icon size-md space-sm" /> (New images), or <img src="/docs/latest/icons/ico-circle-newest.svg" className="icon size-md space-sm" /> (Newest images).

**To view a debug sample in the viewer / player:**

1. Click the debug sample click the thumbnail.

1. Do any of the following:

    * Move to the same sample in another iteration - Move the slider, or click **<** (previous) or **>** (next).
    * Download the file - Click <img src="/docs/latest/icons/ico-download.svg" className="icon size-md space-sm" />.
    * Zoom
    * For images, locate a position on the sample - Hover over the sample and the X, Y coordinates appear in the legend below the sample.




## Tagging experiments

Tags are user-defined, color-coded labels that can be added to experiments (and models), allowing to easily identify and
group experiments. Tags can show any text. For example, add tags for the type of remote machine experiments were executed
on, label versions of experiments, or apply team names to organize experimentation.

* To add tags and change tag colors:
    1. Click the experiment **>** Hover over the tag area **>** **+ADD TAG** or <img src="/docs/latest/icons/ico-bars-menu.svg" alt="Bars menu" className="icon size-sm space-sm" /> (menu)
    1. Do one of the following:
        * Add a new tag - Type the new tag name **>** **(Create New)**.
        * Add an existing tag - Click a tag.
        * Change a tag's colors - Click **Tag Colors** **>** Click the tag icon **>** **Background** or **Foreground** **>** Pick a color **>** **OK** **>** **CLOSE**.
* To remove a tag - Hover over the tag **>** **X**.




## Locating the experiment (Task) ID

* In the info panel, in the top area, to the right of the Task name, click **ID**. The Task ID appears.