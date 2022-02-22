---
sidebar_position: 6
title: Desktop Application
---

# Introduction

In addition to the web tool, there is also a desktop application for those who prefer that, which usually offers around a 3-5x performance boost over the web application as it is not subject to limitations in the browser. This page includes some brief details on how to use it.

# Obtaining The Release

The easiest way is to download the latest releases [here](https://github.com/genshinsim/gcsim/releases) for a one-click .exe file.

You can also build from source - simply install [go from here](https://go.dev/), then clone or download the Github repo. Navigate to the [cmd/gcsim](https://github.com/genshinsim/gcsim/tree/main/cmd/gcsim) folder, then run `go build` which should build the project and provide the same executable.

# Running The Application

You will need to open up a terminal session (either the command line or Powershell in Windows) in the same folder as the .exe, and then you can run commands by doing:

```
./gcsim.exe [[options]]
```

Where `[[options]]` should be replaced by any of the various command line flags. For full details, you can use `./gcsim.exe -help`, which will list all of the flags with details out.

The primary method of running the program is something like the following:

```
./gcsim.exe -c=hu_tao_geo.txt -out=hu_tao_geo.json.gz -gz
```

This runs the sim on a `hu_tao_geo.txt` config file (the same one as you see in the Viewer "Config" tab) that sits in the same folder as the application, and outputs the result to `hu_tao_geo.json.gz` which you can then upload to the [viewer here](https://gcsim.app/viewer).

You can also change the `-c` and `-out` flags to any arbitrary file path.
