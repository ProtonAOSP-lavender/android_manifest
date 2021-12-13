# ProtonAOSP-lavender

ProtonAOSP is a minimal custom Android ROM focused on UI/UX and performance, with a touch of security and privacy. It is based on [Android Open Source Project (AOSP)](https://source.android.com/).

## Getting source code

You must be running a 64-bit Linux distribution and must have installed some packages to build ProtonAOSP-lavender. Google recommends using [Ubuntu](http://www.ubuntu.com/download/desktop) for this and provides instructions for setting up the system (with Ubuntu-specific commands) on [the Android Open Source Project website](https://source.android.com/source/initializing.html#setting-up-a-linux-build-environment). Make sure you have the [repo tool](https://source.android.com/setup/build/downloading) set up. Also, you'll need to get familiar with [Git and Repo](http://source.android.com/source/using-repo.html). Once you have set up your machine according to the instructions by Google, return here and carry on with the rest of the instructions.

## Grabbing the source ##

[Repo](http://source.android.com/source/developing.html) is a tool provided by Google that
simplifies using [Git](http://git-scm.com/book) in the context of the Android source.

### Installing Repo ###

```bash
# Make a directory where Repo will be stored and add it to the path
$ mkdir ~/.bin
$ PATH=~/.bin:$PATH

# Download Repo itself
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/.bin/repo

# Make Repo executable
$ chmod a+x ~/.bin/repo
```

### Initializing Repo ###

```bash
# Create a directory for the source files
# You can name this directory however you want, just remember to replace
# WORKSPACE with your directory for the rest of this guide.
# This can be located anywhere (as long as the fs is case-sensitive)
$ mkdir WORKSPACE
$ cd WORKSPACE

# Install Repo in the created directory
# Use a real name/email combination, if you intend to submit patches
$ repo init -u https://github.com/ProtonAOSP-lavender/android_manifest -b sc
```

## Initializing Repo (Shallow clone) ##

```bash
# Create a directory for the source files
# You can name this directory however you want, just remember to replace
# WORKSPACE with your directory for the rest of this guide.
# This can be located anywhere (as long as the fs is case-sensitive)
$ mkdir WORKSPACE
$ cd WORKSPACE

# Install Repo in the created directory
# Use a real name/email combination, if you intend to submit patches
$ repo init --depth=1 -u https://github.com/ProtonAOSP-lavender/android_manifest -b sc
```

### Downloading the source tree ###

This is what you will run each time you want to pull in upstream changes. Keep in mind that on your first run, it is expected to take a while as it will download all the required Android source files and their change histories.

```bash
# Let Repo take care of all the hard work
#
# The -j# option specifies the number of concurrent download threads to run.
# 4 threads is a good number for most internet connections.
# You may need to adjust this value if you have a particularly slow connection.
$ repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags --optimized-fetch --prune
```

This is a large download that will take approximately 100 GB of disk space, so plan accordingly.

## Building

```bash
  $ . build/envsetup.sh
  $ lunch device_codename-userdebug
  $ m proton -j$(nproc --all) | tee log.txt
```

Good luck and happy building!
