# #💾 Simple Save Tool Addon for Godot

An addon (plugin) for Godot 4.x that implements a Global Singleton (autoload) named **SAVEMANAGER** to simplify persistent data storage using Resources (.tres).

## ##⚙️ Features

- **Global Singleton:** Access your save system from any script as SAVEMANAGER.save_data() or SAVEMANAGER.get_data(...).
- **Resource-Based:** Built on top of Godot's Resource class for native, fast, and structured serialization.
- **Slot System:** Manage multiple save files (e.g., Save_0.tres, Save_1.tres) with built-in slot switching.
- **Ready to Use:** Includes both the SaveManager.gd logic and the SAVE resource class out of the box.

## ##🚀 Installation and Usage

### 1. Installation

1.  Download the addons/simple_save_tool folder.
2.  Copy the folder into your Godot project's addons/ directory.
3.  Go to **Project > Project Settings > Plugins**.
4.  Find **"Simple Save Tool"** and ensure it is **Enabled**.
5.  Ensure **SAVEMANAGER** is added as an **Autoload** (Project Settings > Autoload).

### 2. Usage Examples

The `SAVEMANAGER` handles a dictionary named `DATA` inside a `SAVE` resource. All data is persistent once `save_data()` is called.

### A. Storing and Retrieving Data

```gdscript
var player_name
var player_coins

# Storing data in the current session
SAVEMANAGER.set_data("player_name", "Aris")
SAVEMANAGER.set_data("coins", 150)

# Retrieving data (with optional default value if the key doesn't exist)
player_name = SAVEMANAGER.get_data("player_name", "Generic Hero")
player_coins = SAVEMANAGER.get_data("coins", 0)

```

<!-- #a default value can be passed in "get_data()" as an error handler, the function will return the default value if the key doesn't exist -->

### B. Saving and Loading (Disk)

`save_data() ` is an asynchronous operation. It is recommended to use await to ensure the file system has finished writin

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   func _on_save_button_pressed():      # Save current memory data to "user://Save_0.tres"      await SAVEMANAGER.save_data()      print("Game Saved Successfully!")  func _ready():      # Load existing data from disk into memory      SAVEMANAGER.load_data()   `

##### C. Slots and File Management

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   # Change the active slot (this automatically updates the file path)  SAVEMANAGER.change_slot(2) # Path becomes user://Save_2.tres  # Change the base file name  SAVEMANAGER.change_file_name("MyGameSave") # Path becomes user://MyGameSave_2.tres  # Wipe current slot data  SAVEMANAGER.delete_data()   `

## 📑 API Reference

### 1\. Methods

**MethodDescription**set_data(key: String, value: Variant)Adds or updates a value in the save dictionary.get_data(key, default)Returns the value for the key. If not found, creates it with the default value.save_data(time: float)**(Async)** Writes the data to disk. Emits will_save_data.load_data()Reads the file from disk and populates the manager. Emits load_data_done.delete_data()Deletes the physical file and resets the memory.change_slot(slot: int)Switches the active save slot (0, 1, 2, etc.).change_file_name(name: String)Changes the prefix of the save file.get_all_data()Returns the full Dictionary of the current save.

### 2\. Signals

- **will_save_data()**: Triggered just before the ResourceSaver begins writing.
- **load_data_done()**: Triggered after the ResourceLoader has finished updating the internal resource.
