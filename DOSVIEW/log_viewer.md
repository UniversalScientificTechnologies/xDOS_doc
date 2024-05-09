---
layout: page
title: "DOSVIEW: Log viewer"
permalink: /dosview/log_viewer
parent: DOSVIEW
nav_order: "1"
---

# xDOS log viewer

#### Introduction
`log_viewer` is a part of the `dosview` application, designed for viewing and analyzing log data from dosimeters. This tool enables users to display crucial log file information, including the time evolution of intensity and the energy spectrum. Metadata associated with the logs are also displayed, enhancing the understanding and utility of the data.


#### Features
- **Graphical Display**: Visualizes time evolution of radiation intensity and the energy spectrum in graphical formats.
- **Metadata Display**: Shows associated metadata with each log entry, providing context and additional details about the data.

#### Usage
`dosview` can be operated both via the command line and through its graphical user interface (GUI).

**Command Line:**
To run `dosview` from the command line, you can directly pass the log file name as an argument:
```bash
dosview [file_name]
```
This command will open the specified log file directly in the `dosview` application.

**Graphical Interface:**
Alternatively, `dosview` can be started without specifying a file by command:
```bash
dosview
```
Or by system application list. 
Once opened, navigate through the menu by selecting `File -> Open`, then choose the log file you wish to view. The log will then be opened as a new tab within the graphical interface of `dosview`.

**From file explorer**
TODO


#### Examples
Here's a simple example of how to run `dosview`:

```bash
dosview example_logfile.log
```

This command will open the specified log file and display the intensity and energy spectrum graphs.
