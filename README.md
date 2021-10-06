## Introduction
This is the branch of Pi-Apps that reimagines the whole app store with a fresh perspective. It aims to improve the user-experience, reduce app-development-time, and increase installation reliability.  
When complete, this branch will be merged into the master branch.  
## Objectives:
- App-scripts will replace some commands with functions.
  - This adopts a more PiKISS approach to scripting, where nothing is written twice. Changing one function will improve everything that uses that function.
  - Functions will help developers to write quality code in less time. The learning curve may be slightly steeper, but the resulting benefits makes it worth it.
  - For example, we will use the `git_clone` function instead of `git clone`. This function will condense three commands into one:
  ```bash
  # before:
  rm -rf example-repo
  echo "Cloning example-repo..."
  git clone https://github.com/botspot/example-repo || error "failed to clone example.com"
  
  # after:
  git_clone https://github.com/botspot/example-repo || exit 1
  ```
- Error-handling will be more robust. The entire output will be checked for known errors, rather than the output limited to `pkg-install`.
  - As a result, more error-types will be categorized, meaning we will receive fewer error reports.
  - A dialog box will appear, explaining the error and what the user can do about it. Some types of errors will allow the user to send an error report, while others won't.
- App-status will be improved.
  - If an app fails to install, its status will be changed back to `uninstalled` if the type of error was designated to be an externally-caused error. This prevents apps from unnecessarily being marked as `corrupted` - somethins which currently frustrates many users.
- A new type of app: `package`
  - Pi-Apps has always been a collection of the hard-to-find software. If something was on apt, then it didn't belong in Pi-Apps.
  I originally intended Pi-Apps to run alongside an apt package-manager like `pi-packages`, but it's time to change that. With this branch, Pi-Apps includes a way to natively support installing apt packages.
  - This method doesn't require writing scripts. Each package-app, instead of having `install` or `uninstall` scripts, will simply have a `packages` file, containing a space-separated list of packages to install. Pi-Apps handles the rest, including app-status, installing and uninstalling, and will hide packages that aren't visible on the user's OS.
