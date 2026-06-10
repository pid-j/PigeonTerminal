# PigeonTerminal

## What is PigeonTerminal?

PigeonTerminal is a [TurboWarp](https://turbowarp.org)-based terminal operating system. It is the spiritual successor to [ChickenTerminal](https://github.com/pid-j/ChickenTerminal).

## How do I use PigeonTerminal?

PigeonTerminal is a terminal operating system, so it is recommended to know how to use a terminal. It is built for computer devices, so mobile users will have to wait until support is added.

Please follow the setup after opening PigeonTerminal. You can open a preview at [this link](https://turbowarp.org/fullscreen?project_url=raw.githubusercontent.com/pid-j/PigeonTerminal/refs/heads/main/PigeonTerminal%20PB1.sb3).

### Setup

When you first open PigeonTerminal, you will be met with a textbox that says "Your configuration is missing or corrupted - please click the button to continue to setup." Click the button, and then follow its directions.

The first section of setting up is the user creation section. You will be asked to provide a username and a password. If you provide no password, the password stage will be skipped. You will then be asked if you would like to create more users. Once you are done creating users, you will be asked if the profiles are good, or if you would like to restart.

After setting up your profiles, you will be asked if you would like to load a filesystem from a file. Otherwise, a default filesystem will be set up. **NOTE:** The filesystem has home directories, so you may have to do cleanup if the profiles you made when exporting the filesystem are different to the profiles you have just set up.

After setting up your filesystem, you will be asked to type the name of the user to grant root privileges. This can be changed later. You have completed the initial setup, but you will still need to make per-profile configurations when you log into them.

### Configuration

After the setup ends, the system will restart and you will be asked to log in. You can either:

- log into a user you have made, or
- shut down the system by providing an empty answer.

If you choose to log in, the system will tell you that this user does not have any configuration. You will be asked if you have a URL to copy a configuration from. For first-time users, use the default configuration at the link `https://raw.githubusercontent.com/pid-j/PigeonTerminal/refs/heads/main/cfg.json` or use another public configuration.

For advanced users, the following configuration options are provided.

- Background color (default: #000000)
- Foreground color (default: #ffffff)
- Font family (default: monospace)
- Font size (default: 0.75em)
- Fatal error color (default: #ff0000)
- Warning color (default: #ff8000)
- Success color (default: #00ff00)
- Command parser (default: [ps](https://github.com/pid-j/PigeonScript))
    - Architecture (only zip is supported for now): The method of interaction between PigeonTerminal and the parser. The `zip` option uses the [Zip extension](https://extensions.turbowarp.org/CST1229/zip), and switches to a provided zip archive with a specific ID. This ID is provided in the following format: `{"arch": ["zip", "PARSER_ID"]}`. More architectures may be implemented into the future.
    - Alias: The command that will run the parser. Usually has a short length.
    - Broadcast: The name of the broadcast that, when received by the parser, executes the script provided.
    - Main file: The name of the file that will be used as the entry point to the program, along with the file extension.
    - Link: A link to an always-updated version of the parser that has dedicated support for integration with PigeonTerminal.
- HTML code
    - Constants: Constants that are provided by PigeonTerminal from the configuration are: `$FONTSIZE`, `$FONTFAMILY`, `$COLOR`, `$BACKGROUND`, `$FATALCOLOR`, `$WARNINGCOLOR`, and `$SUCCESSCOLOR`.
    - Messages: The parent window will send messages to the terminal viewer in this format: `{"type": "TYPE_ID", "data": "..."}`. 
        - For terminal text changes, the messages will be sent through messages in this format: `{"type": "TERMINAL_UPDATED", "data": "TerminalData"}`, with the terminal data being encoded in Base64. To decode the messages, parse the data using `JSON.parse()` and decode the data using `atob(parsed.data)`.
        - For other types, just post them back to the parent. The `data` field will always be encoded in Base64.