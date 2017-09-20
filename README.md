# TurtleHub
[TortoiseGit](https://tortoisegit.org/) issue tracker plugin for projects hosted on GitHub. Release versions can be 
downloaded on the [Release](https://github.com/dail8859/TurtleHub/releases) page.

![TH-issue-overview](/img/TH-issue-overview.png)

**Note:** This project is not affiliated with or endorsed by GitHub, Inc.

## Setup
1. Obviously, [TortoiseGit](https://tortoisegit.org/) (and therefore Git) must be installed. 
1. Install TurtleHub at the given default location.
1. Integrate TurtleHub with your project. There are two ways to do this:
    ### a) *Local Integration*
    This is a simple setup for a local repository.

    Use this if you...
    * want to use TurtleHub only locally without sharing the setup.
    * *and* do not plan to change the file path to the desired local repository.

    ### b) BugTraq Integration
    *BugTraq* is a configuration effort to integrate issue trackers into version control systems. Therefore it is 
    independent from TurtleHub. It is mainly known from SVN but found integration into Git as well. It uses the Git 
    configuration hierarchy and thus can be local, shared, global or system wide. 

    While the general BugTraq configuration is TortoiseGit independent, the plugin-specific setup of TurtleHub 
    listed below should be able to work specifically for the whole *Tortoise-* family. Though, it was not tested for 
    TortoiseSVN or other implementations, yet. Feel free to test it and give us feedback.

    Use this if you...
    * want to setup a shared configuration for your project or system.
    * *or* want to set up a portable tracker integration. i.e. independently from your local repository path like on 
    portable mediums.
    
    Because of the benefits, we recommend this option over the *Local Integration*, even if you want to use it only 
    locally.


### a) Local Integration
#### Steps:
1. Once TurtleHub is installed, open the context menu and go to `TortoiseGit > Settings > Issue Tracker Integration`.
1. Click `Add...`. TurtleHub should show up under the `Providers` dropdown menu.
1. The `Working Tree Path` should be set to the directory of a local git repository.
1. Click `Options`
    1. Add the *owner* and *repository name* located on GitHub. You can get these for example from the URL of the 
    repository: e.g. for `https://github.com/dail8859/TurtleHub` the owner is `dail8859` and the repository name is 
    `TurtleHub`.
    1. The *keyword* indicates the prefix TurtleHub uses when you choose and insert issues into the log message. This 
    might be `Closes`, for example, and will format to something like `Closes #1234`. With any of the predefined 
    keywords in place, Github can close a mentioned issue automatically 
    ([see Github documentation](https://help.github.com/articles/closing-issues-using-keywords/)). However, the keyword 
    is completely customizable. If you don't want to use Github's auto-close feature every time, simply choose `<None>` 
    or - after closing the Options dialog - edit the `Parameters` field `keyword=` manually to whatever you like.
    
        ![TH-options](/img/TH-options.png)
        ![TH-config-keyword](/img/TH-config-keyword.png)
    1. *Reference Full Repository Name* enables the extended notation when inserting the issue number into the log 
    message. This is needed if the repository you are pushing to is not on the same repository as the issues or pull 
    requests you are referencing. This means: Github parses the short notation `#1234` assuming the current repository. 
    This is suitable for your own repositories. However, for forks you may want to use the issues or pull requests of 
    the original/upstream repository instead. For this to work, Github needs the full reference in the 
    form `another-owner/external-repository#1234`. This extended notation works always, while the simple notation 
    should only be used if you are sure you are in the same repository as the issues or pull requests you are 
    referencing. Please note, as you usually only have read rights on external repositories, you might want to remove 
    or replace the `Closes` (or equivalent) keyword. (see previous screenshot)
    
        ![TH-options-external-repo](/img/TH-options-external-repo.png)

### b) BugTraq Integration
#### Steps: 
1. Optionally: If you do this the first time, you probably want to setup the *Local Integration* from above first. 
This is *only* needed to retrieve the setup parameters for this method. Afterwards you can remove the *Local 
Integration* again.
1. On your local repository open the context menu and go to `TortoiseGit > Settings > Issue Tracker Config` 
1. If you set up the *Local Integration* in the first step: In the `Effective` scope, check the `IBugTraqProvider` 
frame near the bottom. You should see your current values for the TurtleHub's UUID and parameters. Copy the parameters.
1. Change the scope to your desired scope, e.g. `Project`. In the `IBugTraqProvider` frame near the bottom, remove the 
`inherit` checkboxes and insert the 
UUIDs (a.k.a. GUIDs) and parameters for TurtleHub (e.g. from the previous step).
    1. The 32-bit UUID is: `{B2C6EC0F-8742-4792-9FDC-10635D2C118C}`
    1. The 64-bit UUID is: `{B2C6EC0F-8742-4792-9FDC-10635D2C118B}`
    1. Feel free to add both UUIDs if you want to share your config.
    
    ![TH-BugTraq-Plugin](/img/TH-BugTraq-Plugin.png)
1. Now you can delete your *Local Integration* entry from `Issue Tracker Integration` again, if you did create one.
1. You can share/commit your BugTraq git config (e.g. `.tgitconfig` file on `Project` scope). 
For an example, see [our own BugTraq config](.tgitconfig): 
  ```
  [bugtraq]
    ### TurtleHub specific config
    provideruuid = {B2C6EC0F-8742-4792-9FDC-10635D2C118C}
    provideruuid64 = {B2C6EC0F-8742-4792-9FDC-10635D2C118B}
    providerparams = "owner=dail8859;repository=TurtleHub;keyword=<None>;reffullrepo=True"
  ```


#### Further BugTraq configuration
If you look into the example file above or at the screenshots, you can see further BugTraq configurations. 
These are independent from TurtleHub. For more information about what they are and how to use them, use the `Help` 
button at the bottom: 

![TH-BugTraq-general](/img/TH-BugTraq-general.png)

Their main purpose is to provide links on issue numbers when browsing log messages in TurtleHub. They link to the 
issue's URL on the tracker: 

![TH-BugTraq-link](/img/TH-BugTraq-link.png)
* Make sure `bugtraq.url` refers to the tracker URL you want to refer to and add `%BUGID` in place of where the 
issue number goes. e.g.
`https://github.com/dail8859/TurtleHub/issues/%BUGID%`
* If `bugtraq.warnifnoissue` es enabled, it checks your current commit for issue numbers and warns you if you don't 
provide one when committing.
* Feel free to use this RegEx for `bugtraq.logregex`: `(?:\S+\/\S+)?#(\d+)` It will link against the 
short and extended issue notations.
  ```
  [bugtraq]
    ### general BugTraq config ###

    # Link issue numbers that are found in log browser messages to this URL:
    url = https://github.com/dail8859/TurtleHub/issues/%BUGID%
    
    # Find issue numbers in log browser messages according to this regex:
    logregex = "(?:\\S+\\/\\S+)?#(\\d+)"
    
    # Enable or disable warning, if no issue number is provided upon commit:
    warnifnoissue = false
  ```
* The other properties are ignored if TurtleHub is installed. However, *if the IBugTraqProvider properties are not set 
(or commented out)*, these still might be useful to provide for other project contributors without TurtleHub. If so, an 
edit box appears at the top right hand side instead. There, issue numbers can be inserted manually. Check TortoiseGit's 
*Help* documentation for further information.

  ![TH-no-TH-fallback](/img/TH-no-TH-fallback.png)
  ```
  [bugtraq]
    ### Fallback! For users without TurtleHub: Comment out the 'provider*' properties above! 
    # An input box will appear instead. It's content will be inserted with this syntax:
    message = "dail8859/TurtleHub#%BUGID%"
    append = true
    
    # Label shown next to the input field if no provider is present:
    label = "Issue/Pull Request #"
    
    # The typed issue / pull request IDs must be numbers:
    number = true
  ```


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
