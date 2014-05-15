##GeminiLogging
=============

A logging library for Apollo.

###GeminiLogging Methods
* **GetLogger** - returns a logger object
	* Requires an options table:
		* level - Most detailed level of log to display, see below

		* pattern - Output pattern using the following substitutions:
			* %d - Date
			* %l - Error Level
			* %c - Function Name
			* %n - Line Number
			* %m - Message Passed to Error function

		* appender - Destination for Error message output examples:
			* GeminiConsole - Outputs to GeminiConsole if present, Print otherwise
			* blank - Print Function
			* custom function - function takes 3 vars: self, message, level

###Logger Methods

All loggers accept either a table that will be outputted or a string.format string and arguments.

* debug - Generates a DEBUG level message

* info - Generates a INFO level message

* warn - Generates a WARN level message

* error - Generates a ERROR level message

* fatal - Generates a FATAL level message

* SetLevel - Can be used to dynamically change the log display level. Example:
	* ```lua glog:SetLevel("WARN") ```

###Logging Levels:

The following levels are available:

| Level | Description |
|:---------:|:------------------------------------------------------------------------------ |
| **DEBUG** | Fine-grained informational events that are most useful to debug an application |
| **INFO**  | Informational messages that highlight the progress of the application at coarse-grained level |
| **WARN**  | Potentially harmful situations |
| **ERROR** | Error events that might still allow the application to continue running |
| **FATAL** | Designates very severe error events that will presumably lead the application to abort |

###Example Usage:

```lua
local glog

function MyAddon:OnLoad()
	local tGeminiLogging = Apollo.GetPackage("Gemini:Logging-1.2").tPackage
	glog = GeminiLogging:GetLogger({
        level = GeminiLogging.FATAL,
        pattern = "%d %n %c %l - %m",
        appender = "GeminiConsole"
    })
end

function MyAddon:DoFoo(strBaz, nBar, tBat)
	glog:debug("Baz: %s; Bar: %d", strBaz, nBar)
	glog:info(tBat)
	...
end
```