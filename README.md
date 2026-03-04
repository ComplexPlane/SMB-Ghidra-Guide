# Getting Started with the SMB Ghidra Server

This guide will help you install Ghidra, open the shared SMB Ghidra project, and get started using Ghidra.

## Set up Ghidra

1. Install [OpenJDK 21](https://adoptium.net/temurin/releases/?version=21&os=any&arch=any).
2. Install [Ghidra](https://github.com/NationalSecurityAgency/ghidra) (see the installation instructions in the README).
3. Install the [GameCube Loader](https://github.com/Cuyler36/Ghidra-GameCube-Loader) and [SuperMonkeyBallTools](https://github.com/ComplexPlane/Ghidra-SuperMonkeyBallTools) Ghidra plugins. You can use the prebuilt releases instead of building from source.

## Open Shared Project

You'll need an account on the SMB shared Ghidra server - ask BombSquad for the server URL and to generate a username and temporary password for you.

Once you've made an account:

1. In Ghidra's main window, go to File -> New Project -> Shared Project
2. Enter the server URL and 13100 for the port
3. Login with your username and temporary password (please change password to something secure when asked). If you don't login within 24 hours of account creation, the temporary password will expire and you'll need to reset it again.
4. From the list of projects on the server, choose `mkb2-decompilation`
5. Double-click the `mkb2.main_loop.rel` file to open and checkout the decompilation. It contains all REL files and the DOL for Super Monkey Ball 2 combined.

## Using SuperMonkeyBallTools

The SuperMonkeyBallTools plugin lets you quickly jump between addresses in Ghidra and memory addresses in the game. This is useful because REL modules are not mapped to the same addresses in Ghidra as in the game, and they overlap in-game due to dynamic linking. Go to Window -> SMB: Convert Address to show the window with address conversions.

Also extremely useful: press Shift+G and paste in a game memory address to jump to the location in Ghidra.

In the Convert Address window, there are also buttons which can export symbols and C++ headers for SMB2PracticeMod and SMB2WorkshopMod.

## Labelling Stuff

Please try to gain some familiarity and confidence with the codebase before labelling things willy-nilly. A Ghidra decompilation is one big jigsaw puzzle that builds on itself, and overconfident labels can make things more confusing for others going forward.

We prefix labels with `g_` if we're not 100% sure what they are, or if we only have partial information about them. Please follow the same convention as you label things. For example:

- You see a function that renders bananas, but aren't 100% sure it doesn't render other things too. Call it `g_render_bananas`
- You see a global value related to how fonts are drawn, but aren't sure what it is specifically. A `g_` label is still better than nothing: `g_unk_font_drawing1`

Generally follow the Rust naming conventions: use `snake_case` for most function and variable names (not `camelCase`) and `PascalCase` for struct/enum names. Please only use letters, numbers, and underscores in your names.

## Collaborate on Shared Project

Your changes are saved locally (with Ctrl+S) until you decide to check in your changes to the server.
To check in your changes like committing in Git, in the project window right-click the file and choose "Check In".
To pull down the latest changes, right-click the file and choose "Update".
Checking in your changes often is recommended to avoid manual merges and so others can see your work.

## Learning Ghidra

* Ghidra Cheat Sheet (in your Ghidra install dir, under `docs/CheatSheet.html`)
* [Ghidra quickstart & tutorial: Solving a simple crackme - YouTube](https://www.youtube.com/watch?v=fTGTnrgjuGA&t=243s)

The Ghidra manual is also pretty readable and helpful (Help -> Contents).

## Optional Ghidra Settings

Here's some settings that I like personally, they're 100% optional though.

* I like to map my mouse's back/forward buttons to back/forward in Ghidra. To do this on Windows with [AutoHotkey](https://www.autohotkey.com/):
    ```ahk
    #IfWinActive CodeBrowser
    XButton1::
    Send, !{Left}
    return

    #IfWinActive CodeBrowser
    XButton2::
    Send, !{Right}
    return
    ```

