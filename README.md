# `<>`RevSharp

**C# Scripting for Autodesk Revit**

Write and execute C# scripts directly inside Revit — live, against your actual model, with no recompiling and no restarting required.

---

## What is RevSharp?

RevSharp is a script runner and ribbon button manager for Autodesk Revit, built for MEP engineers, BIM managers, and Revit API developers who want to automate without the traditional add-in development cycle.

---

## Features

- **Live script execution** — write C# and hit Run. Your script executes against your live Revit model instantly
- **No recompiling** — Roslyn compiles your script in memory at runtime. No Visual Studio round-trip required
- **No restarting Revit** — iterate on your script and run it again immediately
- **Instant error feedback** — compile errors surface with exact line numbers in the output pane
- **Ribbon button library** — save scripts as pushbuttons on the RevSharp ribbon tab
- **Hyperfast deployment** — drop a script file in a folder, click Reload, and a new ribbon button appears for every team member
- **Silent mode** — add `// @silent` to suppress the editor window on successful runs
- **Console output** — use `Console.WriteLine()` to print results to the built-in output pane
- **Revit 2025, 2026, and 2027** support

---

## Demo

> *Query a pipe network, bulk renumber sheets, and color code pipe systems by type — all in under 60 seconds.*

*(Video coming soon)*

---

## Installation

1. Download the latest `RevSharpInstaller.msi` from the [Releases](../../releases) page
2. Run the installer — it detects your installed Revit versions automatically
3. Launch Revit — look for the **RevSharp** tab in the ribbon

No manual file copying. No editing `.addin` files. No path configuration.

---

## Getting Started

### Script Editor

Click **Script Editor** in the RevSharp ribbon tab to open the editor window. The following variables are available in every script without any declaration:

| Variable | Type | Description |
|---|---|---|
| `uiapp` | `UIApplication` | Top-level Revit application handle |
| `uidoc` | `UIDocument` | The active document in the UI |
| `doc` | `Document` | The Revit DB document |

The following namespaces are pre-injected:

```csharp
Autodesk.Revit.DB
Autodesk.Revit.DB.Architecture
Autodesk.Revit.DB.Electrical
Autodesk.Revit.DB.Mechanical
Autodesk.Revit.DB.Plumbing
Autodesk.Revit.DB.Structure
Autodesk.Revit.UI
Autodesk.Revit.UI.Selection
System
System.Collections.Generic
System.IO
System.Linq
System.Text
```

### Example Script

```csharp
var walls = new FilteredElementCollector(doc)
    .OfClass(typeof(Wall))
    .WhereElementIsNotElementType()
    .ToList();

Console.WriteLine($"Found {walls.Count} walls");
```

---

## Script Library — Ribbon Buttons

RevSharp scans `Documents\RevSharp\` for scripts and builds ribbon buttons automatically.

### Folder Structure

```
Documents\
    RevSharp\
        My Tools.panel\
            Count Walls.pushbutton\
                CountWalls.cs        (any .cs filename)
                icon.png             (optional, 32x32 PNG)
            Mark Elements.pushbutton\
                MarkElements.cs
        MEP Tools.panel\
            Pipe Summary.pushbutton\
                PipeSummary.cs
```

- Each `*.panel` folder becomes a ribbon panel under the RevSharp tab
- Each `*.pushbutton` folder becomes a ribbon button in that panel
- One `.cs` file per pushbutton — any filename works
- Click **Reload Scripts** in the ribbon to pick up new buttons without restarting Revit

### Silent Mode

Add `// @silent` as the very first line of any script to suppress the editor window on a successful run. If the script errors, the editor always opens regardless.

```csharp
// @silent
var walls = new FilteredElementCollector(doc)
    .OfClass(typeof(Wall))
    .WhereElementIsNotElementType()
    .ToList();
// runs silently, no window opened on success
```

---

## System Requirements

| Requirement | Version |
|---|---|
| Autodesk Revit | 2025, 2026, or 2027 |
| Windows | 10 or 11 (64-bit) |
| .NET | 8.0 (included with Revit 2025+) |

---

## Beta Program

RevSharp is currently in beta. I am looking for:

- MEP engineers who automate Revit workflows
- BIM managers deploying tools across teams
- Revit API developers who want faster iteration

If that is you, **open an Issue** on this repository or connect with me on [LinkedIn](https://www.linkedin.com/in/bo-alambis/) to get set up.

---

## Roadmap

- [ ] Shared network folder support for team-wide script libraries
- [ ] Script versioning and update notifications
- [ ] WiX MSI installer with auto-update
- [ ] Script marketplace / community library
- [ ] GitHub sync for script libraries

---

## License

RevSharp is proprietary software. The source code is not publicly available.

RevSharp is free to use for personal and internal business use.  

See [LICENSE](LICENSE.md) for full terms.  
For commercial licensing: revsharp.admin@gmail.com

---

## Contact

**Bo Alambis**
[LinkedIn](https://www.linkedin.com/in/bo-alambis/) · [Email](revsharp.admin@gmail.com)

---

*Built with Roslyn · AvalonEdit · Autodesk Revit API · .NET 8*
