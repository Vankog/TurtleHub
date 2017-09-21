# TurtleHub
[TortoiseGit](https://tortoisegit.org/) issue tracker plugin for projects hosted on GitHub. Release versions can be 
downloaded on the [Release](../../releases) page.

![TH-issue-overview](/docs/img/TH-issue-overview.png  "Example of TurtleHub's issue picker.")

**Note:** This project is not affiliated with or endorsed by GitHub, Inc.

## Setup
1. Obviously, [TortoiseGit](https://tortoisegit.org/) (and therefore Git) must be installed. 
1. Install TurtleHub with the setup file suitable for your system at the given default location.
1. Integrate TurtleHub with your project. There are two ways to do this:
    ### a) Local Integration
    This is a simple setup for a local repository.

    Use this if you...
    * want to use TurtleHub only locally without sharing the setup.
    * **and** do not plan to change the file path to the desired local repository.
    
    **On how to setup Local Integration see [Local Integration in Setup.md](./docs/Setup.md#a-local-integration).**

    ### b) BugTraq Integration
    *BugTraq* is a configuration effort to integrate issue trackers into version control systems. Therefore it is 
    independent from TurtleHub. It is mainly known from SVN but found integration into Git as well. It uses the Git 
    configuration hierarchy and thus can be local, shared, global or system wide. 

    While the general BugTraq configuration is TortoiseGit independent, the plugin-specific setup of TurtleHub 
    listed below should be able to work specifically for the whole *Tortoise-* family. Though, it was not tested for 
    TortoiseSVN or other implementations, yet. Feel free to test it and give us feedback.

    Use this if you...
    * want to setup a shared configuration for your project or system.
    * **or** want to set up a portable tracker integration. i.e. independently from your local repository path like on 
    portable mediums.
    
    Because of the benefits, we recommend this option over the *Local Integration*, even if you want to use it only 
    locally.

    **On how to setup BugTraq Integration see 
    [BugTraq Integration in Setup.md](./docs/Setup.md#b-bugtraq-integration)**..
    
    **For further BugTraq configurations about issue linking and a fallback for users without TurtleHub, see 
    [Further BugTraq configuration in Setup.md](./docs/Setup.md#further-bugtraq-configuration).**

## Usage
When committing, the issue chooser should appear at the top right of the dialog. Open it and let TurtleHub fetch the 
issues. If you want to see pull requests, too, enable the checkbox at the bottom.
Select your desired issues. These will be inserted into your log message.

## Development
The code is developed using Visual Studio 2015. In order to develop TurtleHub, first use one of the installers and 
keep the default installation directory. When Visual Studio builds the new DLL it will copy over the installed files.

Running the `build.cmd` batch file will build the installers and place them in the `bin` directory.

## License
This code is released under the [GNU General Public License version 2](http://www.gnu.org/licenses/gpl-2.0.txt).
